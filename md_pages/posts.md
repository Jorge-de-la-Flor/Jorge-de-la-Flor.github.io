---
layout: default
title: Blog & Charlas — Jorge de la Flor
---

# Blog & Charlas

Este es mi espacio para compartir **ideas, investigaciones, experimentos y experiencias de ingeniería** alrededor de sistemas de software, cloud, sistemas embebidos, ingeniería de lenguajes y Cyber-Physical Systems.

También encontrarás aquí las **charlas y workshops** en los que he participado como ponente.

---

## 📝 Blog {#blog}

{% assign posts = site.posts | sort: 'date' | reverse %}

{% if posts.size == 0 %}

<p style="color: var(--text-muted);">Próximamente nuevos artículos. ¡Vuelve pronto!</p>

{% else %}

<div class="posts-grid">

  {% for post in posts %}

  <div class="post-card">

    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>

    <p style="color: var(--text-muted); font-size: 0.85rem;">

      <i class="far fa-calendar-alt"></i> {{ post.date | date: "%d/%m/%Y" }} ·

      {% for category in post.categories %}

        <span class="post-category">{{ category }}</span>

      {% endfor %}

    </p>

    <p style="color: var(--text-secondary);">
      {{ post.excerpt | strip_html | truncatewords: 30 }}
    </p>

    <a href="{{ post.url | relative_url }}" class="cta-link" style="font-size: 0.9rem;">
      Leer más →
    </a>

  </div>

  {% endfor %}

</div>

{% endif %}

---

## 🎤 Charlas {#talks}

<div class="talks-list">

  <div class="talk-item">

    <h3>Microsoft Build 2026 Community Event — Azure User Group Latam</h3>

    <p class="talk-date">
      <i class="far fa-calendar-alt"></i> IDAT Lima, Perú · Junio 2026
    </p>

    <p style="color: var(--text-secondary);">
      <strong>"Building a Multi-Tenant Python Runtime on Azure Functions"</strong>
    </p>

    <p style="color: var(--text-secondary); font-size: 0.95rem;">
      Ponencia invitada sobre arquitectura de sistemas serverless multi-tenant,
      aislamiento, confiabilidad y las decisiones de ingeniería detrás de la
      construcción de un runtime Python sobre Azure Functions.
    </p>

  </div>

  <div class="talk-item">

    <h3>CSWeek 2026</h3>

    <p class="talk-date">
      <i class="far fa-calendar-alt"></i> Lima, Perú · Agosto 2026
    </p>

    <p style="color: var(--text-secondary);">
      <strong>
        "Aislamiento y Límites de Confianza en Producción:
        Construyendo Sistemas a Prueba de Fallos"
      </strong>
    </p>

    <p style="color: var(--text-secondary); font-size: 0.95rem;">
      Charla sobre aislamiento, límites de confianza, invariantes y verificación
      de sistemas en producción, con énfasis en cómo diseñar arquitecturas que
      puedan fallar de forma segura.
    </p>

  </div>

</div>

---

## 📚 Temas

Los temas sobre los que escribo y hablo incluyen:

- **Arquitectura de sistemas:** diseño modular, sistemas distribuidos, cloud-agnosticismo y confiabilidad.
- **Cloud y backend:** serverless, multi-tenancy, APIs, infraestructura y automatización.
- **Ingeniería de lenguajes:** AST, transpiladores, inferencia de tipos, análisis estático y generación de código.
- **Rust y Python:** programación de sistemas, tooling, FFI y desarrollo de software de alto y bajo nivel.
- **Sistemas embebidos:** firmware, generación de código, abstracción de hardware y desarrollo multi-target.
- **Cyber-Physical Systems:** sensores, actuadores, edge computing, estimación y sistemas distribuidos.
- **Seguridad y confiabilidad:** aislamiento, límites de confianza, verificación y diseño para fallos seguros.
- **Infraestructura para agentes de IA:** MCP, tool-use e integración entre agentes y sistemas externos.
- **Modelado de sistemas:** análisis de capacidad, simulación, teoría de colas y optimización.

---

## 🎙️ ¿Quieres que hable en tu evento?

Si estás organizando un **meetup, conferencia, workshop, podcast técnico o actividad académica** y quieres contar conmigo como ponente o invitado, puedes escribirme directamente.

📩 **[{{ site.author.email }}](mailto:{{ site.author.email }})**

Estoy especialmente interesado en espacios donde pueda compartir experiencias prácticas sobre **arquitectura de sistemas, software de sistemas, Rust, Python, ingeniería de lenguajes, sistemas embebidos y Cyber-Physical Systems**.

---

[← Volver al inicio]({{ '/' | relative_url }})