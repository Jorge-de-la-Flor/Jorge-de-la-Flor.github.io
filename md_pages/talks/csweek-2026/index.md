---
layout: default
title: "Aislamiento y Límites de Confianza en Producción — CS Week Perú 2026"
description: "Diseñando sistemas que contienen el impacto de los fallos mediante límites de confianza, invariantes y aislamiento."
---

# Aislamiento y Límites de Confianza en Producción

### Diseñando sistemas que contienen el impacto de los fallos

**CS Week Perú 2026 · Lima, Perú · Agosto de 2026**

---

## Cuando algo falla, ¿qué puede afectar?

Diseñar sistemas confiables no significa asumir que los fallos pueden eliminarse por completo.

Los componentes fallan. Las dependencias dejan de responder. Los procesos terminan. Los recursos se agotan. Los mensajes pueden retransmitirse.

La pregunta interesante, entonces, no es solamente:

> **¿Cómo evitamos que falle?**

También debemos preguntarnos:

> **¿Qué puede afectar cuando falle?**

Esta fue la idea central de mi charla en **CS Week Perú 2026**.

A partir de ella exploré una forma de diseñar sistemas utilizando **invariantes arquitectónicas, límites de confianza y mecanismos de aislamiento** para reducir el *blast radius* de errores y comportamientos inesperados.

El objetivo no es construir sistemas que nunca fallen.

> **El objetivo es controlar hasta dónde puede propagarse un fallo.**

---

## Los tests no cuentan toda la historia

Una suite de unit tests puede demostrar que una función se comporta correctamente bajo determinados escenarios.

Pero un sistema en producción es algo más que la suma de sus funciones.

Las ejecuciones pueden ocurrir simultáneamente. Los procesos pueden reutilizarse. Los componentes pueden compartir recursos. Los tenants pueden interactuar con la misma infraestructura.

Una función puede pasar todos sus tests y, aun así, el sistema puede violar una propiedad cuando varias ejecuciones interactúan.

Por eso existe una diferencia importante entre una **propiedad local** y una **propiedad arquitectónica**.

Una propiedad local puede comprobarse observando una unidad.

Una propiedad arquitectónica requiere observar cómo se comporta el sistema completo bajo las condiciones que realmente importan.

> **Algunas propiedades pertenecen al sistema completo, no a una unidad aislada.**

---

## De propiedades a invariantes

Cuando diseñamos un sistema para producción, una pregunta útil es:

> **¿Qué debe permanecer verdadero incluso cuando las cosas no salen como esperamos?**

Eso nos lleva al concepto de **invariante arquitectónica**.

Una invariante no describe necesariamente cómo funciona un componente.

Describe algo que el sistema **no debería permitir que se rompa**.

Por ejemplo:

| Ámbito | Invariante |
| --- | --- |
| Contexto | Una ejecución no debe contaminar el contexto lógico de otra |
| Identidad | Una operación debe permanecer ligada al ámbito criptográfico esperado |
| Ejecución | Un fallo debe permanecer contenido dentro del ámbito de ejecución definido |

A partir de estas propiedades aparecen tres fronteras diferentes.

---

## Tres fronteras

### 1. Contexto — aislamiento lógico

En un runtime asíncrono, múltiples ejecuciones pueden intercalarse dentro del mismo proceso.

El proceso puede ser compartido.

El contexto lógico no debería serlo.

Una forma de preservar esta propiedad es asociar el contexto a la ejecución utilizando primitivas específicas del runtime, como `ContextVar` en Python, en lugar de depender de estado global compartido.

Esto permite mantener información como el `tenant_id` asociada al contexto de una ejecución.

Pero hay una distinción importante.

`ContextVar` proporciona aislamiento lógico.

No proporciona aislamiento físico de memoria.

No crea un sandbox.

No crea una frontera de proceso.

> **Aislamiento lógico ≠ aislamiento físico.**

Cuando necesitamos contener memoria, CPU, crashes u OOM, necesitamos una frontera diferente.

<!-- AQUÍ VA EL GRÁFICO DE AISLAMIENTO DE CONTEXTO -->

### 2. Identidad — aislamiento criptográfico

La siguiente pregunta es diferente:

> **¿A qué ámbito pertenece realmente una operación?**

Un dominio criptográfico demasiado amplio puede aumentar innecesariamente el *blast radius* de un compromiso.

