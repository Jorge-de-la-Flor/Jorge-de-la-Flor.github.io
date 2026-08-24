---
layout: default
title: Jorge de la Flor — Software & Cyber-Physical Systems Developer
---

<div class="profile-hero">

<img src="{{ '/assets/images/avatar.jpg' | relative_url }}"
       alt="Jorge de la Flor"
       class="profile-avatar"
       onerror="this.style.display='none'">

  <h1 class="profile-name">Jorge de la Flor</h1>

  <p class="profile-title" style="font-size: 1.1rem; font-weight: 400;">
    Software & Cyber-Physical Systems Developer
  </p>

  <p class="profile-title"
     style="font-weight: 300; color: var(--text-muted); font-size: 0.95rem;">
    Systems Software · Distributed Systems · Embedded Systems · Language Engineering
  </p>

  <p style="font-size: 1.3rem; font-weight: 600; color: var(--accent-rust); margin: 0.5rem 0 0.2rem; letter-spacing: -0.02em;">
    “Designing the infrastructure that enables the next generation of software.”
  </p>

  <p style="font-size: 0.85rem; color: var(--text-muted); margin-top: 0.2rem;">
    aka FrostCore
  </p>

  <div class="tech-badges">

    <span class="tech-badge rust">
      <i class="fas fa-cog"></i> Rust
    </span>

    <span class="tech-badge python">
      <i class="fab fa-python"></i> Python
    </span>

    <span class="tech-badge cpp">
      <i class="fas fa-microchip"></i> C/C++
    </span>

    <span class="tech-badge embedded">
      <i class="fas fa-microchip"></i> Embedded
    </span>

    <span class="tech-badge ml">
      <i class="fas fa-code-branch"></i> Systems Engineering
    </span>

  </div>

  <div class="social-links">

    <a href="mailto:{{ site.author.email }}"
       class="social-link"
       title="Email">
      <i class="fas fa-envelope"></i>
    </a>

    <a href="https://linkedin.com/in/{{ site.social.linkedin }}"
       class="social-link"
       title="LinkedIn"
       target="_blank">
      <i class="fab fa-linkedin-in"></i>
    </a>

    <a href="https://github.com/{{ site.social.github }}"
       class="social-link"
       title="GitHub"
       target="_blank">
      <i class="fab fa-github"></i>
    </a>

    <a href="{{ site.social.linktree }}"
       class="social-link"
       title="Linktree"
       target="_blank">
      <i class="fas fa-link"></i>
    </a>

    {% if site.social.sessionize %}
    <a href="{{ site.social.sessionize }}"
       class="social-link"
       title="Sessionize"
       target="_blank">
      <i class="fas fa-calendar-alt"></i>
    </a>
    {% endif %}

  </div>

</div>

---

## Sobre mí

<div style="font-size: 1.05rem; line-height: 1.8; color: var(--text-secondary);">

  <p>
    <strong>Desarrollo sistemas que conectan distintas capas de la computación</strong>:
    desde infraestructura cloud, runtimes y sistemas distribuidos hasta firmware,
    microcontroladores y sistemas ciberfísicos.
  </p>

  <p>
    Trabajo principalmente con <strong>Python y Rust</strong>, combinando
    arquitectura de sistemas, ingeniería de lenguajes, generación de código,
    computación embebida y sistemas distribuidos para construir software
    <strong>robusto, eficiente y verificable</strong>.
  </p>

  <p>
    Soy creador de <strong>Apider</strong>, <strong>Pyperantio</strong>,
    <strong>OMNI-PY</strong>, <strong>Flow++</strong> y
    <strong>FrostCloud</strong>. También soy instructor técnico,
    mentor open-source y ponente en eventos de la comunidad tecnológica.
  </p>

</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/about/' | relative_url }}" class="cta-link">
    Conoce más sobre mí →
  </a>
</div>

---

## Lo que construyo

<div class="card-grid">

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-project-diagram" style="color: #4fc3f7;"></i>
      Sistemas distribuidos
    </h3>

    <p class="card-desc">
      Runtimes, servicios y arquitecturas diseñadas para operar de forma
      confiable en producción, con especial atención a aislamiento,
      escalabilidad y límites claros entre componentes.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-microchip" style="color: #DEA584;"></i>
      Sistemas embebidos y CPS
    </h3>

    <p class="card-desc">
      Firmware, generación de código y sistemas ciberfísicos que conectan
      software, hardware, sensores, comunicación y lógica de control.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-code-branch" style="color: #8b5cf6;"></i>
      Ingeniería de lenguajes
    </h3>

    <p class="card-desc">
      AST, análisis estático, inferencia de tipos, transformación de código
      y generación multi-target mediante pipelines verificables.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-layer-group" style="color: #34d399;"></i>
      Arquitectura de sistemas
    </h3>

    <p class="card-desc">
      Diseño de sistemas que mantienen responsabilidades, dependencias y
      fronteras de ejecución explícitas, evitando acoplamientos innecesarios
      con plataformas o implementaciones concretas.
    </p>

  </div>

</div>

---

## Proyectos destacados

<div class="card-grid">

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-cloud" style="color: #4fc3f7;"></i>
      Apider SDK
    </h3>

    <p class="card-desc">
      Runtime de automatización multi-tenant desplegado en Azure Functions
      y publicado en PyPI. Integra servicios externos mediante una interfaz
      Python unificada y cuenta con una suite end-to-end de
      <strong>61 checks ejecutados contra producción</strong>.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-microchip" style="color: #DEA584;"></i>
      Pyperantio
    </h3>

    <p class="card-desc">
      Motor propietario de generación de firmware que transforma una
      descripción tipada de hardware en implementaciones nativas para
      múltiples toolchains de MCU. <strong>IP en reserva.</strong>
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-code" style="color: #8b5cf6;"></i>
      OMNI-PY
    </h3>

    <p class="card-desc">
      Pipeline de ingeniería de lenguajes que utiliza Python como
      representación intermedia y Rust para análisis y verificación,
      con generación de código validada mediante toolchains reales.
    </p>

  </div>

