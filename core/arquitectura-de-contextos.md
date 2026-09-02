# Arquitectura de contextos

**Versión:** v0.1 · **Estado:** EXPLORATORIO / en proceso · **Fecha:** 2026-08-06
**Deriva de:** puente-transferencia-hallazgos.md v0.2, puente-incorporacion.md v0.1, metodologia-sintesis.md (esquema §2b), metodologia-global.md v0.3, decisiones-consolidacion.md v0.3.
**Tier:** núcleo (`core/`), pero **no maduro** — a diferencia del resto de `core/`.

> **Aviso de madurez.** Este documento **da marco, no norma firme**. Recoge lo que ya funciona (el mecanismo de puentes) y deja marcado lo abierto (automatización, frontera de la herramienta de diseño). Es, previsiblemente, el último que se cerrará.
>
> **Qué es.** Cómo se coordinan los **contextos aislados** —hilos de conversación y herramientas— que cada uno guarda una parte del estado del proyecto, para que ese estado no se desincronice.
> **Por qué existe.** Un proceso repartido en varios contextos que **no comparten memoria** necesita un mecanismo para que ninguno opere sobre una versión desactualizada. Hoy ese mecanismo es **manual** (el humano) apoyado en **puentes documentales**.

---

## 1 · El problema

- Los contextos (hilos de conversación, herramientas) están **aislados**: no comparten memoria; lo que sabe uno no lo sabe otro.
- El **estado del proyecto vive repartido** entre ellos.
- Sin coordinación, cada contexto opera sobre una versión vieja → **desfase y deriva** (una fuente que aparenta vigencia pero ya no la tiene).
- Es un **problema reconocido del sector** (coordinación multi-instancia / memoria compartida para IA). El patrón propio —almacén Markdown en Git, acceso por conexión, registros con ciclo de vida, compuertas humanas de revisión— converge con soluciones open-source existentes. *[Según exploraste: mem0ry4ai, cognee, talamus — verificar y contrastar.]*

## 2 · Dos manifestaciones

El problema aparece en dos planos, con el mismo fondo:

- **(A) Coordinación entre hilos de trabajo** — la construcción de la metodología. Hilos con roles definidos (Corpus, Pruebas, Investigación); los hallazgos y las propuestas fluyen **hacia arriba por puentes, no lateralmente**. Es donde el mecanismo está más desarrollado.
- **(B) Coordinación de datos entre herramientas** — la ejecución del proyecto. El tier 3 vive **distribuido** (definición e implementación en el repo, diseño en su herramienta). La frontera **no volcable** es la herramienta de diseño: su tier 3 se lee por conexión al proyecto de diseño (handoff), no está en el repo.

## 3 · El mecanismo actual: puentes + sincronía humana

- **Puente:** un documento-canal por el que el estado cruza entre dos contextos, **clasificado y con estado**. Los contextos lo comparten; ninguno relee los registros crudos del otro.
- **Edición por columnas:** cada contexto es **dueño de unas columnas** (su contenido) y solo escribe esas; nunca pisa las del otro. Si un contexto discrepa de lo ajeno, no lo reescribe: lo marca y lo **devuelve**, no lo sobrescribe.
- **El humano es el punto único de sincronía:** transporta el puente entre contextos y **valida qué cruza**. Una sola copia viaja con él (el "gate humano" entre conversaciones).
- **Retorno / cierre del circuito:** el contexto receptor rellena el **estado de vuelta**. Sin retorno, el emisor mediría contra una versión desactualizada — el mismo desfase que el mecanismo evita.
- **Puentes concretos** (en `puentes/`): transferencia de hallazgos (Pruebas ↔ Metodología) e incorporación (Investigación → Corpus).

## 4 · Principios (heredados del núcleo, aplicados a contextos)

- **Autosuficiencia del cruce:** lo que cruza debe **bastar al receptor** sin acceso al historial del emisor — el mismo criterio que el contrato entre etapas (`metodologia-aplicada §6`).
- **Clasificación antes de cruzar:** nada cruza sin estar **clasificado y con destino**; si no, obligaría al receptor a rediagnosticar.
- **Registro del cruce:** qué cruzó, cuándo y con qué estado, para que sea auditable.

## 5 · Lo abierto (por qué no está maduro)

- **Automatización aparcada.** Se intentó automatizar la persistencia de puentes (conexión, Git); las credenciales no propagaron al sandbox y se volvió a la **sincronía humana manual**. Parqueado en un proyecto meta-arquitectura aparte.
- **La frontera de la herramienta de diseño.** Su tier 3 no se vuelca al repo; hoy se lee por conexión al proyecto de diseño. Cómo coordinar esa frontera de forma más robusta está **abierto**.
- **Convergencia con el sector.** Contrastar el patrón propio con las soluciones existentes (verificar nombres y encaje).
- **Estado general:** este documento da marco; las reglas firmes de coordinación se afinarán con uso — es lo menos maduro del corpus.