Una estrategia consiste en derivar material criptográfico a partir de una raíz de confianza, limitando las claves derivadas al ámbito correspondiente.

<!-- AQUÍ VA EL GRÁFICO DE DERIVACIÓN DE CLAVES -->

La clave raíz debe permanecer protegida mediante un mecanismo apropiado de gestión de secretos o claves.

Pero la autenticidad tampoco implica automáticamente protección contra *replay*.

Una firma HMAC permite verificar autenticidad e integridad respecto de la clave correspondiente.

No impide por sí sola que un mensaje legítimo sea retransmitido.

Dependiendo del protocolo, pueden ser necesarios mecanismos adicionales:

- timestamps;
- acceptance windows;
- nonces;
- registro de operaciones utilizadas.

Cada uno protege una propiedad diferente.

> **La frontera criptográfica debe definirse según las garantías que realmente necesita el protocolo.**

### 3. Ejecución — contención física

Existe una tercera situación.

¿Qué ocurre cuando el aislamiento lógico ya no es suficiente?

Un proceso compartido puede contener múltiples ejecuciones y componentes.

Si una operación consume demasiada memoria, agota CPU o provoca un fallo fatal, otros componentes que comparten ese ámbito pueden verse afectados.

Aquí aparecen problemas como **Noisy Neighbor** y propagación de fallos.

Una respuesta posible consiste en introducir una frontera de ejecución más fuerte mediante procesos independientes, contenedores, límites de recursos y mecanismos de supervisión y recuperación.

<!-- AQUÍ VA EL GRÁFICO DE SEPARACIÓN DE WORKERS -->

Pero incluso una frontera de proceso tiene límites.

Una cola puede ser compartida.

Una base de datos puede ser compartida.

Un host puede imponer una limitación común.

Una dependencia externa puede convertirse en un punto común de fallo.

> **Una frontera no elimina el riesgo. Define cómo lo contenemos.**

---

## El entorno real también forma parte de la arquitectura

Una arquitectura no está completamente validada porque funcione en una laptop.

Las garantías deben evaluarse en el entorno donde realmente se ejecuta el sistema.

En este caso, las propiedades se evaluaron sobre un despliegue real basado en **Azure Functions**.

Eso permitió observar condiciones que no necesariamente aparecen durante una prueba puramente local:

- concurrencia;
- reutilización de procesos;
- aislamiento entre invocaciones;
- gestión de material criptográfico;
- interacción con servicios externos;
- comportamiento ante errores;
- integración entre componentes.

> **El entorno real de ejecución forma parte de la validación arquitectónica.**

---

## Del diseño a la evidencia

Una invariante por sí sola no constituye evidencia.

Podemos pensar en el proceso como una cadena:

```bash
INVARIANTE
    ↓
MECANISMO
    ↓
IMPLEMENTACIÓN
    ↓
DESPLIEGUE
    ↓
VALIDACIÓN
    ↓
EVIDENCIA
```

Cada etapa responde una pregunta diferente.

- **Invariante:** ¿Qué propiedad queremos preservar?
- **Mecanismo:** ¿Qué decisión arquitectónica debería preservarla?
- **Implementación:** ¿Cómo se materializa técnicamente?
- **Despliegue:** ¿Cómo se comporta en el entorno real?
- **Validación:** ¿Qué escenarios utilizamos para ponerla a prueba?
- **Evidencia:** ¿Qué resultados observables obtuvimos?

La idea es importante porque evita confundir tres cosas distintas: **tener un diseño razonable, implementarlo correctamente y demostrar que se comporta como esperamos**.

El objetivo no es demostrar que un sistema es perfecto.

El objetivo es aumentar, de forma verificable, nuestra confianza en que las propiedades definidas se mantienen bajo las condiciones que hemos decidido evaluar.

---

## Evidencia en un sistema desplegado

En este caso, la validación no se realizó únicamente sobre funciones aisladas o mediante mocks.

**Apider** se encuentra desplegado sobre **Azure Functions**, y la suite utilizada para la validación realiza las operaciones contra ese entorno real.

Esto permite evaluar el comportamiento de diferentes componentes y escenarios dentro del mismo sistema desplegado.

Entre las propiedades y situaciones evaluadas se encuentran:

- interacción con servicios externos;
- webhooks;
- ejecución concurrente;
- manejo de errores;
- diferentes rutas de ejecución;
- comportamiento del runtime;
- integración entre componentes;
- propiedades relacionadas con el aislamiento.

