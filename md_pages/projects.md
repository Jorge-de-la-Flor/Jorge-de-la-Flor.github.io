---
layout: default
title: Proyectos — Jorge de la Flor
---

# Proyectos

Selección de proyectos en arquitectura de software, diseño de protocolos, sistemas embebidos y CPS.

---

## Proyectos destacados

### Apider SDK — Runtime Python nativo en la nube
`pip install apider` · PyPI · Azure Functions

Runtime multi-tenant serverless que expone Email, Telegram, Discord, Slack, Google Sheets, HTTP, Webhooks y CloudScheduler a través de un SDK Python limpio. Innovaciones clave: aislamiento multi-tenant con ContextVar, cifrado Fernet de credenciales en tránsito, arquitectura cliente-ligero/servidor-rápido (protección IP), servidor MCP stateless para orquestación de agentes IA y facturación Paddle con control de excesos. Suite de 61 pruebas de integración.

[Ver en PyPI →](https://pypi.org/project/apider)

---

### Pyperantio — Tooling propietario para firmware embebido
Python · Rust · Sistemas embebidos

Tooling interno para generación de código firmware en 4+ familias de MCUs, basado en emisión automática de código a partir de modelos de configuración hardware-independientes. Reduce drásticamente las reescrituras de HAL al portar firmware entre plataformas.

🔒 *IP filing en progreso*

---

### OMNI-PY — Transpilador de Python a múltiples lenguajes
Python (AST) · Rust (FFI PyO3) · Emite: Java · Go · JavaScript

La capa AST de Python ingiere código fuente como nodos semánticos, no como texto. Un TypeTracker en Rust realiza inferencia de tipos y análisis de nulabilidad exhaustivos mediante un puente FFI PyO3. Los emisores generan código idiomático en Java, Go y JavaScript con inyección automática de imports, wrappers y declaraciones de paquete, incorporando validaciones de tipos, manejo explícito de opcionales y protecciones de seguridad aritmética en tiempo de generación.

---

### Plataforma Distribuida de Sensores — Sistema Edge Embebido
ESP32 · Raspberry Pi · Filtro Kalman · MQTT · SQLite · SSE

Sistema ciber-físico completo: filtro Kalman en tiempo discreto en MCU para estimación de estado con ruido, pipeline de sensores controlado por FSM (PIR + ultrasónico), distribución UART → MQTT → edge node, persistencia SQLite, API REST y dashboard de monitoreo en tiempo real con SSE.

---

## Exploración técnica

### Embedded System Architectures
Implementación de modelos de control basados en estados y estructuras de firmware modulares para plataformas de sensores basadas en microcontroladores (ESP32, STM32).

### Sensor Uncertainty & Probabilistic Estimation
Experimentos explorando el modelado de ruido de sensores y estimación de estado, incluyendo enfoques de filtrado Kalman para entornos ruidosos.

### Distributed Edge Systems
Diseño de servicios de coordinación basados en Linux que permiten la comunicación entre nodos de hardware heterogéneos mediante protocolos de mensajería ligera y orquestación tolerante a fallos.

---

Más proyectos y código en mi [GitHub](https://github.com/{{ site.social.github }}).

---

[← Volver al inicio]({{ '/' | relative_url }})
