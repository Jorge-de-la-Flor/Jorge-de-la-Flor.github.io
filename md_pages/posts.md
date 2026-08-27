---
layout: default
title: Blog & Charlas — Jorge de la Flor
---

# Blog & Charlas

Este es mi espacio para compartir **ideas, investigaciones, experimentos y experiencias de ingeniería**, así como las charlas y workshops en los que participo como ponente.

Aquí encontrarás contenido sobre arquitectura de sistemas, software de sistemas, cloud, Rust, Python, ingeniería de lenguajes, sistemas embebidos y Cyber-Physical Systems.

---

<div class="blog-talks-grid">

  <!-- BLOG -->

  <section class="content-column">

    <div class="section-heading">

      <span class="section-icon">
        <i class="fas fa-pen-fancy"></i>
      </span>

      <div>
        <h2 style="margin-bottom: 0.2rem;">Blog</h2>

        <p style="color: var(--text-muted); margin: 0;">
          Artículos, investigaciones y experimentos técnicos.
        </p>
      </div>

    </div>

    {% assign posts = site.posts | sort: 'date' | reverse %}

    {% if posts.size == 0 %}

      <div class="empty-state">

        <i class="fas fa-feather-alt"></i>

        <p>
          Próximamente nuevos artículos técnicos.
        </p>

      </div>

    {% else %}

      <div class="posts-list">

        {% for post in posts %}

        <article class="post-card">

          <p class="post-meta">

            <i class="far fa-calendar-alt"></i>

            {{ post.date | date: "%d/%m/%Y" }}

            {% if post.categories.size > 0 %}

              ·

              {% for category in post.categories %}

                <span class="post-category">
                  {{ category }}
                </span>

              {% endfor %}

            {% endif %}

          </p>

          <h3>
            <a href="{{ post.url | relative_url }}">
              {{ post.title }}
            </a>
          </h3>

          <p class="post-excerpt">
            {{ post.excerpt | strip_html | truncatewords: 35 }}
          </p>

          <a href="{{ post.url | relative_url }}"
             class="cta-link">

            Leer artículo →

          </a>

        </article>

        {% endfor %}

      </div>

    {% endif %}

  </section>


  <!-- CHARLAS -->

  <section class="content-column">

    <div class="section-heading">

      <span class="section-icon">
        <i class="fas fa-microphone-alt"></i>
      </span>

      <div>

        <h2 style="margin-bottom: 0.2rem;">
          Charlas
        </h2>

        <p style="color: var(--text-muted); margin: 0;">
          Conferencias, workshops y presentaciones técnicas.
        </p>

      </div>

    </div>


    <div class="talks-list">


      <!-- CSWEEK -->

      <article class="talk-item">

        <p class="talk-date">

          <i class="far fa-calendar-alt"></i>

          Agosto 2026 · Lima, Perú

        </p>

        <h3>

          <a href="{{ 'md_pages/talks/csweek-2026/' | relative_url }}">

            Aislamiento y Límites de Confianza en Producción:
            Construyendo Sistemas a Prueba de Fallos

          </a>

        </h3>

        <p class="talk-event">

          CSWeek 2026

        </p>

        <p class="talk-description">

          Cómo diseñar sistemas que mantengan límites de confianza
          claros, preserven invariantes y puedan fallar de forma segura
          en producción.

        </p>

        <div class="talk-links">

          <a href="{{ 'md_pages/talks/csweek-2026/' | relative_url }}"
             class="cta-link">

            Ver charla →

          </a>

        </div>

      </article>


      <!-- MICROSOFT BUILD -->

      <article class="talk-item">

        <p class="talk-date">

          <i class="far fa-calendar-alt"></i>

          Junio 2026 · Lima, Perú

        </p>

        <h3>

          <a href="{{ 'md_pages/talks/microsoft-build-2026/' | relative_url }}">

            Building a Multi-Tenant Python Runtime
            on Azure Functions

          </a>

        </h3>

        <p class="talk-event">

          Microsoft Build 2026 Community Event ·
          Azure User Group Latam

        </p>

        <p class="talk-description">

          Arquitectura y lecciones de ingeniería detrás de la
          construcción de un runtime Python serverless
          multi-tenant sobre Azure Functions.

        </p>

        <div class="talk-links">

          <a href="{{ 'md_pages/talks/microsoft-build-2026/' | relative_url }}"
             class="cta-link">

            Ver charla →

          </a>

        </div>

      </article>


    </div>

  </section>

</div>

---

## Temas

<div class="topic-grid">

  <span class="topic-tag">Arquitectura de sistemas</span>
  <span class="topic-tag">Sistemas distribuidos</span>
  <span class="topic-tag">Software de sistemas</span>
  <span class="topic-tag">Cloud</span>
  <span class="topic-tag">Rust</span>
  <span class="topic-tag">Python</span>
  <span class="topic-tag">Ingeniería de lenguajes</span>
  <span class="topic-tag">Generación de código</span>
  <span class="topic-tag">Sistemas embebidos</span>
  <span class="topic-tag">Cyber-Physical Systems</span>
  <span class="topic-tag">Protocolos</span>
  <span class="topic-tag">Seguridad y confiabilidad</span>
  <span class="topic-tag">Infraestructura para agentes IA</span>
  <span class="topic-tag">Modelado de sistemas</span>

</div>

---

## ¿Quieres que participe en tu evento?

Si estás organizando un **meetup, conferencia, workshop, podcast técnico o actividad académica** y quieres contar conmigo como ponente o invitado, puedes escribirme directamente.

📩 **[{{ site.author.email }}](mailto:{{ site.author.email }})**

Estoy especialmente interesado en espacios donde pueda compartir experiencias prácticas sobre **arquitectura de sistemas, software de sistemas, Rust, Python, ingeniería de lenguajes, sistemas embebidos y Cyber-Physical Systems**.

---

[← Volver al inicio]({{ '/' | relative_url }})