---
layout: default
title: Blog & Charlas — Jorge de la Flor
---

# Blog & Charlas

Aquí encontrarás mis artículos técnicos y las charlas que he impartido en eventos.

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
      <p style="color: var(--text-secondary);">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      <a href="{{ post.url | relative_url }}" class="cta-link" style="font-size: 0.9rem;">Leer más →</a>
    </div>
    {% endfor %}
  </div>
{% endif %}

---

## 🎤 Charlas {#talks}

<div class="talks-list">

  <div class="talk-item">
    <h3>Microsoft Build 2026 Community Event — Azure User Group Latam</h3>
    <p class="talk-date"><i class="far fa-calendar-alt"></i> IDAT Lima, Perú · Junio 2026</p>
    <p style="color: var(--text-secondary);"><strong>"Building a Multi-Tenant Python Runtime on Azure Functions"</strong></p>
    <p style="color: var(--text-secondary); font-size: 0.95rem;">
      Ponencia invitada donde compartí la arquitectura y lecciones aprendidas al desarrollar <strong>Apider</strong>, un runtime serverless multi-tenant con aislamiento por ContextVar, cifrado Fernet, servidor MCP stateless y facturación Paddle.
    </p>
  </div>

  <!-- Espacio para futuras charlas -->
  <p style="color: var(--text-muted); margin-top: 1.5rem;">Próximas charlas y eventos en preparación.</p>

</div>

---

## 📢 ¿Quieres que hable en tu evento?

Si estás organizando un meetup, conferencia, workshop o podcast técnico y te gustaría que participe como ponente o invitado, escríbeme a [{{ site.author.email }}](mailto:{{ site.author.email }}).

**Temas que manejo:**
- Arquitectura de software y cloud-agnosticismo
- Diseño de protocolos para sistemas embebidos
- Ingeniería de lenguajes y transpiladores
- Rust y Python en sistemas críticos
- Cyber-Physical Systems y edge computing

---

[← Volver al inicio]({{ '/' | relative_url }})
