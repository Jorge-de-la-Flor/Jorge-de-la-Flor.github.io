---
layout: academy
title: "Snake Code Institute - Domina Python"
mode: "snake"
permalink: /md_pages/sci/
description: "Curso profesional de Python desde fundamentos hasta POO avanzada, SOLID y testing."
cta_link: "#inscripcion-snake"
# enroll_link_snake: "https://tuenlace-de-inscripcion.com/python-vanilla-pro"
cta_label: "Inscribirme"
---

<div class="hero">
  <div class="hero-logo">
    <img src="{{ '/assets/images/logo-sci.png' | relative_url }}" alt="Snake Code Institute">
  </div>
  <span class="badge">DOMINA PYTHON</span>
  <h1 class="hero-title">
    Snake Code <span class="gradient">Institute</span>
  </h1>
  <p class="hero-description">
    El lugar donde Python se aprende de verdad. Desde fundamentos hasta arquitectura profesional con POO, SOLID y testing.
  </p>
  <div class="hero-buttons">
    <a href="{{ '/md_pages/sci/temario/' | relative_url }}" class="btn btn-primary snake">
      Ver Temario Completo
      <svg width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6"/>
      </svg>
    </a>
    <a href="{{ '/md_pages/sci/inscripcion/' | relative_url }}" class="btn btn-secondary snake">
      Inscribirme Ahora
    </a>
  </div>
  <div class="stats">
    <div>
      <div class="stat-value">10</div>
      <div class="stat-label">Módulos</div>
    </div>
    <div>
      <div class="stat-value">50+</div>
      <div class="stat-label">Horas de contenido</div>
    </div>
    <div>
      <div class="stat-value">100%</div>
      <div class="stat-label">Práctico</div>
    </div>
  </div>
</div>

<div class="content-section" id="temario-snake">
  <h2 class="section-title">Lo que dominarás</h2>

  <div class="code-preview">
    <div class="code-header">
      <span class="code-dot red"></span>
      <span class="code-dot yellow"></span>
      <span class="code-dot green"></span>
      <span class="code-filename">data_processor.py</span>
    </div>
    <pre class="code-content"><span class="comment"># No solo aprenderás esto...</span>
<span class="function">print</span>(<span class="string">"Hola Mundo"</span>)


<span class="comment"># Aprenderás a construir esto:</span>
<span class="keyword">class</span> <span class="class">DataProcessor</span>:
    <span class="string">"""Procesador de datos siguiendo principios SOLID."""</span>

    <span class="keyword">def</span> <span class="function">__init__</span>(<span class="variable">self</span>, strategy: <span class="type">ProcessingStrategy</span>):
        <span class="variable">self</span>._strategy = strategy
        <span class="variable">self</span>._validators: <span class="type">list</span>[Validator] = []

    <span class="keyword">def</span> <span class="function">process</span>(<span class="variable">self</span>, data: <span class="type">DataFrame</span>) -> <span class="type">Result</span>:
        validated = <span class="variable">self</span>._validate(data)
        <span class="keyword">return</span> <span class="variable">self</span>._strategy.execute(validated)</pre>
  </div>

  <div class="modules-grid">
    <div class="module-card">
      <span class="module-num">01</span>
      <h3 class="module-title">Fundamentos</h3>
      <p class="module-desc">Variables, operadores, estructuras de control</p>
    </div>
    <div class="module-card">
      <span class="module-num">02</span>
      <h3 class="module-title">Funciones</h3>
      <p class="module-desc">Parámetros, scope, decoradores, closures</p>
    </div>
    <div class="module-card">
      <span class="module-num">03</span>
      <h3 class="module-title">Estructuras de Datos</h3>
      <p class="module-desc">Listas, diccionarios, sets, comprehensions</p>
    </div>
    <div class="module-card">
      <span class="module-num">04</span>
      <h3 class="module-title">POO Fundamentos</h3>
      <p class="module-desc">Clases, herencia, polimorfismo</p>
    </div>
    <div class="module-card">
      <span class="module-num">05</span>
      <h3 class="module-title">POO Avanzado</h3>
      <p class="module-desc">Métodos especiales, dataclasses, ABC</p>
    </div>
    <div class="module-card">
      <span class="module-num">06</span>
      <h3 class="module-title">SOLID</h3>
      <p class="module-desc">Principios de diseño de software</p>
    </div>
    <div class="module-card">
      <span class="module-num">07</span>
      <h3 class="module-title">Testing</h3>
      <p class="module-desc">Pytest, mocking, TDD</p>
    </div>
    <div class="module-card">
      <span class="module-num">08</span>
      <h3 class="module-title">Manejo de Errores</h3>
      <p class="module-desc">Excepciones, logging, debugging</p>
    </div>
    <div class="module-card">
      <span class="module-num">09</span>
      <h3 class="module-title">Archivos y Datos</h3>
      <p class="module-desc">I/O, JSON, CSV, bases de datos</p>
    </div>
    <div class="module-card">
      <span class="module-num">10</span>
      <h3 class="module-title">Proyecto Final</h3>
      <p class="module-desc">Aplicación completa con arquitectura limpia</p>
    </div>
  </div>
</div>

<div class="cta-section" id="inscripcion-snake">
  <h2 class="cta-title">¿Listo para dominar Python?</h2>
  <p class="cta-description">No pierdas más tiempo con tutoriales que no te llevan a ningún lado.</p>
  <a href="{{ '/md_pages/sci/inscripcion/' | relative_url }}" class="cta-button">Inscribirme Ahora</a>
</div>
