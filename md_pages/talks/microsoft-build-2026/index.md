---
layout: default
title: "Construyendo un Runtime Python Multi-Tenant sobre Azure Functions — Microsoft Build 2026"
description: "Lecciones de la construcción de una plataforma real de automatización Python multi-tenant sobre Azure Functions."
---

# Construyendo un Runtime Python Multi-Tenant sobre Azure Functions

### Lecciones de una Plataforma Real de Automatización

**Microsoft Build 2026 · Agosto de 2026**

---

## El reto

¿Qué ocurre cuando queremos que miles de usuarios ejecuten automatizaciones Python sobre una plataforma serverless?

A primera vista, el problema parece sencillo.

Un usuario escribe unas pocas líneas de Python:

```python
main.py
```

Y espera que esas líneas puedan desencadenar integraciones con servicios como correo electrónico, plataformas de mensajería, hojas de cálculo, APIs de inteligencia artificial u otros servicios HTTP.

Pero detrás de esas pocas líneas aparecen preguntas arquitectónicas mucho más difíciles:

- múltiples usuarios compartiendo infraestructura;
- ejecuciones concurrentes;
- credenciales diferentes;
- escalado automático;
- ejecución basada en eventos;
- tareas programadas;
- control del consumo de recursos;
- aislamiento del estado específico de cada tenant;
- actualización de la plataforma sin obligar a los usuarios a reinstalar el SDK.

Por lo tanto, el problema interesante no era simplemente:

> **¿Cómo ejecutamos código Python?**

Era:

> **¿Cómo ejecutamos automatizaciones Python para múltiples tenants manteniendo una experiencia simple para el desarrollador?**

Esta pregunta se convirtió en la base de **Apider**, un runtime de automatización multi-tenant construido sobre **Azure Functions**.

El objetivo no era simplemente construir otro SDK de Python.

> **El objetivo era validar si Azure Functions podía servir como base para un runtime Python multi-tenant real.**

---

## ¿Qué ocurre realmente detrás de dos líneas de Python?

Una de las decisiones arquitectónicas más importantes fue separar la experiencia del desarrollador de la infraestructura necesaria para ejecutar el código.

Desde el punto de vista del usuario, automatizar debería sentirse como escribir funciones Python.

El desarrollador no debería tener que preocuparse por:

- aprovisionar infraestructura;
- administrar workers;
- implementar webhooks;
- programar tareas;
- gestionar individualmente cada integración;
- coordinar la ejecución distribuida.

En su lugar, el SDK proporciona una interfaz ligera.

Cuando el usuario escribe algo como:

```python
Telegram.send(...)
```

la integración no se ejecuta localmente dentro del proceso Python del usuario.

El SDK actúa como cliente.

La solicitud se envía mediante HTTPS al runtime y la ejecución ocurre en Azure.

Desde allí, el runtime puede interactuar con servicios externos y devolver el resultado al usuario.

Esto crea una separación arquitectónica importante:

```bash
Código Python del usuario
          │
          ▼
      SDK ligero
          │
        HTTPS
          │
          ▼
    Azure Functions
          │
     ┌────┼─────────────┐
     ▼    ▼             ▼
  Email Telegram     APIs HTTP
```

La interfaz permanece simple aunque detrás exista una infraestructura distribuida.

> **El desarrollador ve una API de Python. El runtime se encarga de la complejidad de ejecución.**

---

## **Problema #1 — Multi-Tenancy**

El primer problema apareció cuando múltiples usuarios comenzaron a compartir el mismo runtime.

Imaginemos dos usuarios ejecutando automatizaciones simultáneamente.

El usuario A tiene:

```bash
OPENAI_API_KEY=abc
```

El usuario B tiene:

```bash
OPENAI_API_KEY=xyz
```

Ambas ejecuciones pueden terminar utilizando el mismo proceso.

Eso introduce una pregunta crítica:

> **¿Cómo evitamos que las credenciales de una ejecución puedan interferir con otra?**

En un sistema multi-tenant, un error de aislamiento puede provocar:

- fuga de datos entre tenants;
- exposición de credenciales;
- facturación asociada al usuario incorrecto;
- dificultad para auditar ejecuciones;
- pérdida de confianza en la plataforma.

Por lo tanto, el runtime necesita mantener el contexto correspondiente a cada ejecución.

> **En multi-tenancy, el aislamiento no es una característica adicional. Es parte fundamental de la arquitectura.**

---

## **Aislamiento de contexto con `ContextVar`**

Una primera aproximación podría ser almacenar las credenciales en una variable global o en `os.environ`.

El problema es que ese estado pertenece al proceso.

Si múltiples ejecuciones comparten el mismo proceso, también pueden terminar compartiendo ese estado.

Por ejemplo:

```python
os.environ["OPENAI_API_KEY"] = key
```

En un runtime concurrente, una ejecución podría modificar el valor mientras otra todavía lo está utilizando.

El problema, por lo tanto, no era la concurrencia en sí.

Era:

> **¿Dónde almacenamos el estado asociado a cada ejecución?**

La solución fue utilizar `ContextVar`.

Conceptualmente:

```python
token = current_env.set(env)

try:
    result = execute()
finally:
    current_env.reset(token)
```

En lugar de tratar las credenciales como estado global del proceso, el runtime las asocia al contexto lógico de la ejecución actual.

El patrón puede utilizarse para mantener información como:

