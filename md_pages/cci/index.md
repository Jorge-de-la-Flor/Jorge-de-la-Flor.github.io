---
layout: academy
title: "Crab Code Institute - Domina Rust"
mode: "crab"
permalink: /md_pages/cci/
description: "Curso intensivo de Rust para desarrolladores de sistemas, performance y seguridad de memoria."
cta_link: "#inscripcion-crab"
cta_label: "Inscribirme"
---

<div class="hero">
  <div class="hero-logo">🦀</div>
  <span class="badge">DOMINA RUST</span>
  <h1 class="hero-title">
    Crab Code <span class="gradient">Institute</span>
  </h1>
  <p class="hero-description">
    Aprende Rust desde cero, con foco en ownership, concurrencia segura y sistemas reales de alto rendimiento.
  </p>
  <div class="hero-buttons">
    <a href="{{ '/md_pages/cci/temario/' | relative_url }}" class="btn btn-primary crab">
      Ver Temario Completo
      <svg width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6"/>
      </svg>
    </a>
    <a href="{{ '/md_pages/cci/inscripcion/' | relative_url }}" class="btn btn-secondary crab">
      Inscribirme Ahora
    </a>
  </div>
  <div class="stats">
    <div>
      <div class="stat-value">8</div>
      <div class="stat-label">Módulos</div>
    </div>
    <div>
      <div class="stat-value">40+</div>
      <div class="stat-label">Horas de contenido</div>
    </div>
    <div>
      <div class="stat-value">100%</div>
      <div class="stat-label">Sistemas reales</div>
    </div>
  </div>
</div>

<div class="content-section" id="temario-crab">
  <h2 class="section-title">Lo que dominarás</h2>

  <div class="code-preview">
    <div class="code-header">
      <span class="code-dot red"></span>
      <span class="code-dot yellow"></span>
      <span class="code-dot green"></span>
      <span class="code-filename">data_processor.rs</span>
    </div>
    <pre class="code-content"><span class="comment">// No solo aprenderás esto...</span>
<span class="keyword">fn</span> <span class="function">main</span>() {
    <span class="function">println!</span>(<span class="string">"Hola Mundo"</span>);
}


<span class="comment">// Aprenderás a construir esto:</span>
<span class="keyword">pub struct</span> <span class="class">DataProcessor</span>&lt;T: <span class="type">Strategy</span>&gt; {
    strategy: T,
    validators: <span class="type">Vec</span>&lt;Box&lt;<span class="keyword">dyn</span> <span class="type">Validator</span>&gt;&gt;,
}


<span class="keyword">impl</span>&lt;T: <span class="type">Strategy</span>&gt; <span class="class">DataProcessor</span>&lt;T&gt; {
    <span class="keyword">pub fn</span> <span class="function">process</span>(&<span class="variable">self</span>, data: DataFrame) -> <span class="type">Result</span>&lt;Output, Error&gt; {
        <span class="keyword">let</span> validated = <span class="variable">self</span>.validate(data)?;
        <span class="variable">self</span>.strategy.execute(validated)
    }
}</pre>
  </div>

  <div class="modules-grid">
    <div class="module-card">
      <span class="module-num">01</span>
      <h3 class="module-title">Fundamentos</h3>
      <p class="module-desc">Variables, ownership, borrowing</p>
    </div>
    <div class="module-card">
      <span class="module-num">02</span>
      <h3 class="module-title">Control de Flujo</h3>
      <p class="module-desc">Pattern matching, enums, Option, Result</p>
    </div>
    <div class="module-card">
      <span class="module-num">03</span>
      <h3 class="module-title">Structs y Traits</h3>
      <p class="module-desc">Tipos personalizados, polimorfismo con traits</p>
    </div>
    <div class="module-card">
      <span class="module-num">04</span>
      <h3 class="module-title">Memoria y Lifetimes</h3>
      <p class="module-desc">Referencias, lifetimes, seguridad de memoria</p>
    </div>
    <div class="module-card">
      <span class="module-num">05</span>
      <h3 class="module-title">Colecciones</h3>
      <p class="module-desc">Vec, HashMap, iteradores</p>
    </div>
    <div class="module-card">
      <span class="module-num">06</span>
      <h3 class="module-title">Error Handling</h3>
      <p class="module-desc">Result, ?, errores personalizados</p>
    </div>
    <div class="module-card">
      <span class="module-num">07</span>
      <h3 class="module-title">Concurrencia</h3>
      <p class="module-desc">Threads, async/await, channels</p>
    </div>
    <div class="module-card">
      <span class="module-num">08</span>
      <h3 class="module-title">Proyecto Final</h3>
      <p class="module-desc">CLI o servicio web con Axum</p>
    </div>
  </div>
</div>

<div class="cta-section" id="inscripcion-crab">
  <h2 class="cta-title">¿Listo para dominar Rust?</h2>
  <p class="cta-description">El lenguaje del futuro para sistemas de alto rendimiento.</p>
  <a href="{{ '/md_pages/cci/inscripcion/' | relative_url }}" class="cta-button">Inscribirme Ahora</a>
</div>
