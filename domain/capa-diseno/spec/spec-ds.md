# spec-ds — requisitos del sistema de diseño

**Versión:** v0.1 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** plantilla-hoja-requisitos-app.md v0.3 (§1, extraído), metodologia-capa-diseno.md v0.22.
**Tier:** 2 (capa `diseno`) · **Clase:** hoja de requisitos.

> **Qué es.** Los requisitos que el **sistema de diseño** debe cumplir para la implementación. **No reconstruye el DS** —eso lo gestiona la herramienta de diseño de forma nativa—; fija **qué debe exponer y cómo se nombra**, para que la implementación lo consuma sin duplicar lo que la herramienta ya organiza.

## Requisitos
- **Dos capas de tokens** — ☐ el DS separa **primitivos** (valores crudos: paleta, escala) de **semánticos** (nombran un uso: superficie, primario, espaciado-m…).
- **Regla de consumo (dura)** — ☐ componentes y vistas usan **solo tokens semánticos, nunca primitivos** (referenciar un primitivo es una fuga).
- **Cobertura semántica mínima:** ☐ color/superficie · ☐ tipografía (familias · tamaños · pesos) · ☐ espaciado/rejilla · ☐ estados base (foco · deshabilitado · error).
- **Contrato de nombres semánticos** — la lista de tokens semánticos expuestos, **por nombre**: es lo que la implementación referencia. Este es el punto de encuentro con el código.
- **Origen** — ☐ propio · ☐ framework (Material/Bootstrap). Un DS ajeno vinculado que no aplica → ☐ saneado.