- `tenant_id`;
- credenciales;
- configuración;
- información de procesamiento;
- datos necesarios para logs y debugging.

> **El problema no era dónde ejecutar las funciones. Era dónde mantener de forma segura el estado de cada ejecución.**

Sin embargo, existe una distinción importante.

`ContextVar` **no es un sandbox**.

No crea:

- un proceso independiente;
- memoria físicamente aislada;
- límites de CPU;
- una frontera contra código arbitrario;
- protección contra un crash del proceso.

Proporciona una frontera de **contexto lógico**.

> **Aislamiento lógico ≠ aislamiento físico.**

<!-- AQUÍ VA EL GRÁFICO DE AISLAMIENTO DE CONTEXTO -->

---

## **Problema #2 — Seguridad**

Una vez resuelto el problema del contexto apareció otra pregunta:

> **¿Cómo transportamos las credenciales sin exponerlas?**

Cada usuario puede tener credenciales diferentes para servicios como:

- OpenAI;
- Stripe;
- Telegram;
- Google;
- APIs HTTP.

Estas credenciales no deberían viajar como texto plano ni quedar expuestas innecesariamente en código o configuración.

Por eso, el runtime utiliza diferentes capas de protección.

---

## **Cifrado con Fernet**

Apider utiliza Fernet para proteger el payload de credenciales.

El modelo es conceptualmente:

```bash
Credenciales
     │
     ▼
Cifrado local
     │
     ▼
Payload cifrado
     │
     ▼
    HTTPS
     │
     ▼
Azure Functions
     │
     ▼
Descifrado en memoria
     │
     ▼
Ejecución
```

Aquí existen dos mecanismos diferentes.

**HTTPS** protege el canal de transporte.

**Fernet** protege el contenido del payload.

Son capas distintas y complementarias.

> **HTTPS protege el canal. Fernet protege el payload.**

Las credenciales pueden descifrarse en memoria cuando son necesarias y mantenerse asociadas al contexto de la ejecución.

El objetivo es reducir su exposición y evitar convertir las credenciales de los usuarios en configuración permanente del runtime.

---

## **Problema #3 — Actualizaciones**

Después apareció otro problema:

> **¿Cómo actualizar la lógica del producto sin obligar a los usuarios a reinstalar el SDK?**

Si toda la lógica vive dentro del SDK, cada cambio requiere distribuir una nueva versión.

Esto puede generar:

- clientes atascados en versiones antiguas;
- más combinaciones de versiones que mantener;
- mayor coste de soporte;
- evolución más lenta del producto.

En entornos enterprise, una actualización puede además requerir revisión, QA, aprobaciones y despliegues coordinados.

Por eso, la arquitectura separó deliberadamente la interfaz del cliente de la lógica del runtime.

---

## **Arquitectura Thin Client / Fat Server**

La solución fue mantener el SDK lo más ligero posible y colocar la lógica que evoluciona en el servidor.

Cuando un usuario ejecuta:

```python
Telegram.send(...)
```

está utilizando una interfaz que representa una operación remota.

Conceptualmente:

```bash
Aplicación Python
        │
        ▼
    SDK ligero
        │
       HTTPS
        │
        ▼
   Runtime remoto
        │
   ┌────┼───────────┐
   ▼    ▼           ▼
Email Telegram    APIs HTTP
```

Esto permite corregir errores, mejorar integraciones y agregar funcionalidades sin que el usuario tenga que reinstalar el SDK para cada cambio de lógica interna.

> **El SDK es la interfaz. El runtime es donde vive la lógica que evoluciona.**

La decisión tiene un trade-off evidente:

La experiencia del desarrollador se vuelve más sencilla.

La infraestructura se vuelve más compleja.

Pero esa complejidad queda centralizada en el runtime.

---

## **Problema #4 — Automatización basada en eventos**

El siguiente problema fue convertir el runtime en una plataforma capaz de reaccionar ante eventos.

Las empresas generan eventos constantemente:

- pagos;
- pedidos;
- pushes de código;
- tickets;
- notificaciones;
- cambios de estado.

Plataformas como Stripe, GitHub y Shopify pueden enviar webhooks cuando ocurre uno de estos eventos.

Pero recibir una petición HTTP no es suficiente para construir un sistema de automatización confiable.

El runtime debe considerar:

- eventos duplicados;
- eventos perdidos;
- reintentos;
- idempotencia;
- autenticación;
- validación de firmas;
- monitoreo;
- recuperación;
- disponibilidad del endpoint.

> **El problema no es recibir un webhook. El problema es convertir eventos externos en ejecuciones confiables.**

---

## **Solución — Webhooks**

El evento puede ocurrir mucho tiempo después de que se registró la automatización.

Puede llegar:

- minutos después;
- horas después;
- días después.

Por lo tanto, el runtime necesita persistir suficiente información para reconstruir la ejecución cuando llegue el evento.

Para este escenario, Apider utiliza **Azure Table Storage** para almacenar la información necesaria asociada a los webhooks, con acceso controlado mediante **Azure RBAC**.

RBAC significa *Role-Based Access Control*.

El flujo puede representarse así:

```bash
Registro del webhook
        │
        ▼
Persistencia del estado
        │
        ▼
Azure Table Storage
        │
        │
        │      tiempo después
        │             │
        │             ▼
        │          Webhook
        │             │
        └─────────────┘
                      │
                      ▼
             Recuperar contexto
                      │
                      ▼
                  Ejecutar
```

