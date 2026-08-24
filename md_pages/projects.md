---
layout: default
title: Proyectos — Jorge de la Flor
---

# Proyectos

Una selección de proyectos en **arquitectura de sistemas, ingeniería de lenguajes, generación de código, sistemas embebidos y Cyber-Physical Systems**.

Estos proyectos exploran una misma pregunta de fondo: **cómo diseñar sistemas que puedan evolucionar, verificarse y mantenerse confiables a medida que cambian sus lenguajes, plataformas, infraestructura y condiciones de ejecución.**

---

## Proyectos destacados

### Apider SDK — Runtime Python para infraestructura cloud

`Python` · `Azure Functions` · `PyPI` · `MCP` · `Paddle`

Runtime de automatización **multi-tenant serverless** diseñado para proporcionar una interfaz Python consistente sobre múltiples servicios e integraciones.

Integra Email, Telegram, WhatsApp, Discord, Slack, Google Sheets, HTTP, Webhooks y CloudScheduler mediante un SDK Python, además de infraestructura para escenarios de agentes de IA mediante MCP.

La arquitectura separa la interfaz cliente de la lógica de integración y los componentes sensibles del sistema, manteniendo el runtime y los secretos del lado servidor.

Incluye aislamiento por contexto, protección de credenciales, mecanismos de facturación y una suite de **61 checks end-to-end ejecutados contra producción**.

[Ver en PyPI →](https://pypi.org/project/apider/)

---

### Pyperantio — Generación de firmware embebido

`Python` · `Rust` · `embedded-hal` · `MCUs`

Tooling propietario para generación de código de firmware embebido.

Una API tipada en Python permite describir el hardware mediante modelos de configuración y generar firmware nativo para múltiples familias y toolchains de microcontroladores.

El proyecto busca reducir la dependencia entre la lógica de alto nivel y las implementaciones específicas de cada plataforma, permitiendo reutilizar modelos y generar implementaciones adaptadas al hardware de destino.

El sistema incorpora validación de configuraciones antes de la generación de código, permitiendo detectar incompatibilidades de hardware durante el proceso de diseño.

🔒 *Detalles internos de arquitectura y generación reservados por estrategia de propiedad intelectual.*

---

### OMNI-PY — Ingeniería de lenguajes y generación de código

`Python` · `Rust` · `PyO3` · `AST` · `Java` · `Go` · `JavaScript` · `Rust`

Proyecto de ingeniería de lenguajes orientado a la **transformación bidireccional entre múltiples lenguajes de programación**.

Python funciona como representación intermedia del pipeline, mientras componentes implementados en Rust realizan análisis y verificaciones adicionales.

El sistema cubre las combinaciones entre **Java, Go, JavaScript y Rust**, utilizando un pipeline común para transformar, analizar y generar código.

Los resultados se validan mediante **compilación y ejecución contra toolchains reales**, en lugar de depender únicamente de comparaciones textuales o aserciones sobre el código generado.

---

### Flow++ — Modelado y optimización de sistemas

`Python` · `stdlib` · `MIT`

Toolkit para **modelar, analizar y optimizar pipelines** mediante una representación estructurada de sus etapas, capacidades y latencias.

El análisis permite identificar cuellos de botella, estimar throughput, crecimiento de colas y estabilidad, y evaluar cambios orientados a alcanzar una capacidad objetivo.

Combina análisis estático, simulación en tiempo discreto, teoría de colas y modelos analíticos para comparar escenarios antes y después de una modificación.

El sistema explicita las asunciones de cada modelo para que las decisiones derivadas puedan ser interpretadas y verificadas.

---

### FrostCloud — Control Plane en Rust

`Rust` · `axum` · `SeaORM` · `PostgreSQL` · `SQLite`

Plano de control para el ecosistema FrostCore, desarrollado íntegramente en Rust.

Proporciona capacidades de **cuentas, identidad, catálogo de servicios y activaciones por cuenta**, manteniendo el control plane separado del camino de datos de los servicios.

La arquitectura utiliza fronteras explícitas entre crates para aislar responsabilidades como identidad, transporte y persistencia.

El proyecto explora cómo construir infraestructura de control pequeña, modular y verificable sin introducir dependencias innecesarias entre sus componentes.

---

### Plataforma Distribuida de Sensado — Sistema Cyber-Physical

`ESP32` · `Raspberry Pi` · `Kalman Filter` · `MQTT` · `SQLite` · `SSE`

Sistema ciberfísico distribuido que integra sensores, procesamiento embebido, comunicación edge y visualización en tiempo real.

El sistema combina:

- Filtrado de Kalman en tiempo discreto sobre el microcontrolador.
- Pipeline multi-sensor controlada mediante una máquina de estados.
- Sensores PIR y ultrasónico.
- Comunicación `UART → MQTT → edge`.
- Persistencia mediante SQLite.
- API REST.
- Dashboard de monitoreo en tiempo real mediante Server-Sent Events.

El proyecto explora la integración de procesamiento local, comunicación distribuida y estimación de estado en presencia de incertidumbre de sensores.

---

## Exploración técnica

### Embedded System Architectures

Investigación y experimentación con arquitecturas de firmware modulares y modelos de control basados en estados para plataformas embebidas.

Trabajo principalmente con **ESP32, STM32 y RP2040**, explorando separación de responsabilidades, abstracciones de hardware y diseño de firmware orientado a múltiples plataformas.

---

### Sensor Uncertainty & Probabilistic Estimation

Experimentos con modelado de incertidumbre y estimación de estado a partir de sensores ruidosos.

Incluye exploraciones con **filtros de Kalman**, modelos discretos y procesamiento de señales para sistemas donde las mediciones físicas contienen ruido e incertidumbre.

---

### Distributed Edge Systems

Investigación sobre sistemas distribuidos en el edge capaces de coordinar nodos de hardware heterogéneos.

Explora comunicación mediante protocolos ligeros, separación entre procesamiento local y coordinación central, y mecanismos orientados a mantener la operación del sistema ante fallos parciales.

---

### Systems & Language Engineering

Exploración de técnicas para transformar representaciones de alto nivel en implementaciones específicas de plataforma.

Incluye experimentación con AST, análisis estático, inferencia de tipos, generación de código, compilación cruzada y validación mediante toolchains reales.

---

## Una misma línea de investigación

Aunque los proyectos abarcan dominios diferentes, comparten una preocupación arquitectónica común:

> **¿Cómo diseñar sistemas que no dependan innecesariamente de una implementación concreta y que puedan ser transformados, verificados y adaptados a diferentes entornos?**

Esta idea constituye parte del fundamento del **Modelo Agnóstico (AMP)** y del principio de **Agnosticismo por Transformación** desarrollado en *The Agnostic Engineer: Architecture Beyond Infrastructure*.

---

## Código y proyectos abiertos

Una parte del trabajo experimental y open-source está disponible en mi [GitHub]({{ site.social.github }}).

---

[← Volver al inicio]({{ '/' | relative_url }})
