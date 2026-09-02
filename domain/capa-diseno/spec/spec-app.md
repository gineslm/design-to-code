# spec-app — requisitos globales de la app

**Versión:** v0.4 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** plantilla-hoja-requisitos-app.md v0.3 (renombrado; DS→spec-ds, navegación→spec-navegacion), metodologia-capa-diseno.md v0.22.
**Tier:** 2 (capa `diseno`) · **Clase:** hoja de requisitos.

> **Qué es.** La norma de los **requisitos globales de la app** — lo que aplica a toda la app y no vive en una spec concreta. Aloja también el **registro y propagación** del ámbito compartido técnico↔diseño.
> **Qué NO incluye:** el DS (→ `spec-ds`), la navegación (→ `spec-navegacion`), ni el criterio de aceptación del paquete completo (→ `spec-vision-general`).

---

## 1 · Listado de componentes
- **Inventario completo** de componentes compartidos — ☐.
- **Cada patrón repetido, extraído una sola vez** — ☐.
- **Cada componente con su ficha** — ☐.

## 2 · Estructura y roles de archivos
> Qué archivo cumple qué rol, para que la implementación no lo infiera.
- **Cada archivo declara su rol** — ☐. Taxonomía: **componente** (lleva ficha) · **vista** (lleva ficha) · **prototipo** (no se convierte a código; referencia del routing) · **documento** (trazabilidad/notas; no se convierte) · **sistema de diseño** (tokens).
- **Documento de trazabilidad** — ☐ existe y clasifica cada archivo real por su rol.

## 3 · Ámbito compartido técnico↔diseño
> Decisiones a la vez técnicas y de diseño; viven aquí, las fichas de vista las aplican.
- **Plataforma** — *ej.: web · móvil · híbrida.*
- **Breakpoints** — *ej.: <600 · 600–1024 · >1024.*
- **Objetivo de accesibilidad** — *ej.: WCAG 2.1 AA.*
- **Soporte de navegadores/dispositivos** — *ej.: últimas 2 versiones.*
- **Otras restricciones técnicas con impacto visual** — una fila por restricción.

## 4 · Reglas globales de diseño
> Reglas que aplican a toda la app; las fichas las difieren aquí.
- Una fila por regla — *ej.: tono de tú · datos sintéticos · error con texto además de color · foco visible.*

## 5 · Registro de decisiones globales de diseño
- Una fila por decisión: qué se decidió · dónde impacta. *(También al registro de capa.)*

## 6 · Decisiones técnicas que afectan al diseño — propagación a la capa de definición
- Una fila por decisión: qué cambió · qué diseño afecta · ☐ propagado a la capa de definición.

---

## Criterio de aceptación (de esta spec)
- ☐ Listado de componentes completo (§1) · ☐ Estructura y roles con trazabilidad (§2) · ☐ Ámbito técnico↔diseño (§3) · ☐ Reglas globales volcadas (§4) · ☐ Decisiones técnicas pendientes propagadas (§6).
> El criterio de aceptación **del paquete completo** (todas las specs) vive en `spec-vision-general`.