En una ejecución inmediata, las credenciales pueden acompañar a la solicitud.

En un webhook, la ejecución futura necesita recuperar el contexto necesario para ejecutarse.

> **La persistencia existe porque el evento puede sobrevivir a la solicitud que creó la automatización.**

---

## **Scheduler Distribuido**

Los eventos externos no son la única forma de iniciar una automatización.

También necesitamos ejecutar funciones periódicamente.

Por ejemplo:

```python
run_every(...)
```

Una solución tradicional sería utilizar un cron job en una máquina local.

Pero eso rompe el modelo serverless.

El usuario no debería tener que mantener una máquina encendida para ejecutar una tarea periódica.

La solución fue almacenar la definición de los trabajos programados en Azure Table Storage.

Un **Timer Trigger** se ejecuta periódicamente, busca los trabajos pendientes y dispara el runtime correspondiente.

Conceptualmente:

```bash
              Azure Table Storage
                      │
                      ▼
             Trabajos programados
                      │
                      ▼
                Timer Trigger
                      │
                  cada minuto
                      │
                      ▼
              Trabajos pendientes
                      │
                      ▼
                   Runtime
                      │
                      ▼
               Función Python
```

Desde el punto de vista del usuario, solamente existe una función Python.

La infraestructura se encarga de almacenar, detectar e iniciar los trabajos.

> **El usuario ve una función programada. La plataforma administra el scheduler.**

---

## **Arquitectura Completa**

Después de resolver aislamiento, seguridad, actualizaciones, webhooks y scheduling, la arquitectura convergió alrededor de un único runtime.

El SDK es la interfaz.

La ejecución ocurre en Azure.

```bash
                         APIDER
                           │
                      Python SDK
                           │
                         HTTPS
                           │
                           ▼
                  ┌─────────────────┐
                  │ Azure Functions │
                  │     Runtime     │
                  └─────────────────┘
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
      Ejecución         Webhooks        Scheduler
      directa
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                    Contexto de tenant
                           │
                           ▼
                     Integraciones
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
           Email        Telegram      APIs HTTP
```

La complejidad se encuentra en la infraestructura.

La experiencia del desarrollador permanece simple.

> **Un único runtime puede exponer múltiples capacidades sin obligar al desarrollador a administrar múltiples sistemas.**

<!-- AQUÍ VA EL GRÁFICO DE ARQUITECTURA COMPLETA -->

---

## **Resultados obtenidos**

La arquitectura permitió construir un runtime multi-tenant funcional sobre Azure Functions.

Entre los resultados:

- runtime multi-tenant funcional;
- aislamiento de contexto por ejecución;
- arquitectura serverless;
- transporte cifrado de credenciales;
- webhooks persistentes;
- scheduler distribuido;
- SDK publicado en PyPI;
- escalado automático mediante Azure Functions;
- lógica de negocio centralizada en el runtime.

Pero los resultados técnicos también produjeron varias conclusiones.

### **ContextVar fue más importante de lo esperado**

El aislamiento del contexto terminó siendo uno de los elementos fundamentales del runtime.

### **La simplicidad para el usuario genera complejidad interna**

Dos líneas de Python pueden representar una cadena completa de operaciones distribuidas.

### **Azure Functions puede soportar arquitecturas más complejas de lo que parece**

El modelo serverless puede convertirse en la base de un runtime más completo.

### **Diseñar para multi-tenancy desde el inicio evita problemas futuros**

El aislamiento afecta prácticamente todas las capas del sistema.

---

## **Lecciones aprendidas**

### **Diseñar el aislamiento antes que las integraciones**

Si tuviera que volver a empezar, diseñaría el aislamiento incluso antes que las integraciones.

Las integraciones individuales eran relativamente sencillas.

Los problemas más complejos aparecieron alrededor de la concurrencia y del estado compartido.

> **En un runtime multi-tenant, la frontera entre ejecuciones es más importante que la integración individual.**

### **La concurrencia cambia la forma de pensar el estado**

Cuando varias ejecuciones pueden compartir un proceso, cualquier estado mutable debe analizarse cuidadosamente.

La pregunta no es solamente:

> "¿Esta variable funciona?"

Sino:

> **"¿Quién puede verla, durante cuánto tiempo y bajo qué contexto?"**

### **Serverless no significa ausencia de arquitectura**

Aunque Azure Functions abstrae gran parte de la infraestructura, siguen existiendo problemas de:

- estado;
- concurrencia;
- eventos;
- persistencia;
- reintentos;
- scheduling;
- seguridad;
- observabilidad.

Serverless elimina parte de la infraestructura que el desarrollador debe administrar.

No elimina los problemas arquitectónicos.

### **La abstracción correcta puede ocultar mucha complejidad**

El objetivo de una buena API no es necesariamente que el sistema sea simple.

Es conseguir que la complejidad que el desarrollador no necesita controlar permanezca detrás de una frontera bien definida.

---

## **Demo**

Todo lo que hemos visto hasta ahora existe para conseguir que la experiencia final sea esto:

```python
automation()
```

Dos o tres líneas de Python pueden representar una ejecución que atraviesa múltiples componentes.

Detrás existe:

- aislamiento multi-tenant;
- ejecución distribuida;
- manejo de credenciales;
- integraciones;
- persistencia;
- eventos;
- scheduling;
- escalado automático.

La demo mostró precisamente esa diferencia entre lo que observa el desarrollador y lo que ocurre detrás.

