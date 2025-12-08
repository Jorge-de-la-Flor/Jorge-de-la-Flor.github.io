---
layout: default
title: Snake & Crab Code Institute
description: Programas de Python (SCI) y Rust (CCI) en un solo lugar.
---

<div class="sci-cci-toggle">
  <button class="toggle-btn active" data-target="sci">
    <span class="dot"></span> Snake Code Institute
  </button>
  <button class="toggle-btn" data-target="cci">
    <span class="dot"></span> Crab Code Institute
  </button>
</div>

<div class="sci-cci-slider show-sci" id="sci-cci-slider">
  <div class="slides">
    <!-- SCI -->
    <section class="slide sci">
      <header class="hero">
        <h1>Snake Code Institute</h1>
        <p>Programa intensivo para dominar Python desde cero hasta proyectos reales.</p>
        <div class="hero-actions">
          <a href="{{ '/md_pages/sci/' | relative_url }}" class="primary-btn">Ir a la página SCI</a>
          <a href="#temario-sci" class="ghost-btn">Ver temario SCI</a>
        </div>
      </header>

      <main class="content">
        <section>
          <h2>Somos Snake Code</h2>
          <p>
            Python como herramienta principal para construir software útil: scripts, automatización,
            backend y proyectos que sí usarías en la vida real.
          </p>
        </section>

        <section id="temario-sci">
          <h2>Temario Snake Code</h2>
          <ul>
            <li>Fundamentos de programación con Python</li>
            <li>Estructuras de datos y módulos</li>
            <li>POO aplicada a proyectos</li>
            <li>Buenas prácticas y primeras automaciones</li>
          </ul>
          <p>
            Puedes ver el temario completo en la página dedicada de SCI:
            <a href="{{ '/md_pages/sci/temario' | relative_url }}">Temario completo SCI</a>.
          </p>
        </section>
      </main>
    </section>

    <!-- CCI -->
    <section class="slide cci">
      <header class="hero">
        <h1>Crab Code Institute</h1>
        <p>Rust para gente que ya programa y quiere ir a sistemas, performance y control fino.</p>
        <div class="hero-actions">
          <a href="{{ '/md_pages/cci/' | relative_url }}" class="primary-btn cci-btn">Ir a la página CCI</a>
          <a href="#temario-cci" class="ghost-btn cci-ghost">Ver temario CCI</a>
        </div>
      </header>

      <main class="content">
        <section>
          <h2>Somos Crab Code</h2>
          <p>
            Rust pensado para embedded, CLI tools y sistemas donde los detalles importan, sin
            perder el toque pedagógico directo y sin humo.
          </p>
        </section>

        <section id="temario-cci">
          <h2>Temario Crab Code</h2>
          <ul>
            <li>Fundamentos de Rust y mentalidad de ownership</li>
            <li>Tipos, enums, pattern matching y módulos</li>
            <li>Proyectos de línea de comandos y utilidades</li>
            <li>Camino hacia embedded / sistemas</li>
          </ul>
          <p>
            Aquí luego enlazas al temario completo de CCI cuando lo tengas:
            de>/md_pages/cci/temario</code>.
          </p>
        </section>
      </main>
    </section>
  </div>
</div>
