---
layout: default
title: Sobre mí — FrostCore | Jorge de la Flor
---

# Sobre mí

## Perfil profesional

**Software & Cyber-Physical Systems Developer** especializado en arquitectura de software de sistemas y cloud, sistemas distribuidos, computación embebida e ingeniería de lenguajes.

Diseño sistemas que conectan distintas capas de la computación: desde infraestructura cloud, runtimes y servicios distribuidos hasta firmware, microcontroladores y sistemas ciberfísicos. Mi trabajo se centra en construir sistemas **robustos, eficientes, verificables y capaces de operar de forma confiable en producción**.

Trabajo principalmente con **Python y Rust**, complementados con C/C++, herramientas de sistemas y tecnologías de infraestructura cloud.

Soy creador de **Apider**, **Pyperantio**, **OMNI-PY**, **Flow++** y **FrostCloud**, proyectos que exploran problemas de automatización, portabilidad, generación de código, modelado de sistemas e infraestructura.

Los principios arquitectónicos que conectan parte de este trabajo están formalizados en el **Modelo Agnóstico (AMP)**, desarrollado en mi manuscrito técnico *The Agnostic Engineer: Architecture Beyond Infrastructure*.

Combino una formación en **International Business** con experiencia práctica en ingeniería de software, sistemas y desarrollo de productos. Soy instructor técnico, mentor open-source y ponente en eventos de la comunidad tecnológica, incluyendo **Microsoft Build 2026**, **Azure User Group Latam** y **CSWeek 2026**.

---

## Quién soy

Soy **Jorge de la Flor**, ingeniero de software de sistemas y cloud, especializado en construir software que cruza fronteras entre abstracción e implementación.

Me interesa especialmente el punto donde diferentes capas de un sistema necesitan trabajar juntas de manera predecible: servicios distribuidos que deben mantener aislamiento y confiabilidad, herramientas que transforman código entre lenguajes y plataformas, y sistemas embebidos donde hardware, memoria, tiempo y comunicación forman parte del problema de ingeniería.

No me interesa estar limitado a una capa específica de la tecnología. Me interesa entender **el sistema completo**: cómo se modela, cómo se transforma, cómo se ejecuta, cómo falla y cómo puede verificarse.

Por encima de un lenguaje o framework concreto, busco construir sistemas con **límites claros, comportamiento verificable y capacidad de evolucionar sin quedar atados innecesariamente a una implementación, plataforma o proveedor**.

---

## Qué hago

Actualmente trabajo de forma independiente como **Arquitecto de Software de Sistemas y Cloud**, desarrollando proyectos de software, tooling y sistemas embebidos en la convergencia de:

- **Arquitectura de sistemas:** sistemas modulares, distribuidos, escalables y cloud-agnósticos.
- **Sistemas distribuidos y cloud:** runtimes serverless, APIs, aislamiento multi-tenant, infraestructura de ejecución y CI/CD.
- **Ingeniería de lenguajes:** AST, transformación de código, lexing, parsing, transpiladores, análisis estático e inferencia de tipos.
- **Generación de código:** transformación de representaciones de alto nivel en implementaciones específicas y verificables.
- **Sistemas embebidos:** firmware y tooling para microcontroladores como ESP32, STM32 y RP2040.
- **Sistemas ciberfísicos:** integración de software, hardware, sensores, actuadores, comunicación y lógica de control.
- **Protocolos y comunicación:** integración de sistemas mediante APIs, protocolos de red, interfaces seriales y buses de comunicación.
- **Sistemas de agentes de IA:** infraestructura MCP, tool-use agéntico y mecanismos de integración entre agentes y sistemas externos.
- **Modelado de sistemas:** análisis de capacidad, teoría de colas, simulación y modelado de pipelines.

---

## Experiencia profesional

### Independiente — Ingeniero de Software de Sistemas y Cloud
*ago 2024 – Presente*

Desarrollo proyectos propios de software, infraestructura, tooling y sistemas embebidos, combinando arquitectura de sistemas, ingeniería de lenguajes, cloud y computación de bajo nivel.

- **Apider:** Runtime de automatización multi-tenant desplegado en Azure Functions y publicado en PyPI. Proporciona una interfaz Python unificada para integrar servicios y automatizaciones, incorporando aislamiento por contexto, protección de credenciales, integración con agentes de IA mediante MCP y mecanismos de facturación. El sistema cuenta con una suite end-to-end de **61 checks ejecutados contra producción**.

- **Pyperantio:** Motor propietario de generación de código para firmware embebido. Una API tipada en Python permite describir configuraciones de hardware y generar firmware para múltiples toolchains de microcontroladores. La validación se realiza sobre las restricciones del hardware antes de generar código. Los detalles internos de arquitectura y generación permanecen reservados como parte de la estrategia de propiedad intelectual.