```bash
       Código Python
            │
            ▼
       SDK ligero
            │
          HTTPS
            │
            ▼
     Azure Functions
            │
     ┌──────┼──────┐
     ▼      ▼      ▼
 Contexto Seguridad Eventos
     │      │      │
     └──────┼──────┘
            ▼
        Ejecución
            │
            ▼
      Integraciones
```

> **La experiencia final es pequeña porque el runtime absorbe la complejidad.**

---

## **Ideas Clave**

La presentación puede resumirse en cuatro ideas.

### **El reto no era ejecutar código**

Ejecutar Python era relativamente sencillo.

El reto era ejecutarlo para múltiples usuarios sin que sus ejecuciones interfirieran entre sí.

### **ContextVar permitió aislamiento por ejecución**

El estado específico de cada ejecución necesitaba estar asociado al contexto lógico y no a un estado global compartido.

### **Azure Functions proporcionó la infraestructura serverless**

El runtime pudo utilizar Azure Functions como base para ejecución basada en eventos y escalado automático.

### **La simplicidad para el desarrollador requiere infraestructura**

El desarrollador ve una API Python sencilla.

Detrás existe:

- un runtime;
- aislamiento;
- seguridad;
- persistencia;
- eventos;
- scheduling;
- integraciones;
- infraestructura cloud.

> **La API puede ser pequeña aunque el sistema detrás sea grande.**

---

## **La idea central**

Al comenzar el proyecto, parecía que estaba construyendo un SDK.

Pero con el tiempo quedó claro que el SDK era solamente la parte visible.

La arquitectura real era un runtime.

El SDK proporciona la interfaz.

Azure Functions proporciona la infraestructura de ejecución.

El runtime proporciona:

- aislamiento;
- ejecución;
- integración;
- manejo de eventos;
- scheduling;
- coordinación.

Esta distinción cambia completamente la forma de pensar el proyecto.

No se trata solamente de construir una librería que facilite llamadas a APIs.

Se trata de construir una capa de ejecución que permita que esas operaciones sean utilizadas por múltiples usuarios dentro de una infraestructura compartida.

> **El SDK es la interfaz. El runtime es el sistema.**

---

## **Conclusión**

La pregunta original era:

> **¿Cómo ejecutar código Python escrito por miles de usuarios en Azure Functions de forma segura?**

La respuesta no fue una única tecnología.

Fue una combinación de decisiones arquitectónicas:

- aislamiento de contexto;
- manejo seguro de credenciales;
- arquitectura Thin Client / Fat Server;
- ejecución serverless;
- webhooks;
- persistencia;
- scheduler distribuido;
- escalado automático.

El resultado fue una experiencia extremadamente sencilla para el desarrollador.

El usuario escribe Python.

La plataforma se encarga del resto.

Pero esa simplicidad no significa que la infraestructura sea simple.

Significa que la complejidad está encapsulada detrás de una interfaz.

> **La complejidad no desaparece. Se mueve hacia el runtime.**

---

## **Materiales**

Esta página funciona como punto de referencia para los materiales de la charla presentada en **Microsoft Build 2026**.

A medida que estén disponibles, se irán incorporando aquí.

### **Slides**

[Ver presentación →](...)

### **PDF**

[Descargar PDF de la presentación →](...)

### **Código y demos**

[Ver código y demos →](...)

### **Grabación**

[Ver grabación →](...)

---

## **Galería**

Registro visual de la presentación en **Microsoft Build 2026**.

### **Fotografías**

![Jorge de la Flor durante la presentación en Microsoft Build 2026](...)

![Jorge de la Flor en Microsoft Build 2026](...)

### **Material de speaker**

[Ver material de speaker →](...)

---

## **Recursos**

La charla se apoya en el proyecto Apider y en las tecnologías utilizadas para construir el runtime.

### **Proyectos**

- [Apider →](...)
- [Apider Python SDK →](...)

### **Azure**

- [Azure Functions →](...)
- [Azure Table Storage →](...)
- [Azure RBAC →](...)

### **Python**

- [`contextvars` →](...)

### **Seguridad**

- [Fernet →](...)

### **Artículos**

- [Artículo relacionado →](...)
- [Artículo relacionado →](...)

---

## **Ponente**

### **Jorge de la Flor**

*Software & Cyber-Physical Systems Developer*

Trabajo en arquitectura de software, sistemas distribuidos, sistemas embebidos y desarrollo de herramientas.

Mis intereses se encuentran en la intersección entre software, sistemas e infraestructura, especialmente en sistemas donde la ejecución, el aislamiento y la experiencia del desarrollador requieren decisiones arquitectónicas explícitas.

Soy el creador de **Apider**, un runtime de automatización basado en Python y construido sobre Azure Functions.

[Sobre mí →](/md_pages/about/)

[Portfolio →](/)

---

## **Sobre la presentación**

| | |
|---|---|
| **Evento** | Microsoft Build 2026 |
| **Lugar** | Microsoft Build |
| **Fecha** | Agosto de 2026 |
| **Título** | Building a Multi-Tenant Python Runtime on Azure Functions |
| **Subtítulo** | Lessons from a Real Automation Platform |
| **Temas** | Python · Azure Functions · Multi-Tenancy · Serverless · Sistemas Distribuidos · Arquitectura de Runtimes |

---

## **Cierre**

> **BUILD THE RUNTIME.**
>
> **ISOLATE THE EXECUTION.**
>
> **HIDE THE COMPLEXITY.**

