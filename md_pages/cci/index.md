---
layout: academy
title: Crab Code Institute - Domina Rust
description: El lugar donde Rust se aprende de verdad
cta_text: Inscribirme
cta_url: "#inscripcion"
---

<section class="section text-center">
  <div class="container">
    <div class="float-animation" style="font-size: 5rem; margin-bottom: 2rem;">
      🦀
    </div>
    
    <span class="badge">DOMINA RUST</span>
    
    <h1 class="title-xl" style="margin-top: 1.5rem;">
      Crab Code <span class="gradient-text">Institute</span>
    </h1>
    
    <p class="text-muted" style="max-width: 42rem; margin: 1.5rem auto 0; font-size: 1.125rem;">
      El lugar donde Rust se aprende de verdad. Desde ownership hasta sistemas de alto rendimiento.
    </p>
    
    <div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 1rem; margin-top: 2.5rem;">
      <a href="#temario" class="btn btn-primary">Ver Temario</a>
      <a href="#inscripcion" class="btn btn-secondary">Inscribirme</a>
    </div>
    
    <div class="stats-grid" style="margin-top: 4rem;">
      <div>
        <div class="stat-value">8</div>
        <div class="stat-label">Modulos</div>
      </div>
      <div>
        <div class="stat-value">40+</div>
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
        <span class="code-filename">main.rs</span>
      </div>
      <pre class="code-content"><span class="comment">// No solo aprenderas esto...</span>
<span class="function">println!</span>(<span class="string">"Hola Mundo"</span>);

<span class="comment">// Aprenderas a construir esto:</span>
<span class="keyword">pub struct</span> <span class="class">DataProcessor</span><<span class="lifetime">'a</span>, T: <span class="type">Process</span>> {
    strategy: &<span class="lifetime">'a</span> T,
    validators: <span class="type">Vec</span><<span class="type">Box</span><<span class="keyword">dyn</span> <span class="type">Validate</span>>>,
}

<span class="keyword">impl</span><<span class="lifetime">'a</span>, T: <span class="type">Process</span>> <span class="class">DataProcessor</span><<span class="lifetime">'a</span>, T> {
    <span class="keyword">pub fn</span> <span class="function">process</span>(&<span class="variable">self</span>, data: <span class="type">DataFrame</span>) -> <span class="type">Result</span><<span class="type">Output</span>> {
        <span class="keyword">let</span> validated = <span class="variable">self</span>.validate(&data)?;
        <span class="variable">self</span>.strategy.execute(validated)
    }
}</pre>
    </div>
    
    <div class="grid-3" style="margin-top: 3rem;">
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">01</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Fundamentos</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Variables, tipos, control flow</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">02</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Ownership</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Borrowing, lifetimes, memoria</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">03</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Structs & Enums</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Pattern matching, Option, Result</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">04</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Traits</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Generics, bounds, impl</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">05</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Error Handling</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Result, ?, custom errors</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">06</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Concurrencia</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Threads, async/await, Tokio</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">07</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Unsafe & FFI</h3>
        <p class="text-muted" style="font-size: 0.875rem;">Raw pointers, C interop</p>
      </div>
      <div class="card">
        <span style="color: var(--crab-primary); font-weight: 700;">08</span>
        <h3 style="margin-top: 0.5rem; font-weight: 600;">Proyecto Final</h3>
        <p class="text-muted" style="font-size: 0.875rem;">CLI tool con async</p>
      </div>
    </div>
  </div>
</section>

<section class="section text-center" id="inscripcion">
  <div class="container">
    <h2 class="title-lg">Listo para dominar Rust?</h2>
    <p class="text-muted" style="margin-top: 1rem;">Aprende el lenguaje mas amado por desarrolladores.</p>
    <a href="#" class="btn btn-primary btn-lg" style="margin-top: 2rem;">Inscribirme Ahora</a>
  </div>
</section>