- **OMNI-PY:** Sistema de ingeniería de lenguajes orientado a la transformación bidireccional entre múltiples lenguajes. Utiliza Python como representación intermedia y Rust para componentes de análisis y verificación, con generación de código validada contra toolchains reales.

- **Flow++:** Toolkit de modelado, análisis y optimización de pipelines. Permite identificar cuellos de botella, estimar throughput y crecimiento de colas, evaluar estabilidad y recomendar cambios orientados a alcanzar una capacidad objetivo, respaldado por simulación y análisis cuantitativo.

- **FrostCloud:** Plano de control desarrollado íntegramente en Rust para cuentas, identidad, catálogo de servicios y activaciones. La arquitectura separa explícitamente el plano de control del camino de datos y utiliza fronteras por crate para mantener aisladas las responsabilidades del sistema.

- **Plataforma de Sensado Distribuido:** Sistema ciberfísico basado en ESP32 y Raspberry Pi que integra sensores, filtrado de Kalman, máquinas de estados, UART, MQTT, persistencia y visualización en tiempo real.

- **The Agnostic Engineer:** Manuscrito técnico en preparación que formaliza el concepto de **Agnosticismo por Transformación** como principio arquitectónico para diseñar sistemas capaces de sobrevivir a cambios de infraestructura, lenguaje y proveedor.

### Instructor Técnico y Mentor Open-Source — Latinoamérica
*ene 2024 – Presente*

Mentoría e instrucción técnica para desarrolladores y estudiantes de distintos países de Latinoamérica, con énfasis en Python, Rust y programación de sistemas.

He enseñado conceptos de gestión de memoria, desarrollo bare-metal, concurrencia, paralelismo y diseño con seguridad de tipos, conectando conceptos de alto nivel con su implementación a bajo nivel.

### UNEX DIESEL SAC — Especialista en Logística de Importación y Soporte Técnico
*ago 2023 – jul 2024*

Coordiné operaciones de importación end-to-end con proveedores internacionales y entidades regulatorias, además de desarrollar iniciativas de automatización orientadas a reducir tiempos de documentación y carga operativa.

---

## Proyectos seleccionados

### Apider SDK — Runtime Python para infraestructura cloud

`Python` · `Azure Functions` · `PyPI` · `MCP` · `Paddle`

Runtime serverless multi-tenant diseñado para proporcionar una interfaz Python consistente sobre múltiples servicios e integraciones, incluyendo Email, Telegram, WhatsApp, Discord, Slack, Google Sheets, HTTP, Webhooks y CloudScheduler.

El proyecto aborda problemas de aislamiento, automatización e integración de servicios mediante una arquitectura que mantiene la lógica de integración y los componentes sensibles fuera del cliente. También incorpora infraestructura para escenarios de agentes de IA mediante MCP y mecanismos de facturación basados en consumo.

El despliegue cuenta con una suite de **61 checks end-to-end ejecutados contra producción**.

---

### Pyperantio — Generación de firmware embebido

`Python` · `Rust` · `embedded-hal` · `MCUs`

Tooling propietario orientado a reducir la dependencia entre los modelos de configuración de hardware y las implementaciones concretas de firmware.

Una API tipada en Python permite describir el hardware una vez y generar firmware nativo para múltiples toolchains y familias de microcontroladores.

El sistema incorpora validación de configuraciones antes de la generación de código, permitiendo detectar incompatibilidades de hardware durante el proceso de diseño en lugar de descubrirlas después de generar o ejecutar el firmware.

La arquitectura interna y los mecanismos específicos de generación se mantienen reservados debido a su estrategia de propiedad intelectual.

---

### OMNI-PY — Ingeniería de lenguajes y generación de código

`Python` · `Rust` · `PyO3` · `AST` · `Java` · `Go` · `JavaScript` · `Rust`

Proyecto de ingeniería de lenguajes orientado a la transformación bidireccional entre múltiples lenguajes.

Python funciona como representación intermedia del pipeline, mientras que componentes implementados en Rust realizan análisis y verificaciones adicionales. Los generadores producen código para diferentes lenguajes de destino y validan sus resultados mediante compilación y ejecución contra toolchains reales.

El objetivo no es simplemente traducir sintaxis, sino preservar las propiedades semánticas necesarias para que el código generado sea correcto y ejecutable en su plataforma de destino.

---

### Flow++ — Modelado y optimización de sistemas

`Python` · `stdlib` · `MIT`

Toolkit para modelar pipelines como sistemas de etapas con capacidad y latencia.