**Jorge de la Flor**

Software & Cyber-Physical Systems Developer

---

[← Volver a Charlas](/md_pages/talks/)


### Lecciones de una Plataforma Real de Automatización

**Microsoft Build 2026 · Agosto de 2026**

---

## El reto

¿Qué ocurre cuando queremos que miles de usuarios ejecuten automatizaciones Python sobre una plataforma serverless?

A primera vista, el problema parece sencillo.

Un usuario escribe unas pocas líneas de Python:

```python
main.py
```

Y espera que esas líneas puedan desencadenar integraciones con servicios como correo electrónico, plataformas de mensajería, hojas de cálculo, APIs de inteligencia artificial u otros servicios HTTP.

Pero detrás de esas pocas líneas aparecen preguntas arquitectónicas mucho más difíciles:

- múltiples usuarios compartiendo infraestructura;
- ejecuciones concurrentes;
- credenciales diferentes;
- escalado automático;
- ejecución basada en eventos;
- tareas programadas;
- control del consumo de recursos;
- aislamiento del estado específico de cada tenant;
- actualización de la plataforma sin obligar a los usuarios a reinstalar el SDK.

Por lo tanto, el problema interesante no era simplemente:

> **¿Cómo ejecutamos código Python?**

Era:

> **¿Cómo ejecutamos automatizaciones Python para múltiples tenants manteniendo una experiencia simple para el desarrollador?**

Esta pregunta se convirtió en la base de **Apider**, un runtime de automatización multi-tenant construido sobre **Azure Functions**.

El objetivo no era simplemente construir otro SDK de Python.

> **El objetivo era validar si Azure Functions podía servir como base para un runtime Python multi-tenant real.**

---

## ¿Qué ocurre realmente detrás de dos líneas de Python?

Una de las decisiones arquitectónicas más importantes fue separar la experiencia del desarrollador de la infraestructura necesaria para ejecutar el código.

Desde el punto de vista del usuario, automatizar debería sentirse como escribir funciones Python.

El desarrollador no debería tener que preocuparse por:

- aprovisionar infraestructura;
- administrar workers;
- implementar webhooks;
- programar tareas;
- gestionar individualmente cada integración;
- coordinar la ejecución distribuida.

En su lugar, el SDK proporciona una interfaz ligera.

Cuando el usuario escribe algo como:

```python
Telegram.send(...)
```

la integración no se ejecuta localmente dentro del proceso Python del usuario.

El SDK actúa como cliente.

La solicitud se envía mediante HTTPS al runtime y la ejecución ocurre en Azure.

Desde allí, el runtime puede interactuar con servicios externos y devolver el resultado al usuario.

Esto crea una separación arquitectónica importante:

```bash
Código Python del usuario
          │
          ▼
      SDK ligero
          │
        HTTPS
          │
          ▼
    Azure Functions
          │
     ┌────┼─────────────┐
     ▼    ▼             ▼
  Email Telegram     APIs HTTP
```

La interfaz permanece simple aunque detrás exista una infraestructura distribuida.

> **El desarrollador ve una API de Python. El runtime se encarga de la complejidad de ejecución.**

---

## **Problema #1 — Multi-Tenancy**

El primer problema apareció cuando múltiples usuarios comenzaron a compartir el mismo runtime.

Imaginemos dos usuarios ejecutando automatizaciones simultáneamente.

El usuario A tiene:

```bash
OPENAI_API_KEY=abc
```

El usuario B tiene:

```bash
OPENAI_API_KEY=xyz
```

Ambas ejecuciones pueden terminar utilizando el mismo proceso.

Eso introduce una pregunta crítica:

> **¿Cómo evitamos que las credenciales de una ejecución puedan interferir con otra?**

En un sistema multi-tenant, un error de aislamiento puede provocar:

- fuga de datos entre tenants;
- exposición de credenciales;
- facturación asociada al usuario incorrecto;
- dificultad para auditar ejecuciones;
- pérdida de confianza en la plataforma.

Por lo tanto, el runtime necesita mantener el contexto correspondiente a cada ejecución.

> **En multi-tenancy, el aislamiento no es una característica adicional. Es parte fundamental de la arquitectura.**

---

## **Aislamiento de contexto con `ContextVar`**

Una primera aproximación podría ser almacenar las credenciales en una variable global o en `os.environ`.

El problema es que ese estado pertenece al proceso.

Si múltiples ejecuciones comparten el mismo proceso, también pueden terminar compartiendo ese estado.

Por ejemplo:

```python
os.environ["OPENAI_API_KEY"] = key
```

En un runtime concurrente, una ejecución podría modificar el valor mientras otra todavía lo está utilizando.

El problema, por lo tanto, no era la concurrencia en sí.

Era:

> **¿Dónde almacenamos el estado asociado a cada ejecución?**

La solución fue utilizar `ContextVar`.

Conceptualmente:

```python
token = current_env.set(env)

try:
    result = execute()
finally:
    current_env.reset(token)
```

En lugar de tratar las credenciales como estado global del proceso, el runtime las asocia al contexto lógico de la ejecución actual.

El patrón puede utilizarse para mantener información como:

- `tenant_id`;
- credenciales;
- configuración;
- información de procesamiento;
- datos necesarios para logs y debugging.

> **El problema no era dónde ejecutar las funciones. Era dónde mantener de forma segura el estado de cada ejecución.**

