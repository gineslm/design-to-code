# spec-entidades — modelo de datos

**Versión:** v0.1 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** spec-vision-general.md v0.1 (§3, hueco de datos), metodologia-capa-diseno.md v0.22.
**Tier:** 2 (capa `diseno`) · **Clase:** molde (una entrada por entidad).

> **Qué es.** Documenta el **modelo de datos** que la app maneja (entidades, campos, relaciones). **Nace en la capa de definición** (entidades, historias de usuario); no es una decisión de diseño, es **dato heredado que se registra** aquí para que la implementación tipe y modele, y para que las specs de vista y componente lo **referencien donde lo usan**.

## Por cada entidad
- **Nombre** — *ej.: «Cita».*
- **Campos** — una fila por campo: nombre · tipo · obligatorio. *Ej.: «fecha · fecha-hora · sí».*
- **Relaciones** — con qué otras entidades y de qué tipo. *Ej.: «pertenece a un Paciente».*
- **Notas de dominio** — reglas relevantes que la implementación debe respetar. *Ej.: regla clínica: metadatos neutros, sin interpretar resultados.*

> Las fichas de **vista** y **componente** referencian a estas entidades donde muestran sus datos; no repiten el modelo, lo citan.