El análisis permite identificar cuellos de botella, estimar throughput, crecimiento de colas y estabilidad, y evaluar cambios mediante simulación y modelos analíticos. El sistema explicita las asunciones utilizadas por cada modelo para que las decisiones derivadas puedan ser interpretadas y verificadas.

---

### FrostCloud — Control plane en Rust

`Rust` · `axum` · `SeaORM` · `PostgreSQL` · `SQLite`

Workspace desarrollado íntegramente en Rust para proporcionar cuentas, identidad, catálogo de servicios y activaciones por cuenta.

El proyecto explora una separación estricta entre **control plane y data plane**, utilizando fronteras arquitectónicas a nivel de crate para mantener aisladas las responsabilidades de identidad, transporte y persistencia.

---

### Plataforma de Sensado Distribuido — Sistema ciberfísico

`ESP32` · `Raspberry Pi` · `Kalman Filter` · `MQTT` · `SQLite` · `SSE`

Sistema ciberfísico distribuido que integra múltiples nodos de sensado y procesamiento.

El sistema combina filtrado de Kalman en tiempo discreto sobre el microcontrolador, una pipeline multi-sensor controlada mediante FSM, comunicación UART → MQTT → edge, persistencia SQLite, API REST y visualización en tiempo real mediante Server-Sent Events.

---

## Publicaciones y ponencias

- **Libro en preparación:** *The Agnostic Engineer: Architecture Beyond Infrastructure* — Jorge A. de la Flor. Manuscrito técnico sobre el **Agnosticismo por Transformación** y el diseño de sistemas capaces de sobrevivir a cambios de infraestructura, lenguaje y proveedor.

- **Ponencia — junio 2026:** *"Building a Multi-Tenant Python Runtime on Azure Functions"* — Microsoft Build 2026 Community Event · Azure User Group Latam · IDAT Lima.

- **Ponencia — agosto 2026:** *"Aislamiento y Límites de Confianza en Producción: Construyendo Sistemas a Prueba de Fallos"* — CSWeek 2026 · Lima.

---

## Habilidades técnicas

- **Arquitectura de sistemas:** sistemas distribuidos, diseño cloud-agnóstico, sistemas multi-tenant, separación de responsabilidades, APIs y CI/CD.
- **Cloud y backend:** Azure Functions, serverless, Azure Table Storage · AWS EC2, Lambda, S3 e IAM · REST APIs · axum · SeaORM · PostgreSQL · SQLite · SQLAlchemy.
- **Ingeniería de lenguajes:** Python `ast`, transformación de AST, lexing, parsing, transpiladores bidireccionales, inferencia de tipos, análisis estático y PyO3.
- **Generación de código:** pipelines de transformación, generación multi-target, validación mediante compilación y ejecución contra toolchains reales.
- **Sistemas embebidos:** ESP32, STM32, Arduino, RP2040 · UART, I2C, SPI, MQTT · embedded-hal · Rust bare-metal · generación de firmware multi-backend.
- **Sistemas ciberfísicos:** sensores, actuadores, máquinas de estados, filtrado de Kalman, comunicación edge y sistemas distribuidos.
- **Sistemas de agentes IA:** MCP, tool-use agéntico, JSON-RPC 2.0, integración de agentes y extracción estructurada.
- **Seguridad y confiabilidad:** derivación de claves por tenant, HMAC-SHA256, cifrado Fernet, aislamiento ContextVar, sandboxing de procesos, protección anti-SSRF, hashing de tokens y verificación de invariantes.
- **Modelado de sistemas:** teoría de colas, simulación en tiempo discreto, modelado mediante DAG, ley de Little y análisis de capacidad.
- **Lenguajes:** Python · Rust · C/C++ · Java · Go · SQL · Bash.
- **Idiomas:** Español (nativo) · Inglés (avanzado) · Chino (básico, HSK 2).

---

## Educación

**Bachelor of Arts in International Business — Doble Titulación**

Universidad San Ignacio de Loyola (Perú) & San Ignacio University (USA) · 2019–2024

- Consistentemente en el tercio superior de la cohorte.
- 1er lugar — USIL-SIU International University Fairs (2020).

---

## Certificaciones

- **Claude Architect** — DevCompass.
- **HSK 2 — Chino** — Instituto Confucio — PUCP.

---

## Intereses de investigación

**Arquitectura de sistemas** · **Sistemas distribuidos** · **Ingeniería de lenguajes** · **Generación de código** · **Sistemas embebidos** · **Cyber-Physical Systems** · **Protocolos y comunicación** · **Verificación y confiabilidad de sistemas** · **Infraestructura para agentes de IA**

---

[← Volver al inicio]({{ '/' | relative_url }})