Sin embargo, existe una distinción importante.

`ContextVar` **no es un sandbox**.

No crea:

- un proceso independiente;
- memoria físicamente aislada;
- límites de CPU;
- una frontera contra código arbitrario;
- protección contra un crash del proceso.

Proporciona una frontera de **contexto lógico**.

> **Aislamiento lógico ≠ aislamiento físico.**

<!-- AQUÍ VA EL GRÁFICO DE AISLAMIENTO DE CONTEXTO -->

---

## **Problema #2 — Seguridad**

Una vez resuelto el problema del contexto apareció otra pregunta:

> **¿Cómo transportamos las credenciales sin exponerlas?**

Cada usuario puede tener credenciales diferentes para servicios como:

- OpenAI;
- Stripe;
- Telegram;
- Google;
- APIs HTTP.

Estas credenciales no deberían viajar como texto plano ni quedar expuestas innecesariamente en código o configuración.

Por eso, el runtime utiliza diferentes capas de protección.

---

## **Cifrado con Fernet**

Apider utiliza Fernet para proteger el payload de credenciales.

El modelo es conceptualmente:

```bash
Credenciales
     │
     ▼
Cifrado local
     │
     ▼
Payload cifrado
     │
     ▼
    HTTPS
     │
     ▼
Azure Functions
     │
     ▼
Descifrado en memoria
     │
     ▼
Ejecución
```

Aquí existen dos mecanismos diferentes.

**HTTPS** protege el canal de transporte.

**Fernet** protege el contenido del payload.

Son capas distintas y complementarias.

> **HTTPS protege el canal. Fernet protege el payload.**

Las credenciales pueden descifrarse en memoria cuando son necesarias y mantenerse asociadas al contexto de la ejecución.

El objetivo es reducir su exposición y evitar convertir las credenciales de los usuarios en configuración permanente del runtime.

---

## **Problema #3 — Actualizaciones**

Después apareció otro problema:

> **¿Cómo actualizar la lógica del producto sin obligar a los usuarios a reinstalar el SDK?**

Si toda la lógica vive dentro del SDK, cada cambio requiere distribuir una nueva versión.

Esto puede generar:

- clientes atascados en versiones antiguas;
- más combinaciones de versiones que mantener;
- mayor coste de soporte;
- evolución más lenta del producto.

En entornos enterprise, una actualización puede además requerir revisión, QA, aprobaciones y despliegues coordinados.

Por eso, la arquitectura separó deliberadamente la interfaz del cliente de la lógica del runtime.

---

## **Arquitectura Thin Client / Fat Server**

La solución fue mantener el SDK lo más ligero posible y colocar la lógica que evoluciona en el servidor.

Cuando un usuario ejecuta:

```python
Telegram.send(...)
```

está utilizando una interfaz que representa una operación remota.

Conceptualmente:

```bash
Aplicación Python
        │
        ▼
    SDK ligero
        │
       HTTPS
        │
        ▼
   Runtime remoto
        │
   ┌────┼───────────┐
   ▼    ▼           ▼
Email Telegram    APIs HTTP
```

Esto permite corregir errores, mejorar integraciones y agregar funcionalidades sin que el usuario tenga que reinstalar el SDK para cada cambio de lógica interna.

> **El SDK es la interfaz. El runtime es donde vive la lógica que evoluciona.**

La decisión tiene un trade-off evidente:

La experiencia del desarrollador se vuelve más sencilla.

La infraestructura se vuelve más compleja.

Pero esa complejidad queda centralizada en el runtime.

---

## **Problema #4 — Automatización basada en eventos**

El siguiente problema fue convertir el runtime en una plataforma capaz de reaccionar ante eventos.

Las empresas generan eventos constantemente:

- pagos;
- pedidos;
- pushes de código;
- tickets;
- notificaciones;
- cambios de estado.

Plataformas como Stripe, GitHub y Shopify pueden enviar webhooks cuando ocurre uno de estos eventos.

Pero recibir una petición HTTP no es suficiente para construir un sistema de automatización confiable.

El runtime debe considerar:

- eventos duplicados;
- eventos perdidos;
- reintentos;
- idempotencia;
- autenticación;
- validación de firmas;
- monitoreo;
- recuperación;
- disponibilidad del endpoint.

> **El problema no es recibir un webhook. El problema es convertir eventos externos en ejecuciones confiables.**

---

## **Solución — Webhooks**

El evento puede ocurrir mucho tiempo después de que se registró la automatización.

Puede llegar:

- minutos después;
- horas después;
- días después.

Por lo tanto, el runtime necesita persistir suficiente información para reconstruir la ejecución cuando llegue el evento.

Para este escenario, Apider utiliza **Azure Table Storage** para almacenar la información necesaria asociada a los webhooks, con acceso controlado mediante **Azure RBAC**.

RBAC significa *Role-Based Access Control*.

El flujo puede representarse así:

```bash
Registro del webhook
        │
        ▼
Persistencia del estado
        │
        ▼
Azure Table Storage
        │
        │
        │      tiempo después
        │             │
        │             ▼
        │          Webhook
        │             │
        └─────────────┘
                      │
                      ▼
             Recuperar contexto
                      │
                      ▼
                  Ejecutar
```

En una ejecución inmediata, las credenciales pueden acompañar a la solicitud.

En un webhook, la ejecución futura necesita recuperar el contexto necesario para ejecutarse.

