# spec-vision-general — sistema de especificaciones (capa de diseño)

**Versión:** v0.2 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** spec-app v0.4, spec-ds v0.1, spec-navegacion v0.1, spec-entidades v0.1, spec-vista v0.3, spec-componente v0.7, metodologia-capa-diseno.md v0.22.
**Tier:** 2 (capa `diseno`) · **Clase:** índice.

> **Qué es.** El mapa de **todas las especificaciones** de la capa de diseño: los niveles, qué captura cada uno y qué documento lo define. El conjunto documenta, de forma determinada, **todo lo que la capa de implementación necesita para traducir el diseño a código** — sin que nada quede solo "de palabra".
> **Cómo leerlo.** Los niveles **anidan** de lo global a lo atómico; cada spec es **independiente** (no se referencian entre sí como método) y este índice es quien las conecta. El detalle de cada nivel vive en su documento.

---

## 1 · El esquema

```
spec-app ─────────── requisitos globales (norma)
  │  listado de componentes · estructura y roles de archivos
  │  ámbito técnico↔diseño · reglas globales · propagación técnica
  │
  ├─ spec-ds ──────── tokens (primitivos + semánticos)        ← base de estilo
  ├─ spec-navegacion ─ pantallas + transiciones + prototipo   → routing
  ├─ spec-entidades ── modelo de datos (viene de definición)  ← lo referencian vista y componente
  │
  └─ spec-vista ───── cada pantalla
        │  compone ↓
        └─ spec-componente ── cada pieza reutilizable
              │  referencian ↓
              └─ spec-ds (tokens semánticos) · spec-entidades (datos)
```

**Anidamiento:** app → (ds · navegación · entidades) → vistas → componentes → (ds · entidades). Cada nivel referencia hacia abajo; ninguno redefine lo del inferior.

---

## 2 · Los niveles

> **Clase:** *molde* (se rellena por instancia) · *hoja de requisitos* (norma) · *índice*.

| Spec | Clase | Qué captura |
|---|---|---|
| `spec-app` | hoja de requisitos | requisitos globales: listado de componentes, estructura/roles de archivos, ámbito técnico↔diseño, reglas globales, propagación técnica |
| `spec-ds` | hoja de requisitos | dos capas de tokens, alcance mínimo, **contrato de nombres semánticos** (no reconstruye el DS) |
| `spec-navegacion` | hoja de requisitos | pantallas, transiciones (origen→acción→destino), prototipo → base del routing |
| `spec-entidades` | molde | modelo de datos (entidades, campos, relaciones); nace en definición, se referencia donde se usa |
| `spec-vista` | molde | cada pantalla: composición, layout/responsive, estados, navegación, comportamiento, datos que muestra |
| `spec-componente` | molde | cada pieza: tipo/nativo, props, estados+render, tokens, comportamiento, accesibilidad, datos que representa |
| `spec-vision-general` | índice | este documento |

---

## 3 · Clases de spec (el tipo común)

Todas comparten cabecera estándar y declaran su **clase**. Dos clases operativas:

- **Molde** — se rellena por cada instancia y produce N fichas (componente, vista, entidades). El artefacto rellenado es tier 3.
- **Hoja de requisitos** — norma única de un artefacto global (app, ds, navegación); dice qué debe cumplirse, no se rellena por ítem.

Esta separación es la que buscabas: **plantillas de requisitos** (esta carpeta, lo que la implementación busca y usa) frente a **descripciones de proceso o normas de proceder** (`metodologia-capa-diseno`, `fases-proceso-diseno`), que viven fuera de `spec/`.

---

## 4 · Qué garantiza el conjunto

Con los siete documentos completos, un lector **sin acceso a la conversación de diseño** tiene todo lo necesario para traducir a código: la base de estilo (`spec-ds`), cómo conectan las pantallas (`spec-navegacion`), qué datos maneja (`spec-entidades`), qué es cada pieza (`spec-componente`), cómo se componen las pantallas (`spec-vista`) y las reglas globales (`spec-app`). **Ese es el criterio de aceptación del paquete completo**, visto como sistema.

---

## Pendiente
- **Arquitectura de la información** — la nombramos y la aparcamos; si hace falta, su sitio sería un `spec-arquitectura` propio o dentro de `spec-app`. Hoy no se incluye.
