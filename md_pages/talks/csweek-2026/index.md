---
layout: default
title: "Aislamiento y Límites de Confianza en Producción — CS Week Perú 2026"
description: "Diseñando sistemas que contienen el impacto de los fallos mediante límites de confianza, invariantes y aislamiento."
---

# Aislamiento y Límites de Confianza en Producción

## Diseñando sistemas que contienen el impacto de los fallos

**CS Week Perú 2026 · Lima, Perú · Agosto de 2026**

---

## Sobre esta charla

¿Qué significa realmente que un sistema sea estable en producción?

Prevenir los fallos es la primera línea de defensa. Sin embargo, ningún sistema real puede asumir que todos sus componentes se comportarán correctamente en todo momento.

Esta charla parte de una pregunta diferente:

> **Cuando un componente falla, ¿qué puede afectar?**

A partir de esta pregunta, se presenta un enfoque de diseño basado en **límites de confianza, invariantes arquitectónicas y mecanismos de aislamiento** para reducir el *blast radius* de errores, comportamientos inesperados y fallos de ejecución.

El objetivo no es construir sistemas que nunca fallen.

> **El objetivo es controlar hasta dónde puede propagarse un fallo.**

---

## Temas principales

### 1. La estabilidad más allá de los unit tests

Los unit tests permiten verificar el comportamiento de unidades individuales bajo escenarios determinados.

Pero algunas propiedades pertenecen al sistema completo y solamente pueden evaluarse cuando observamos la interacción entre ejecuciones, componentes, contexto e infraestructura.

La charla explora la diferencia entre **propiedades locales** y **propiedades arquitectónicas**.

---

### 2. Límites de confianza

Un **Trust Boundary** define una frontera explícita donde cambia lo que el sistema está dispuesto a asumir.

Una frontera debe responder preguntas concretas:

- ¿Qué protegemos?
- ¿Qué permitimos cruzar?
- ¿Qué condiciones deben cumplirse?
- ¿Qué ocurre si esas condiciones dejan de cumplirse?

La arquitectura se analiza a partir de tres elementos:

| Elemento | Pregunta |
| --- | --- |
| **Invariante** | ¿Qué propiedad queremos preservar? |
| **Mecanismo** | ¿Qué control técnico la impone? |
| **Evidencia** | ¿Cómo verificamos que se mantiene? |

> **Diseñar una frontera no demuestra automáticamente que funciona.**

---

### 3. Diseño basado en invariantes

Una **invariante arquitectónica** define una propiedad que el sistema debe preservar bajo las condiciones establecidas por el diseño.

En esta charla se analizan tres ámbitos:

| Ámbito | Propiedad |
| --- | --- |
| **Contexto** | Una ejecución no debe contaminar el contexto lógico de otra |
| **Identidad** | Una operación debe permanecer ligada al ámbito criptográfico esperado |
| **Ejecución** | Un fallo debe permanecer contenido dentro del ámbito de ejecución definido |

Tres propiedades.

Tres fronteras.

Un mismo objetivo:

> **Limitar qué puede afectar un fallo o una ejecución fuera de lo esperado.**

---

## Las tres fronteras

### Contexto — Aislamiento lógico

En runtimes asíncronos, múltiples ejecuciones pueden intercalarse dentro del mismo proceso.

El proceso puede ser compartido.

El contexto lógico no debería serlo.

La charla analiza cómo mecanismos de contexto, como `ContextVar` en Python, pueden utilizarse para mantener información asociada a una ejecución sin recurrir a estado global compartido.

También se establece una distinción fundamental:

> **Aislamiento lógico ≠ aislamiento físico.**

`ContextVar` no constituye un sandbox, no proporciona aislamiento físico de memoria y no crea una frontera de proceso.

Cuando necesitamos contener recursos, crashes u OOM, necesitamos una frontera adicional.

---

### Identidad — Aislamiento criptográfico

Otra frontera aparece al preguntarnos:

> **¿A qué ámbito pertenece realmente una operación?**

Un dominio criptográfico demasiado amplio puede incrementar innecesariamente el *blast radius* de un compromiso.

La charla aborda estrategias para limitar el material criptográfico al ámbito correspondiente y separar dominios de confianza mediante derivación de claves.

También se analiza una distinción importante entre:

- autenticidad;
- integridad;
- protección contra *replay*.

Una firma HMAC puede demostrar autenticidad e integridad respecto de una clave, pero no impide por sí sola que un mensaje legítimo sea retransmitido.

Por ello, dependiendo del protocolo, pueden ser necesarios mecanismos adicionales como:

- timestamps;
- acceptance windows;
- nonces;
- registro de operaciones utilizadas.

> **La frontera criptográfica debe definirse según las garantías que realmente necesita el protocolo.**

---

### Ejecución — Contención física

Cuando el aislamiento lógico ya no es suficiente, necesitamos una frontera de ejecución más fuerte.

Un proceso compartido puede contener múltiples ejecuciones y componentes. Un consumo excesivo de memoria, CPU o un fallo fatal puede afectar a otros componentes que compartan ese ámbito.