> **La persistencia existe porque el evento puede sobrevivir a la solicitud que creó la automatización.**

---

## **Scheduler Distribuido**

Los eventos externos no son la única forma de iniciar una automatización.

También necesitamos ejecutar funciones periódicamente.

Por ejemplo:

```python
run_every(...)
```

Una solución tradicional sería utilizar un cron job en una máquina local.

Pero eso rompe el modelo serverless.

El usuario no debería tener que mantener una máquina encendida para ejecutar una tarea periódica.

La solución fue almacenar la definición de los trabajos programados en Azure Table Storage.

Un **Timer Trigger** se ejecuta periódicamente, busca los trabajos pendientes y dispara el runtime correspondiente.

Conceptualmente:

```bash
              Azure Table Storage
                      │
                      ▼
             Trabajos programados
                      │
                      ▼
                Timer Trigger
                      │
                  cada minuto
                      │
                      ▼
              Trabajos pendientes
                      │
                      ▼
                   Runtime
                      │
                      ▼
               Función Python
```

Desde el punto de vista del usuario, solamente existe una función Python.

La infraestructura se encarga de almacenar, detectar e iniciar los trabajos.

> **El usuario ve una función programada. La plataforma administra el scheduler.**

---

## **Arquitectura Completa**

Después de resolver aislamiento, seguridad, actualizaciones, webhooks y scheduling, la arquitectura convergió alrededor de un único runtime.

El SDK es la interfaz.

La ejecución ocurre en Azure.

```bash
                         APIDER
                           │
                      Python SDK
                           │
                         HTTPS
                           │
                           ▼
                  ┌─────────────────┐
                  │ Azure Functions │
                  │     Runtime     │
                  └─────────────────┘
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
      Ejecución         Webhooks        Scheduler
      directa
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                    Contexto de tenant
                           │
                           ▼
                     Integraciones
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
           Email        Telegram      APIs HTTP
```

La complejidad se encuentra en la infraestructura.

La experiencia del desarrollador permanece simple.

> **Un único runtime puede exponer múltiples capacidades sin obligar al desarrollador a administrar múltiples sistemas.**

<!-- AQUÍ VA EL GRÁFICO DE ARQUITECTURA COMPLETA -->

---

## **Resultados obtenidos**

La arquitectura permitió construir un runtime multi-tenant funcional sobre Azure Functions.

Entre los resultados:

- runtime multi-tenant funcional;
- aislamiento de contexto por ejecución;
- arquitectura serverless;
- transporte cifrado de credenciales;
- webhooks persistentes;
- scheduler distribuido;
- SDK publicado en PyPI;
- escalado automático mediante Azure Functions;
- lógica de negocio centralizada en el runtime.

Pero los resultados técnicos también produjeron varias conclusiones.

### **ContextVar fue más importante de lo esperado**

El aislamiento del contexto terminó siendo uno de los elementos fundamentales del runtime.

### **La simplicidad para el usuario genera complejidad interna**

Dos líneas de Python pueden representar una cadena completa de operaciones distribuidas.

### **Azure Functions puede soportar arquitecturas más complejas de lo que parece**

El modelo serverless puede convertirse en la base de un runtime más completo.

### **Diseñar para multi-tenancy desde el inicio evita problemas futuros**

El aislamiento afecta prácticamente todas las capas del sistema.

---

## **Lecciones aprendidas**

### **Diseñar el aislamiento antes que las integraciones**

Si tuviera que volver a empezar, diseñaría el aislamiento incluso antes que las integraciones.

Las integraciones individuales eran relativamente sencillas.

Los problemas más complejos aparecieron alrededor de la concurrencia y del estado compartido.

> **En un runtime multi-tenant, la frontera entre ejecuciones es más importante que la integración individual.**

### **La concurrencia cambia la forma de pensar el estado**

Cuando varias ejecuciones pueden compartir un proceso, cualquier estado mutable debe analizarse cuidadosamente.

La pregunta no es solamente:

> "¿Esta variable funciona?"

Sino:

> **"¿Quién puede verla, durante cuánto tiempo y bajo qué contexto?"**

### **Serverless no significa ausencia de arquitectura**

Aunque Azure Functions abstrae gran parte de la infraestructura, siguen existiendo problemas de:

- estado;
- concurrencia;
- eventos;
- persistencia;
- reintentos;
- scheduling;
- seguridad;
- observabilidad.

Serverless elimina parte de la infraestructura que el desarrollador debe administrar.

No elimina los problemas arquitectónicos.

### **La abstracción correcta puede ocultar mucha complejidad**

El objetivo de una buena API no es necesariamente que el sistema sea simple.

Es conseguir que la complejidad que el desarrollador no necesita controlar permanezca detrás de una frontera bien definida.

---

## **Demo**

Todo lo que hemos visto hasta ahora existe para conseguir que la experiencia final sea esto:

```python
automation()
```

Dos o tres líneas de Python pueden representar una ejecución que atraviesa múltiples componentes.

Detrás existe:

- aislamiento multi-tenant;
- ejecución distribuida;
- manejo de credenciales;
- integraciones;
- persistencia;
- eventos;
- scheduling;
- escalado automático.

La demo mostró precisamente esa diferencia entre lo que observa el desarrollador y lo que ocurre detrás.

```bash
       Código Python
            │
            ▼
       SDK ligero
            │
          HTTPS
            │
            ▼
     Azure Functions
            │
     ┌──────┼──────┐
     ▼      ▼      ▼
 Contexto Seguridad Eventos
     │      │      │
     └──────┼──────┘
            ▼
        Ejecución
            │
            ▼
      Integraciones
```