### Resultado

> **61 de 61 verificaciones pasaron.**

Este resultado constituye evidencia observable sobre los escenarios evaluados.

Pero hay una distinción importante.

**61 de 61 no significa que el sistema sea perfecto.**

Tampoco significa que se hayan demostrado todas las condiciones posibles de producción.

Significa que, para los escenarios cubiertos por la suite, las propiedades evaluadas se mantuvieron bajo las condiciones en las que fueron probadas.

> **Una suite de pruebas no demuestra la ausencia de todos los fallos. Demuestra qué ocurrió bajo los escenarios que fueron evaluados.**

---

## De la evidencia a la confianza

La ingeniería basada en evidencia no elimina la incertidumbre.

La hace explícita.

Podemos pensar en el nivel de confianza como un proceso progresivo:

### Nivel 1 — Suposición

> "El diseño debería funcionar."

### Nivel 2 — Prueba local

> "La implementación funciona bajo los casos que probamos localmente."

### Nivel 3 — Integración

> "Los componentes funcionan correctamente cuando interactúan."

### Nivel 4 — Entorno real

> "Las propiedades se mantienen bajo las condiciones del entorno donde realmente se ejecuta el sistema."

### Nivel 5 — Evidencia continua

> "Seguimos verificando que esas propiedades se mantengan a medida que el sistema cambia."

La diferencia entre estos niveles no es simplemente la cantidad de tests.

Es el **alcance de las condiciones bajo las cuales estamos obteniendo evidencia**.

Una prueba local responde una pregunta.

Una prueba de integración responde otra.

Una prueba contra el sistema desplegado responde una pregunta todavía más cercana a la realidad.

La confianza aumenta cuando ampliamos las condiciones bajo las cuales una propiedad ha sido observada.

---

## Las fronteras tienen límites

Hasta aquí hemos hablado de contexto, identidad y ejecución como fronteras de aislamiento.

Pero ninguna de ellas constituye aislamiento absoluto.

`ContextVar` no es un sandbox.

Una clave derivada por tenant no elimina el riesgo asociado a la raíz de confianza.

Un proceso independiente no elimina las dependencias compartidas.

Una cola puede saturarse.

Una base de datos puede convertirse en un punto común de fallo.

La infraestructura puede introducir límites que la aplicación no controla directamente.

Por eso, una arquitectura madura no pregunta solamente:

> "¿Qué mecanismo utilizamos?"

También pregunta:

> **"¿Cuál es el límite de ese mecanismo?"**

Esta pregunta es especialmente importante porque una frontera puede ser efectiva y, al mismo tiempo, tener un alcance perfectamente definido.

No necesitamos que una frontera proteja contra todo.

Necesitamos saber **qué protege, qué no protege y qué frontera adicional necesitamos cuando su alcance deja de ser suficiente**.

---

## Preguntas incómodas

Toda frontera debería poder ser cuestionada.

No solamente durante el diseño, sino también después de haber sido implementada.

### ¿Y si `ContextVar` no es suficiente?

Entonces debemos reconocer que el aislamiento lógico tiene un alcance determinado.

Si necesitamos aislar memoria, CPU o ciclos de vida, debemos introducir una frontera de ejecución adicional.

No debemos utilizar una primitiva de contexto como sustituto de un sandbox o de un aislamiento de proceso.

### ¿Y si se compromete el secreto raíz?

La derivación por tenant reduce el dominio criptográfico de las claves derivadas.

Pero la raíz de confianza sigue siendo un punto crítico.

Si la raíz se compromete, el modelo criptográfico completo debe considerarse comprometido.

Por eso, la protección de la clave raíz mediante mecanismos apropiados de gestión de secretos o claves forma parte de la propia frontera de confianza.

### ¿Y si muere un worker?

La separación de procesos puede contener el fallo y proteger al componente coordinador.

Pero todavía debemos considerar:

- reinicio;
- backpressure;
- colas;
- límites de recursos;
- observabilidad;
- dependencias compartidas;
- recuperación.

Un worker aislado no significa que el sistema sea inmune a sus consecuencias.

### ¿Y si falla la infraestructura?

Las fronteras diseñadas dentro de una aplicación no necesariamente pueden contener fallos que ocurren fuera de ella.

Esto obliga a distinguir entre diferentes niveles de aislamiento:

