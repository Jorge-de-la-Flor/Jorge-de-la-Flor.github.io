---
layout: academyy
title: Snake Code Institute - Domina Python
description: El lugar donde Python se aprende de verdad
cta_text: Inscribirme
cta_url: "#inscripcion"
---

<section class="section text-center">
  <div class="container">
    <div class="float-animation" style="font-size: 5rem; margin-bottom: 2rem;">
      <img src="{{ '/assets/images/logo-sci.png' | relative_url }}" alt="Snake Code Institute" style="width: 128px; height: 128px; filter: drop-shadow(0 0 30px rgba(59, 130, 246, 0.3));">
    </div>
    
    <span class="badge">DOMINA PYTHON</span>
    
    <h1 class="title-xl" style="margin-top: 1.5rem;">
      Snake Code <span class="gradient-text">Institute</span>
    </h1>
    
    <p class="text-muted" style="max-width: 42rem; margin: 1.5rem auto 0; font-size: 1.125rem;">
      El lugar donde Python se aprende de verdad. Desde fundamentos hasta arquitectura profesional con POO, SOLID y testing.
    </p>
    
    <div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 1rem; margin-top: 2.5rem;">
      <a href="#temario" class="btn btn-primary">Ver Temario</a>
      <a href="#inscripcion" class="btn btn-secondary">Inscribirme</a>
    </div>
    
    <div class="stats-grid" style="margin-top: 4rem;">
      <div>
        <div class="stat-value">10</div>
        <div class="stat-label">Modulos</div>
      </div>
      <div>
        <div class="stat-value">50+</div>
        <div class="stat-label">Horas</div>
      </div>
      <div>
        <div class="stat-value">100%</div>
        <div class="stat-label">Practico</div>
      </div>
    </div>
  </div>
</section>

<section class="section" id="temario">
  <div class="container">
    <h2 class="title-lg">Lo que dominaras</h2>
    
    <div class="code-block" style="margin-top: 2rem;">
      <div class="code-header">
        <span class="code-dot red"></span>
        <span class="code-dot yellow"></span>
        <span class="code-dot green"></span>
        <span class="code-filename">data_processor.py</span>
      </div>
      <pre class="code-content"><span class="comment"># No solo aprenderas esto...</span>
<span class="function">print</span>(<span class="string">"Hola Mundo"</span>)

<span class="comment"># Aprenderas a construir esto:</span>
<span class="keyword">class</span> <span class="class">DataProcessor</span>:
    <span class="string">"""Procesador siguiendo SOLID."""</span>

    <span class="keyword">def</span> <span class="function">__init__</span>(<span class="variable">self</span>, strategy: <span class="type">Strategy</span>):
        <span class="variable">self</span>._strategy = strategy

    <span class="keyword">def</span> <span class="function">process</span>(<span class="variable">self</span>, data: <span class="type">DataFrame</span>) -> <span class="type">Result</span>:
        <span class="keyword">return</span> <span class="variable">self</span>._strategy.execute(data)</pre>
    </div>
    
    <div class="grid-3" style="margin-top: 3rem;">
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">01</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Fundamentos</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Variables, operadores, control</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">02</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Funciones</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Scope, decoradores, closures</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">03</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Estructuras de Datos</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Listas, dicts, comprehensions</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">04</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">POO Fundamentos</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Clases, herencia, polimorfismo</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">05</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">POO Avanzado</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Dunder, dataclasses, ABC</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">06</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">SOLID</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Principios de diseno</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">07</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Testing</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Pytest, mocking, TDD</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">08</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Errores</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Excepciones, logging</p>
      </div>
      <div class="card">
        <span style="color: var(--snake-primary); font-weight: 700;">09</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Archivos</h3>
        <p class="text-muted" style="font-size: 0.875rem;">I/O, JSON, CSV, DB</p>
      </div>
    </div>
  </div>
</section>

<section class="section text-center" id="inscripcion">
  <div class="container">
    <h2 class="title-lg">Listo para dominar Python?</h2>
    <p class="text-muted" style="margin-top: 1rem;">No pierdas mas tiempo con tutoriales que no te llevan a ningun lado.</p>
    <a href="#" class="btn btn-primary btn-lg" style="margin-top: 2rem;">Inscribirme Ahora</a>
  </div>
</section>