> **La experiencia final es pequeña porque el runtime absorbe la complejidad.**

---

## **Ideas Clave**

La presentación puede resumirse en cuatro ideas.

### **El reto no era ejecutar código**

Ejecutar Python era relativamente sencillo.

El reto era ejecutarlo para múltiples usuarios sin que sus ejecuciones interfirieran entre sí.

### **ContextVar permitió aislamiento por ejecución**

El estado específico de cada ejecución necesitaba estar asociado al contexto lógico y no a un estado global compartido.

### **Azure Functions proporcionó la infraestructura serverless**

El runtime pudo utilizar Azure Functions como base para ejecución basada en eventos y escalado automático.

### **La simplicidad para el desarrollador requiere infraestructura**

El desarrollador ve una API Python sencilla.

Detrás existe:

- un runtime;
- aislamiento;
- seguridad;
- persistencia;
- eventos;
- scheduling;
- integraciones;
- infraestructura cloud.

> **La API puede ser pequeña aunque el sistema detrás sea grande.**

---

## **La idea central**

Al comenzar el proyecto, parecía que estaba construyendo un SDK.

Pero con el tiempo quedó claro que el SDK era solamente la parte visible.

La arquitectura real era un runtime.

El SDK proporciona la interfaz.

Azure Functions proporciona la infraestructura de ejecución.

El runtime proporciona:

- aislamiento;
- ejecución;
- integración;
- manejo de eventos;
- scheduling;
- coordinación.

Esta distinción cambia completamente la forma de pensar el proyecto.

No se trata solamente de construir una librería que facilite llamadas a APIs.

Se trata de construir una capa de ejecución que permita que esas operaciones sean utilizadas por múltiples usuarios dentro de una infraestructura compartida.

> **El SDK es la interfaz. El runtime es el sistema.**

---

## **Conclusión**

La pregunta original era:

> **¿Cómo ejecutar código Python escrito por miles de usuarios en Azure Functions de forma segura?**

La respuesta no fue una única tecnología.

Fue una combinación de decisiones arquitectónicas:

- aislamiento de contexto;
- manejo seguro de credenciales;
- arquitectura Thin Client / Fat Server;
- ejecución serverless;
- webhooks;
- persistencia;
- scheduler distribuido;
- escalado automático.

El resultado fue una experiencia extremadamente sencilla para el desarrollador.

El usuario escribe Python.

La plataforma se encarga del resto.

Pero esa simplicidad no significa que la infraestructura sea simple.

Significa que la complejidad está encapsulada detrás de una interfaz.

> **La complejidad no desaparece. Se mueve hacia el runtime.**

---

## **Materiales**

Esta página funciona como punto de referencia para los materiales de la charla presentada en **Microsoft Build 2026**.

A medida que estén disponibles, se irán incorporando aquí.

### **Slides**

[Ver presentación →](...)

### **PDF**

[Descargar PDF de la presentación →](...)

### **Código y demos**

[Ver código y demos →](...)

### **Grabación**

[Ver grabación →](...)

---

## **Galería**

Registro visual de la presentación en **Microsoft Build 2026**.

### **Fotografías**

![Jorge de la Flor durante la presentación en Microsoft Build 2026](...)

![Jorge de la Flor en Microsoft Build 2026](...)

### **Material de speaker**

[Ver material de speaker →](...)

---

## **Recursos**

La charla se apoya en el proyecto Apider y en las tecnologías utilizadas para construir el runtime.

### **Proyectos**

- [Apider →](...)
- [Apider Python SDK →](...)

### **Azure**

- [Azure Functions →](...)
- [Azure Table Storage →](...)
- [Azure RBAC →](...)

### **Python**

- [`contextvars` →](...)

### **Seguridad**

- [Fernet →](...)

### **Artículos**

- [Artículo relacionado →](...)
- [Artículo relacionado →](...)

---

## **Ponente**

### **Jorge de la Flor**

*Software & Cyber-Physical Systems Developer*

Trabajo en arquitectura de software, sistemas distribuidos, sistemas embebidos y desarrollo de herramientas.

Mis intereses se encuentran en la intersección entre software, sistemas e infraestructura, especialmente en sistemas donde la ejecución, el aislamiento y la experiencia del desarrollador requieren decisiones arquitectónicas explícitas.

Soy el creador de **Apider**, un runtime de automatización basado en Python y construido sobre Azure Functions.

[Sobre mí →](/md_pages/about/)

[Portfolio →](/)

---

## **Sobre la presentación**

| | |
|---|---|
| **Evento** | Microsoft Build 2026 |
| **Lugar** | Microsoft Build |
| **Fecha** | Agosto de 2026 |
| **Título** | Building a Multi-Tenant Python Runtime on Azure Functions |
| **Subtítulo** | Lessons from a Real Automation Platform |
| **Temas** | Python · Azure Functions · Multi-Tenancy · Serverless · Sistemas Distribuidos · Arquitectura de Runtimes |

---

## **Cierre**

> **BUILD THE RUNTIME.**
>
> **ISOLATE THE EXECUTION.**
>
> **HIDE THE COMPLEXITY.**

**Jorge de la Flor**

Software & Cyber-Physical Systems Developer

---

[← Volver a Charlas](/md_pages/talks/)