Esto introduce problemas como:

#### Noisy Neighbor

Un tenant o tarea puede consumir una cantidad desproporcionada de recursos y degradar la disponibilidad de otros tenants.

#### Propagación de fallos

Un fallo grave dentro de un componente puede afectar a otros componentes que comparten su proceso o ciclo de vida.

La separación de procesos, contenedores, límites de recursos, supervisión y recuperación permite introducir fronteras más fuertes.

Pero ninguna frontera es absoluta.

Una cola compartida puede saturarse.

Una base de datos compartida puede convertirse en un punto común de fallo.

Un host puede imponer una limitación compartida.

> **Una frontera no elimina el riesgo. Define cómo lo contenemos.**

---

## Validación en entornos reales

Una arquitectura no está completamente validada porque funcione correctamente en un entorno local.

Las propiedades deben evaluarse en el entorno donde realmente se ejecuta el sistema.

En esta charla se presenta la validación de estas propiedades sobre un despliegue real basado en **Azure Functions**, considerando factores como:

- concurrencia;
- reutilización de procesos;
- aislamiento entre invocaciones;
- gestión de material criptográfico;
- interacción con servicios externos;
- comportamiento ante errores;
- ejecución de componentes secundarios.

> **El entorno real de ejecución forma parte de la validación arquitectónica.**

---

## De la arquitectura a la evidencia

Una invariante teórica no constituye evidencia suficiente.

El proceso puede resumirse como:

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

Cada etapa responde una pregunta diferente:

- **Invariante:** ¿Qué propiedad queremos preservar?
- **Mecanismo:** ¿Qué decisión arquitectónica debería preservarla?
- **Implementación:** ¿Cómo se materializa técnicamente?
- **Despliegue:** ¿Cómo se comporta en el entorno real?
- **Validación:** ¿Qué escenarios utilizamos para ponerla a prueba?
- **Evidencia:** ¿Qué resultados observables obtuvimos?

El objetivo no es demostrar que un sistema es perfecto.

El objetivo es aumentar de forma verificable la confianza en que las propiedades definidas se mantienen bajo las condiciones evaluadas.

---

## Evidencia

Como parte de la validación, se ejecutó una suite de integración contra un despliegue real de **Apider sobre Azure Functions**.

Las verificaciones atraviesan diferentes componentes y escenarios del sistema, incluyendo propiedades relacionadas con:

- servicios externos;
- webhooks;
- ejecución concurrente;
- manejo de errores;
- diferentes rutas de ejecución;
- comportamiento del runtime;
- integración entre componentes;
- aislamiento.

### Resultado

> **61 de 61 verificaciones pasaron.**

Este resultado constituye evidencia observable sobre los escenarios evaluados.

No significa que el sistema sea perfecto ni que se hayan demostrado todas las condiciones posibles de producción.

Significa que las propiedades cubiertas por la suite se mantuvieron bajo las condiciones que fueron probadas.

> **Una suite de pruebas no demuestra la ausencia de todos los fallos. Demuestra qué ocurrió bajo los escenarios que fueron evaluados.**

---

## De la evidencia a la confianza

La ingeniería basada en evidencia no elimina la incertidumbre.

La hace explícita.

Podemos pensar en diferentes niveles de confianza:

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

---

## Las fronteras tienen límites

Ninguno de los mecanismos analizados constituye aislamiento absoluto.

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

---

## Preguntas incómodas

Toda frontera debería poder ser cuestionada.

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

Pero todavía deben considerarse:

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

Esto obliga a distinguir entre:

- aislamiento de aplicación;
- aislamiento de proceso;
- aislamiento de infraestructura;
- aislamiento de dominio de confianza.

Cada uno resuelve problemas diferentes.

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

La pregunta arquitectónica cambia.

No es solamente:

> **"¿Cómo evito que falle?"**

También es:

> **"Si falla, ¿qué puede afectar?"**

Y después:

> **"¿Cómo puedo demostrar que realmente está contenido?"**

Ese cambio de perspectiva transforma la forma en que diseñamos sistemas.

Pasamos de confiar únicamente en mecanismos aislados a definir propiedades explícitas, establecer fronteras y buscar evidencia de que esas propiedades sobreviven bajo condiciones reales.

---

## Materiales

Los materiales de la presentación estarán disponibles aquí.

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

Aquí se recopilan fotografías y material visual de la presentación en CS Week Perú 2026.

### Fotografías

![Jorge de la Flor durante la presentación](...)

![Jorge de la Flor en CS Week Perú 2026](...)

### Certificado

[Ver certificado de speaker →](...)

---

## Recursos

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

**Evento:** CS Week Perú 2026  
**Lugar:** Lima, Perú  
**Fecha:** Agosto de 2026  
**Tema:** Arquitectura de sistemas · Aislamiento · Confiabilidad · Sistemas distribuidos

---

## Cierre

> **DEFINE THE BOUNDARY.**
>
> **CHOOSE THE MECHANISM.**
>
> **VERIFY THE RESULT.**

---

[← Volver a Charlas](/md_pages/talks/)
