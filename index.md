---
layout: default
title: Jorge de la Flor — Software Architect & Protocol Developer
---

<div class="profile-hero">
  <img src="{{ '/assets/images/avatar.jpg' | relative_url }}" alt="Jorge de la Flor" class="profile-avatar" onerror="this.style.display='none'">
  
  <h1 class="profile-name">Jorge de la Flor</h1>
  <p class="profile-title" style="font-size: 1.1rem; font-weight: 400;">Software Architect & Protocol Developer</p>
  <p class="profile-title" style="font-weight: 300; color: var(--text-muted); font-size: 0.95rem;">
    Embedded Systems · Cyber-Physical Systems · Protocol Engineering
  </p>
  
  <!-- ESLOGAN -->
  <p style="font-size: 1.3rem; font-weight: 600; color: var(--accent-rust); margin: 0.5rem 0 0.2rem; letter-spacing: -0.02em;">
    “Piensa en Python, potencia en Rust.”
  </p>
  
  <p style="font-size: 0.85rem; color: var(--text-muted); margin-top: 0.2rem;">aka FrostCore</p>
  
  <div class="tech-badges">
    <span class="tech-badge rust"><i class="fas fa-cog"></i> Rust</span>
    <span class="tech-badge python"><i class="fab fa-python"></i> Python</span>
    <span class="tech-badge cpp"><i class="fas fa-microchip"></i> C/C++</span>
    <span class="tech-badge embedded"><i class="fas fa-microchip"></i> Embedded</span>
    <span class="tech-badge ml"><i class="fas fa-code-branch"></i> Protocol Engineering</span>
  </div>
  
  <div class="social-links">
    <a href="mailto:{{ site.author.email }}" class="social-link" title="Email"><i class="fas fa-envelope"></i></a>
    <a href="https://linkedin.com/in/{{ site.social.linkedin }}" class="social-link" title="LinkedIn" target="_blank"><i class="fab fa-linkedin-in"></i></a>
    <a href="https://github.com/{{ site.social.github }}" class="social-link" title="GitHub" target="_blank"><i class="fab fa-github"></i></a>
    <a href="{{ site.social.linktree }}" class="social-link" title="Linktree" target="_blank"><i class="fas fa-link"></i></a>
    {% if site.social.sessionize %}
    <a href="{{ site.social.sessionize }}" class="social-link" title="Sessionize" target="_blank"><i class="fas fa-calendar-alt"></i></a>
    {% endif %}
  </div>
</div>

---

## Sobre mí

<div style="font-size: 1.05rem; line-height: 1.8; color: var(--text-secondary);">
  <p><strong>Arquitecto de software y desarrollador de protocolos</strong> especializado en la convergencia entre el mundo digital y el físico. Diseño la lógica de alto nivel que define cómo se comunican los sistemas, mientras bajo al metal para optimizar cada ciclo en MCUs como ESP32, STM32 y RP2040.</p>
  
  <p>Creador de <strong>Apider</strong>, <strong>Pyperantio</strong> y <strong>OMNI-PY</strong> — tres plataformas que resuelven problemas de portabilidad, automatización y generación de código. Los principios que las unifican están formalizados como el <strong>Modelo Agnóstico (AMP)</strong> en mi libro en preparación: <em>The Agnostic Engineer: Architecture Beyond Infrastructure</em>.</p>
  
  <p>Combino una formación en <strong>International Business</strong> con experiencia práctica en ingeniería de software. He sido ponente invitado en <strong>Microsoft Build 2026</strong> y en <strong>Azure User Group Latam</strong>.</p>
</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/about/' | relative_url }}" class="cta-link">Ver más →</a>
</div>

---

## Servicios

<div class="card-grid">
  <div class="card">
    <h3 class="card-title"><i class="fas fa-building" style="color: #4fc3f7;"></i> Consultoría</h3>
    <p class="card-desc">Asesoramiento en arquitectura de software, diseño de protocolos, sistemas embebidos y CPS. Desde la estrategia hasta la implementación.</p>
  </div>
  
  <div class="card">
    <h3 class="card-title"><i class="fas fa-code" style="color: #8b5cf6;"></i> Desarrollo a medida</h3>
    <p class="card-desc">Soluciones personalizadas en Python, Rust y C/C++: firmware, herramientas CLI, backend, transpiladores y protocolos de comunicación.</p>
  </div>
  
  <div class="card">
    <h3 class="card-title"><i class="fas fa-graduation-cap" style="color: #f59e0b;"></i> Formación técnica</h3>
    <p class="card-desc">Workshops y mentoría para equipos: arquitectura de software, Rust embedded, Python avanzado, diseño de protocolos y buenas prácticas.</p>
  </div>
  
  <div class="card">
    <h3 class="card-title"><i class="fas fa-flask" style="color: #34d399;"></i> Investigación</h3>
    <p class="card-desc">Exploración de nuevas fronteras en arquitectura agnóstica, ingeniería de lenguajes, protocolos abiertos y sistemas distribuidos.</p>
  </div>
</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/services/' | relative_url }}" class="cta-link">Ver todos los servicios →</a>
</div>