</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/projects/' | relative_url }}" class="cta-link">
    Explorar todos los proyectos →
  </a>
</div>

---

## Publicaciones y charlas

<div class="blog-talks-preview">

  <div class="preview-block">

    <h3>
      <i class="fas fa-pen-fancy"></i>
      Blog
    </h3>

    {% assign latest_post = site.posts | sort: 'date' | reverse | first %}

    {% if latest_post %}

      <p class="preview-date">
        {{ latest_post.date | date: "%d/%m/%Y" }}
      </p>

      <h4>
        <a href="{{ latest_post.url | relative_url }}">
          {{ latest_post.title }}
        </a>
      </h4>

      <p>
        {{ latest_post.excerpt | strip_html | truncatewords: 20 }}
      </p>

      <a href="{{ '/md_pages/posts/' | relative_url }}#blog"
         class="cta-link">
        Ver todos los artículos →
      </a>

    {% else %}

      <p>
        Próximamente nuevos artículos técnicos.
      </p>

    {% endif %}

  </div>

  <div class="preview-block">

    <h3>
      <i class="fas fa-microphone-alt"></i>
      Charlas
    </h3>

    <p class="preview-date">
      Agosto 2026
    </p>

    <h4>
      CSWeek 2026 — Lima
    </h4>

    <p>
      <strong>
        “Aislamiento y Límites de Confianza en Producción:
        Construyendo Sistemas a Prueba de Fallos”
      </strong>
    </p>

    <a href="{{ '/md_pages/posts/' | relative_url }}#talks"
       class="cta-link">
      Ver todas las charlas →
    </a>

  </div>

</div>

---

## Servicios

<div class="card-grid">

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-building" style="color: #4fc3f7;"></i>
      Consultoría
    </h3>

    <p class="card-desc">
      Arquitectura de software, sistemas distribuidos, diseño de protocolos,
      sistemas embebidos y estrategias de integración hardware-software.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-code" style="color: #8b5cf6;"></i>
      Desarrollo a medida
    </h3>

    <p class="card-desc">
      Soluciones en Python, Rust y C/C++ para tooling, backend, firmware,
      generación de código y sistemas de integración.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-graduation-cap" style="color: #f59e0b;"></i>
      Formación técnica
    </h3>

    <p class="card-desc">
      Workshops, mentoría y formación en programación de sistemas,
      Rust, Python, arquitectura y desarrollo embebido.
    </p>

  </div>

  <div class="card">

    <h3 class="card-title">
      <i class="fas fa-flask" style="color: #34d399;"></i>
      Investigación
    </h3>

    <p class="card-desc">
      Investigación independiente en arquitectura de sistemas,
      ingeniería de lenguajes, generación de código y sistemas
      ciberfísicos.
    </p>

  </div>

</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/services/' | relative_url }}" class="cta-link">
    Ver servicios →
  </a>
</div>

---

## Stack

<div style="text-align: center; margin: 1.5rem 0;">

  <p style="font-weight: 500; font-size: 1.1rem; color: var(--text-secondary); margin-bottom: 1rem;">
    <strong>Python · Rust · C/C++</strong>
  </p>

  <div class="tech-badges" style="justify-content: center; gap: 0.6rem;">

    <span class="tech-badge python">
      <i class="fab fa-python"></i> Python
    </span>

    <span class="tech-badge rust">
      <i class="fas fa-cog"></i> Rust
    </span>

    <span class="tech-badge cpp">
      <i class="fas fa-microchip"></i> C/C++
    </span>

    <span class="tech-badge embedded">
      <i class="fas fa-microchip"></i> Embedded
    </span>

    <span class="tech-badge ml">
      <i class="fas fa-code-branch"></i> Systems
    </span>

    <span class="tech-badge"
          style="border-color: #4fc3f7; color: #4fc3f7;">
      <i class="fas fa-cloud"></i> Cloud
    </span>

  </div>

  <p style="font-size: 0.9rem; color: var(--text-muted); margin-top: 1rem;">
    <strong>También:</strong>
    AST · PyO3 · MCP · Azure · AWS · PostgreSQL · SQLite · Docker · CI/CD ·
    embedded-hal · UART · SPI · I²C · MQTT
  </p>

</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/stack/' | relative_url }}" class="cta-link">
    Ver stack completo →
  </a>
</div>

---

## Contacto

<p style="font-size: 1.05rem; color: var(--text-secondary);">
  ¿Tienes un proyecto, una colaboración o una conversación técnica en mente?
  Hablemos.
</p>

<div style="display: flex; gap: 1rem; flex-wrap: wrap; margin-top: 0.5rem;">

<a href="mailto:{{ site.author.email }}"
     class="cta-button"
     style="display: inline-block; padding: 0.6rem 1.5rem; background: var(--accent-rust); color: #fff; border-radius: 50px; font-weight: 600; text-decoration: none;">

    <i class="fas fa-paper-plane" style="margin-right: 0.5rem;"></i>
    Contactarme

  </a>

<a href="{{ '/md_pages/contact/' | relative_url }}"
     class="cta-link"
     style="align-self: center;">
Más formas de contacto →
</a>

</div>