- **aislamiento de aplicación**;
- **aislamiento de proceso**;
- **aislamiento de infraestructura**;
- **aislamiento de dominio de confianza**.

Cada uno resuelve problemas diferentes.

Y, en sistemas reales, varias de estas fronteras pueden coexistir.

---

## Diseñar el fallo antes de que ocurra

La pregunta central de esta charla puede resumirse en una sola frase:

> **¿Qué puede afectar un fallo cuando inevitablemente ocurra?**

No diseñamos software asumiendo que los componentes nunca fallarán.

Las excepciones ocurren.

La memoria se agota.

Los mensajes pueden retransmitirse.

Los procesos pueden terminar.

Las dependencias pueden dejar de responder.

Los recursos pueden saturarse.

Seguimos intentando:

- prevenir;
- detectar;
- corregir;
- recuperar.

Pero cuando la prevención no es suficiente, necesitamos una segunda línea de defensa:

> **Contener el impacto.**

Ahí es donde las fronteras adquieren valor arquitectónico.

Una frontera de contexto limita la contaminación lógica.

Una frontera criptográfica limita el dominio de confianza.

Una frontera de ejecución limita la propagación física de determinados fallos.

Ninguna elimina completamente el riesgo.

Pero cada una puede reducir su radio de impacto.

---

## El objetivo no es eliminar el fallo

Un sistema real no puede asumir que todos sus componentes funcionarán perfectamente durante toda su vida.

Por eso, la pregunta arquitectónica cambia.

No es solamente:

> **"¿Cómo evito que falle?"**

También es:

> **"Si falla, ¿qué puede afectar?"**

Y después:

> **"¿Cómo puedo demostrar que realmente está contenido?"**

Ese cambio de perspectiva transforma la forma en que diseñamos sistemas.

Pasamos de confiar únicamente en mecanismos aislados a definir propiedades explícitas, establecer fronteras y buscar evidencia de que esas propiedades sobreviven bajo condiciones reales.

La confiabilidad deja de ser únicamente una característica que esperamos obtener del sistema.

Se convierte en algo que podemos **diseñar, delimitar y verificar**.

---

## Materiales

Esta página también funciona como punto de referencia para los materiales de la charla.

A medida que estén disponibles, se irán incorporando aquí.

### Slides

[Ver presentación →](...)

### PDF

[Descargar PDF de la presentación →](...)

### Código y demos

[Ver código y demos →](...)

### Grabación

[Ver grabación →](...)

---

## Galería

Registro visual de la presentación en **CS Week Perú 2026**.

### Fotografías

![Jorge de la Flor durante la presentación](...)

![Jorge de la Flor en CS Week Perú 2026](...)

### Certificado

[Ver certificado de speaker →](...)

---

## Recursos

La charla se apoya en documentación, proyectos y referencias relacionadas con los conceptos presentados.

### Artículos

- [Artículo relacionado →](...)
- [Artículo relacionado →](...)

### Repositorios

- [Repositorio del proyecto →](...)
- [Repositorio de la demo →](...)

### Documentación

- [Documentación técnica →](...)
- [Documentación de referencia →](...)

### Referencias

- [Referencia utilizada durante la charla →](...)
- [Referencia utilizada durante la charla →](...)

---

## Ponente

### Jorge de la Flor

**Software & Cyber-Physical Systems Developer**

Trabajo en arquitectura de sistemas, sistemas distribuidos, software embebido y desarrollo de herramientas de bajo nivel.

Mis intereses se encuentran en la intersección entre software, sistemas y hardware, especialmente en sistemas donde las propiedades de confiabilidad, aislamiento y comportamiento en tiempo de ejecución requieren decisiones arquitectónicas explícitas.

[Sobre mí →](/md_pages/about/)

[Portfolio →](/)

---

## Sobre la presentación

| | |
|---|---|
| **Evento** | CS Week Perú 2026 |
| **Lugar** | Lima, Perú |
| **Fecha** | Agosto de 2026 |
| **Tema** | Arquitectura de sistemas · Aislamiento · Confiabilidad · Sistemas distribuidos |

---

## Cierre

> **DEFINE THE BOUNDARY.**
>
> **CHOOSE THE MECHANISM.**
>
> **VERIFY THE RESULT.**

**Jorge de la Flor**  
Software & Cyber-Physical Systems Developer

---

[← Volver a Charlas](/md_pages/talks/)
