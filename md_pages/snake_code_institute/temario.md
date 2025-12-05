---
layout: default
title: "Curso Python Vanilla PRO – Temario Completo"
---

# Curso Python Vanilla PRO – Temario Completo

## Módulo 1 – Introducción, filosofía y fundamentos

- Qué es Python y para qué se usa.
- Python como lenguaje: interpretado vs compilado; tipado dinámico vs estático.
- Implementaciones de Python:
  - CPython (implementación por defecto en C).
  - Mención de PyPy, Cython y Numba como caminos para rendimiento.
- Just-In-Time vs Ahead-Of-Time:
  - Idea general de JIT (ejemplo PyPy/Numba).
  - Idea general de AOT (ejemplo C/Rust).
- PEPs y filosofía de Python:
  - Qué es una PEP.
  - PEP 20 – Zen de Python (ideas principales, import this).
- Tipos de datos básicos en Python: int, float, bool, str, NoneType.
- Comparación con tipos de bajo nivel en otros lenguajes: int8, int16, int32, int64, float32, float64, char, short, long, etc., y cómo eso aparece luego en NumPy.
- Crear variables y constantes.
- Números y operadores aritméticos.
- Operadores relacionales y lógicos.
- Pedir valores por teclado.
- Generar nuevos tipos de datos simples y múltiples variables.
- Laboratorio: ejercicios integradores de introducción.

## Módulo 2 – Listas y manejo de copias

- Listas.
- Índices.
- Sublistas (slicing).
- Métodos de la lista – Parte 1 y 2.
- List comprehensions (creación compacta de listas).
- Matrices (listas de listas).
- Copias en Python (parte 1):
  - Asignación vs copia superficial en listas.
  - list.copy() y efectos en listas anidadas.
- Laboratorio: problemas con listas.

## Módulo 3 – Tuplas

- Tuplas.
- Crear tuplas.
- Desempaquetado de tuplas – Parte 1 y 2.
- Función zip.
- Funciones y operaciones con tuplas.
- Laboratorio: uso de tuplas y zip.

## Módulo 4 – Strings y formateo moderno

- Strings.
- Strings como listas.
- Generar nuevos strings.
- Método .format().
- f-strings (formateo moderno).
- u-strings: prefijo u para Unicode, contexto histórico Python 2 vs Python 3 (ahora por defecto).
- r-strings (raw strings): rutas, regex y escapes.
- t-strings / template strings (Python 3.14+): idea y diferencia con f-strings para casos de seguridad y plantillas.
- Función print (formateo y trucos).
- Búsqueda en listas y secuencias.
- Métodos de listas aplicados a colecciones de texto.
- Laboratorio: formateo de texto y mini scripts.

## Módulo 5 – Diccionarios y copias avanzadas

- Diccionarios.
- Llaves de diccionarios.
- Obtener elementos.
- Llaves, valores y pares.
- Actualizar diccionarios.
- Dict comprehensions (creación compacta de diccionarios).
- Copias en Python (parte 2):
  - .copy() en diccionarios.
  - Módulo copy: copy y deepcopy con estructuras anidadas (listas/dicts dentro de dicts).
- Laboratorio: modelos de datos con diccionarios.

## Módulo 6 – Condiciones y ciclos

- None y valores falsos.
- if (partes 1 y 2), else, elif, condiciones anidadas.
- match (pattern matching básico).
- Operador ternario.
- for / for-each.
- Función range.
- Ciclo while (partes 1 y 2).
- break, continue y pass.
- Laboratorio: problemas de lógica, bucles y decisiones.

## Módulo 7 – Funciones, type hints y programación avanzada

- Crear funciones.
- Parámetros y retorno de valores.
- Retornar múltiples valores.
- Valores por nombre y posición.
- Valores por defecto.
- *args, **kwargs y combinación.
- Funciones como ciudadanos de primera clase.
- Funciones anidadas.
- Variables como funciones.
- Funciones lambda.
- Callbacks.
- Retornar funciones.
- Closures.
- Decoradores (creación y uso).
- Docstrings y buenas prácticas de documentación.
- Anotaciones de tipos (type hints) en funciones: sintaxis básica, Optional, Union, List, Dict, etc.
- Introducción a type-checking con mypy u otra herramienta (revisión estática de tipos).
- Laboratorio: funciones, closures, decoradores y type hints.

## Módulo 8 – POO en Python (OOP PRO, SOLID, DI y patrones)

- Crear clases.
- Método __init__.
- Atributos dinámicos.
- Métodos de instancia.
- Atributos “privados” y convenciones.
- Properties (getters/setters “pythónicas”).
- Herencia y sobrescritura de métodos.
- Herencia múltiple.
- Polimorfismo.
- Clases abstractas y ABC (módulo abc).
- Interfaces y contratos de código usando ABC.
- Decoradores en POO: @classmethod, @staticmethod y @dataclass aplicados a clases.
- Type hints en clases y métodos, uso de forward references para evitar imports circulares.
- Principios SOLID (visión general, estilo Pythonic).
- Inyección de dependencias: pasar dependencias por constructor o parámetros en lugar de crearlas dentro de la clase.
- Patrones de diseño básicos en Python:
  - Singleton (concepto y advertencias).
  - Factory / factory method usando cls y funciones que crean instancias.
- Laboratorio: pequeño sistema orientado a objetos aplicando SOLID “light”, DI y un patrón simple.

## Módulo 9 – Módulos, paquetes, archivos, pip, serialización, errores y optimización

- Módulos y paquetes: import, estructura de carpetas, __init__.py.
- Entornos virtuales básicos (venv) y organización de proyectos.
- Gestor de paquetes con pip:
  - Qué es pip y qué es PyPI.
  - Comandos básicos: pip install, pip uninstall, pip list.
  - requirements.txt y pip install -r requirements.txt.
  - Uso de pip dentro de entornos virtuales.
- Manejo de archivos: lectura y escritura de archivos de texto.
- Manejo de CSV.
- Manejo de JSON.
- Serialización y deserialización:
  - Serializar datos a JSON (json.dump, json.dumps).
  - Leer y reconstruir datos desde JSON (json.load, json.loads).
  - Qué es serialización y para qué sirve (guardar estado, comunicar entre sistemas).
  - (Opcional) Mención de pickle y uso responsable.
- Manejo de errores y excepciones:
  - try/except/else/finally.
  - raise y excepciones personalizadas.
- Optimización básica en Python (enfocada a data analysis):
  - “Primero medir, luego optimizar”: idea de profiling simple.
  - Evitar loops innecesarios y preferir operaciones vectorizadas (introducción conceptual a NumPy/pandas).
  - Elegir estructuras adecuadas (listas vs diccionarios vs sets) y minimizar copias grandes de datos.
  - Mención de librerías optimizadas (NumPy, pandas) y JIT con Numba como caminos para acelerar secciones críticas.
- Laboratorio: app que guarda/carga datos en JSON, maneja errores y aplica al menos una mejora simple de rendimiento.

## Módulo 10 – Testing y proyecto final

- Introducción a testing con unittest o pytest.
- Escribir tests básicos para funciones y clases.
- Ejecutar pruebas y entender resultados.
- Proyecto final:
  - Definición del problema.
  - Diseño con POO, SOLID “light”, DI y type hints.
  - Implementación usando funciones avanzadas, clases, archivos y serialización.
  - Manejo de errores en el flujo principal.
  - Pruebas básicas del proyecto con unittest/pytest.

[back](./)
