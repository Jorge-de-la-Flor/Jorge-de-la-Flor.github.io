---
layout: default
title: Sobre mí — FrostCore | Jorge de la Flor
---

# Sobre mí

## Perfil profesional

Arquitecto de software y desarrollador de sistemas especializado en infraestructura cloud, sistemas embebidos y tooling de lenguajes. Creador de **Apider**, **Pyperantio** y **OMNI-PY** — tres plataformas que resuelven problemas de portabilidad, automatización y generación de código.

Los principios arquitectónicos que subyacen a estos proyectos están formalizados como el **Modelo Agnóstico (AMP)** en mi libro en preparación: *The Agnostic Engineer: Architecture Beyond Infrastructure*.

Combino una formación en **International Business** con experiencia práctica en ingeniería de software. He sido ponente invitado en **Microsoft Build 2026** y en **Azure User Group Latam**.

---

## Experiencia profesional

### Independiente — Arquitecto & Desarrollador de Sistemas
*ago 2024 – Presente*

- **Apider**: Runtime multi-tenant serverless en Azure Functions, publicado en PyPI. Implementa aislamiento por ContextVar, cifrado Fernet para credenciales, servidor MCP stateless para integración con agentes IA, y facturación Paddle. 61 pruebas de integración — todas pasando en CI.

- **Pyperantio**: Tooling propietario para generación de código firmware embebido. Soporte para 4+ familias de MCUs con emisión automática de código a partir de modelos de configuración hardware-independientes. (Detalles técnicos en reserva — IP filing en progreso.)

- **OMNI-PY**: Transpilador de Python a múltiples lenguajes (Java, Go, JavaScript). Capa AST en Python y TypeTracker en Rust (vía FFI PyO3) para inferencia de tipos y análisis de nulabilidad. Emite código idiomático y compilable.

- **The Agnostic Engineer**: Libro técnico en preparación que formaliza el principio de "Agnosticismo por Transformación" como principio arquitectónico unificado.

- **Ponencia invitada**: *"Building a Multi-Tenant Python Runtime on Azure Functions"* — Microsoft Build 2026 Community Event · Azure User Group Latam · IDAT Lima, junio 2026.

### UNEX DIESEL SAC — Especialista en Logística de Importación y Soporte Técnico
*ago 2023 – jul 2024*

Coordiné operaciones de importación end-to-end, diseñé iniciativas de automatización de procesos y realicé análisis de costos y cumplimiento normativo.

---

## Proyectos seleccionados

### Apider SDK — Runtime Python nativo en la nube
`pip install apider` · PyPI · Azure Functions

Runtime multi-tenant serverless que expone Email, Telegram, Discord, Slack, Google Sheets, HTTP, Webhooks y CloudScheduler a través de un SDK Python limpio. Innovaciones clave: aislamiento multi-tenant con ContextVar, cifrado Fernet de credenciales en tránsito, arquitectura cliente-ligero/servidor-rápido (protección IP), servidor MCP stateless para orquestación de agentes IA y facturación Paddle con control de excesos. Suite de 61 pruebas de integración.

### Pyperantio — Tooling propietario para firmware embebido
Python · Rust · Sistemas embebidos

Tooling interno para generación de código firmware en 4+ familias de MCUs, basado en emisión automática de código a partir de modelos de configuración hardware-independientes. Reduce drásticamente las reescrituras de HAL al portar firmware entre plataformas. Detalles técnicos en reserva — IP filing en progreso.

### OMNI-PY — Transpilador de Python a múltiples lenguajes
Python (AST) · Rust (FFI PyO3) · Emite: Java · Go · JavaScript

La capa AST de Python ingiere código fuente como nodos semánticos, no como texto. Un TypeTracker en Rust realiza inferencia de tipos y análisis de nulabilidad exhaustivos mediante un puente FFI PyO3. Los emisores generan código idiomático en Java, Go y JavaScript con inyección automática de imports, wrappers y declaraciones de paquete, incorporando validaciones de tipos, manejo explícito de opcionales y protecciones de seguridad aritmética en tiempo de generación.

---

## Publicaciones y ponencias

- **Libro en preparación:** *The Agnostic Engineer: Architecture Beyond Infrastructure* — Jorge A. de la Flor. Formaliza el *Agnosticismo por Transformación* como principio arquitectónico unificado; Apider, Pyperantio y OMNI-PY como casos de estudio.
- **Ponencia (jun 2026):** *"Building a Multi-Tenant Python Runtime on Azure Functions"* — Microsoft Build 2026 Community Event · Azure User Group Latam · IDAT Lima.

---

## Habilidades técnicas

- **Arquitectura de software:** Diseño cloud-agnóstico (Agnosticismo por Transformación), multi-tenant serverless, diseño de APIs REST, CI/CD, Azure Functions.
- **Ingeniería de lenguajes:** AST de Python, transformación de AST, diseño de transpiladores, inferencia de tipos, PyO3 (FFI Rust - Python).
- **Sistemas embebidos:** ESP32, STM32, Arduino, RP2040 · UART, I2C, SPI, MQTT · embedded-hal, Rust bare-metal.
- **Seguridad:** Cifrado Fernet, aislamiento por ContextVar, modelos de credenciales en tránsito.
- **Ingeniería de datos:** Polars, Pandas, NumPy · PostgreSQL, SQLite, SQLAlchemy.
- **SDK y producto:** Arquitectura SDK multi-tenant, empaquetado PyPI, facturación Paddle, patrón cliente-ligero/servidor-rápido.
- **Lenguajes de programación:** Python · Rust (sistemas y embedded) · C/C++ (embedded) · SQL · Bash.
- **Idiomas:** Español (nativo) · Inglés (avanzado) · Chino (intermedio).

---

## Educación

**Bachelor of Arts in International Business — Doble Titulación**
Universidad San Ignacio de Loyola (Perú) & San Ignacio University (USA) · 2019–2024

- Consistentemente en el tercio superior de la cohorte.
- 1er lugar — USIL-SIU International University Fairs (2020).

---

## Certificaciones

- **Claude Architect** — en progreso — DevCompass.
- **HSK 2 — Chino Intermedio** — Instituto Confucio — PUCP.

---

## Intereses de investigación

Arquitectura de software · Ingeniería de lenguajes · Sistemas distribuidos · Sistemas embebidos · Infraestructura para agentes IA

---

[← Volver al inicio]({{ '/' | relative_url }})
