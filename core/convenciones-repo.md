# Convenciones del repo

**Versión:** v0.1 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-global.md v0.4 (principio de versionado y linaje), metodologia-sintesis.md (esquema del repo).
**Ubicación:** `core/`.

> **Qué es.** Las convenciones concretas de cómo se **mantienen los documentos** del repo. El **principio** (todo se versiona, el linaje es trazable) vive en `metodologia-global`; aquí está la **mecánica**. Empieza con el versionado; puede crecer con otras convenciones (nomenclatura, estructura).

## Versionado documental

- **Cabecera obligatoria** en cada documento: **versión · estado · fecha · «Deriva de»** (con la versión exacta de cada fuente).
- **Numeración:** **MAYOR** invalida derivados; **MENOR** no; el borrador **acumula** (v0.x); la primera versión congelada es **v1.0**.
- **Estados:** `borrador` · `congelado` · `obsoleto`.
- **Desactualización:** un derivado queda **obsoleto** si una fuente subió de **MAYOR** sobre la versión que él referencia. Se comprueba en el **salto de capa** (o a petición).