---

## Proyectos destacados

<div class="card-grid">
  <div class="card">
    <h3 class="card-title"><i class="fas fa-cloud" style="color: #4fc3f7;"></i> Apider SDK</h3>
    <p class="card-desc">Runtime multi-tenant serverless en Azure Functions. Publicado en PyPI. Aislamiento por ContextVar, cifrado Fernet, servidor MCP stateless y facturación Paddle. <strong>61 tests</strong> en CI.</p>
  </div>
  
  <div class="card">
    <h3 class="card-title"><i class="fas fa-microchip" style="color: #DEA584;"></i> Pyperantio</h3>
    <p class="card-desc">Tooling propietario para generación de código firmware embebido. Soporte para <strong>4+ familias de MCUs</strong> con emisión automática de código a partir de modelos hardware-independientes. 🔒 IP filing.</p>
  </div>
  
  <div class="card">
    <h3 class="card-title"><i class="fas fa-code" style="color: #8b5cf6;"></i> OMNI-PY</h3>
    <p class="card-desc">Transpilador de Python a Java, Go y JavaScript. Capa AST en Python + <strong>TypeTracker en Rust</strong> (PyO3) que realiza inferencia de tipos y análisis de nulabilidad.</p>
  </div>
</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/projects/' | relative_url }}" class="cta-link">Ver todos los proyectos →</a>
</div>

---

## Stack Tecnológico

<div style="text-align: center; margin: 1.5rem 0;">
  <p style="font-weight: 500; font-size: 1.1rem; color: var(--text-secondary); margin-bottom: 1rem;">
    <strong>Lenguajes principales:</strong> Python · Rust · C/C++
  </p>
  
  <div class="tech-badges" style="justify-content: center; gap: 0.6rem;">
    <span class="tech-badge python"><i class="fab fa-python"></i> Python</span>
    <span class="tech-badge rust"><i class="fas fa-cog"></i> Rust</span>
    <span class="tech-badge cpp"><i class="fas fa-microchip"></i> C/C++</span>
    <span class="tech-badge embedded"><i class="fas fa-microchip"></i> Embedded</span>
    <span class="tech-badge ml"><i class="fas fa-code-branch"></i> Protocol Engineering</span>
    <span class="tech-badge" style="border-color: #4fc3f7; color: #4fc3f7;"><i class="fas fa-cloud"></i> Azure</span>
    <span class="tech-badge" style="border-color: #f59e0b; color: #f59e0b;"><i class="fas fa-lock"></i> Security</span>
  </div>
  
  <p style="font-size: 0.9rem; color: var(--text-muted); margin-top: 1rem;">
    <strong>Además:</strong> AST · PyO3 · MCP · Polars · PostgreSQL · SQLite · Docker · CI/CD · RTOS · UART, SPI, I²C, MQTT
  </p>
</div>

<div style="text-align: right; margin-top: 0.5rem;">
  <a href="{{ '/md_pages/stack/' | relative_url }}" class="cta-link">Ver stack completo →</a>
</div>

---

## Blog & Charlas

<div class="blog-talks-preview">
  <div class="preview-block">
    <h3><i class="fas fa-pen-fancy"></i> Último artículo</h3>
    {% assign latest_post = site.posts | sort: 'date' | reverse | first %}
    {% if latest_post %}
      <p class="preview-date">{{ latest_post.date | date: "%d/%m/%Y" }}</p>
      <h4><a href="{{ latest_post.url | relative_url }}">{{ latest_post.title }}</a></h4>
      <p>{{ latest_post.excerpt | strip_html | truncatewords: 20 }}</p>
      <a href="{{ '/md_pages/posts/' | relative_url }}#blog" class="cta-link">Ver todos los posts →</a>
    {% else %}
      <p>Próximamente nuevos artículos.</p>
    {% endif %}
  </div>
  
  <div class="preview-block">
    <h3><i class="fas fa-microphone-alt"></i> Última charla</h3>
    <p class="preview-date">Junio 2026</p>
    <h4>Microsoft Build 2026 — Azure User Group Latam</h4>
    <p>"Building a Multi-Tenant Python Runtime on Azure Functions"</p>
    <a href="{{ '/md_pages/posts/' | relative_url }}#talks" class="cta-link">Ver todas las charlas →</a>
  </div>
</div>

---

## Contacto

<p style="font-size: 1.05rem; color: var(--text-secondary);">
  ¿Tienes un proyecto en mente o buscas consultoría? Hablemos.
</p>

<div style="display: flex; gap: 1rem; flex-wrap: wrap; margin-top: 0.5rem;">
  <a href="mailto:{{ site.author.email }}" class="cta-button" style="display: inline-block; padding: 0.6rem 1.5rem; background: var(--accent-rust); color: #fff; border-radius: 50px; font-weight: 600; text-decoration: none;">
    <i class="fas fa-paper-plane" style="margin-right: 0.5rem;"></i> Email
  </a>
  <a href="{{ '/md_pages/contact/' | relative_url }}" class="cta-link" style="align-self: center;">Ver más →</a>
</div>
