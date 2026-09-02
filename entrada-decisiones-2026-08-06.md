# Entrada de decisiones — estructuración del corpus (tiers) y proceso de la capa de diseño

**Versión:** v0.2 · **Estado:** borrador (vivo) · **Fecha:** 2026-08-06
**Deriva de:** metodologia-sintesis.md v0.2, decisiones-consolidacion.md v0.3, metodologia-claude-design.md v0.1, sesión de estructuración (hilo Corpus).

> Entrada pensada para **fundirse como bloque nuevo en `decisiones-consolidacion.md`** (siguiente letra libre, aquí **L**). Registra las decisiones cerradas en esta sesión antes de verterlas a los documentos. No sustituye a los documentos; los alimenta. Cada punto marca a qué documento(s) impacta (§ Propagación pendiente).

---

## L. Estructura del corpus y proceso de la capa de diseño

### L.1 — Arquitectura del corpus en tres tiers (refinada)

- **Tier 1 — núcleo universal (agnóstico).** Un único `metodologia-global.md`. Solo conceptos aplicables a cualquier proceso de transformación por etapas. **Prohibido** mencionar "capa", "agente" o herramienta.
- **Tier 2 — metodología aplicada a nuestro proceso.** Raíz `metodologia-aplicada.md` (las tres capas y sus roles · esquema/topología · cadena T0–T3 · coherencia cruzada del salto de la capa de definición · **protocolo común de agente/gate** · mapa de derivación) + **par por capa** (metodología + instrucciones) + **contratos entre capas**.
- **Tier 3 — datos de proyecto.** No es metodología; queda fuera del análisis. Su sitio en el esquema: **rellena los datos que las instrucciones del tier 2 dejan como variables** (definición, perfil técnico, instancias de briefing y handoff, specs rellenas, registros vivos).
- Cadena: **tier 1 → se instancia en tier 2 → se alimenta con tier 3.** El stack deja de ser caso especial: es un dato del tier 3.

### L.2 — Nomenclatura agnóstica de capas

- Los documentos de capa se nombran por **función**, no por herramienta: `capa-definicion` (era claude-ai), `capa-diseno` (era claude-design), `capa-conversion` (era claude-code-im).
- Motivo: la metodología vale para cualquier herramienta que cubra la función (p. ej., prototipado IA + diseño), no solo Claude Design.

### L.3 — Regla de partición global ↔ aplicado

- Cuando un concepto tiene **núcleo abstracto + detalle atado al proceso**, se **separan**: el núcleo va a `metodologia-global`, el detalle a `metodologia-aplicada`, con referencia cruzada.
- Aplicaciones acordadas: (a) **meta-plantilla de procedimiento** — la *forma* (contexto→alcance→requerimiento→definición→validación→registro→retorno) es global; su instancia concreta (protocolo de agente anuncia→recibe→consulta→enruta→no-cierra-con-conflicto) es aplicada. (b) **versionado** — el esquema (`Deriva de`, MAYOR/MENOR, detección de desfase) es global; la regla "comprobación solo en el salto de capa" es aplicada.
- Motivo: el tier 1 solo tiene valor si es reutilizable ante un segundo proceso; colar detalle atado lo invalida.

### L.4 — Documentos por capa: **uno solo** (metodología + procedimiento) — revisa el "dos" y corrige §G

- **Un único documento por capa**, que reúne las **reglas firmes** de la capa y su **procedimiento** (fases, gates, minigates). Se secciona internamente (reglas [firme] · procedimiento [pasos]) y mantiene los marcadores de madurez, para no perder la separación estable/operativo.
- **Por qué uno y no dos:** al extraer el **protocolo común de agente/gate** a `metodologia-aplicada` (L.5), lo que quedaba en cada capa —reglas específicas + pasos— no justifica partirse en `metodologia` + `instrucciones`; la frontera se volvía artificial y reintroducía duplicación. *(Revisa la decisión previa de "dos documentos por capa".)*
- **Corrección a `decisiones §G`:** el antiguo "tres documentos por capa" contaba metodología + instrucciones + **registro**. Ahora: **un** documento de método por capa (tier 2) + un artefacto de **registro** (tier 3, no es método).

### L.5 — Protocolo común de agente/gate → sección de `metodologia-aplicada`

- El protocolo que hoy se **duplica** literalmente en ambos `instrucciones-*` (abrir registro vacío · protocolo de gate · regla de oro · comprobar versiones en salto de capa · qué devolver al cerrar) sube a una **sección única** de `metodologia-aplicada`.
- Las instrucciones de capa quedan adelgazadas a "sigue el protocolo común + estos pasos". Mata la duplicación en su raíz.

### L.6 — Proceso de la capa de diseño: modelo de dos granos [firme el modelo; andamiaje los umbrales]

El proceso deja de ser fases globales y pasa a granos:

- **Grano app (una vez):** DS → esquema de navegación → wireframes.
- **Grano componente (bucle, uno a uno):** por componente, **WF → HF → spec** (referencia al DS). Se cierra el componente antes de pasar al siguiente.
- **Grano vista (bucle, cuando hay componentes suficientes):** montar con componentes ya spec'd → HF de vista → spec de vista **si la requiere**.
- **Cierre:** prototipo navegable → **gate visual** → handoff.
- **[ANDAMIAJE]** (por validar, sin fosilizar): umbrales de cambio de grano, de dónde sale el WF dentro del bucle de componente, si toda vista genera spec.

### L.7 — Orden HF → spec dentro del grano de componente (supersede sintético §3 / §A)

- La spec se produce **después** del HF de su componente (no antes). **Supersede** la decisión deliberada "especificaciones (T2.3) antes que alta fidelidad (T2.4)" de `metodologia-sintesis §3` y `decisiones §A`.
- **Alcance de la supersesión (no es total):** "estructura/función antes que píxeles" **se conserva en el grano app** (esquema de navegación + wireframes preceden a cualquier HF); se **invierte solo en el grano componente**, donde el HF precede a la spec.
- Motivo: la spec recoge así valores visuales ya asentados → **elimina el "Spec visual: pendiente"** que forzó a la conversión a reconstruir apariencia a ojo (causa estructural de C/D).
- Decisión consciente y registrada (se avisó de que revertía una decisión previa; el usuario la tomó a propósito).

### L.8 — Reglas firmes del proceso de diseño [RESPALDADO]

1. **DS-first + referencia.** El DS se consolida **antes** que los componentes; los componentes lo **referencian** (ideal por defecto). Al generar un DS, se revisa contra un alcance mínimo, o se sustituye por el de un framework (Material/Bootstrap).
2. **Spec después del HF** (consecuencia del grano de componente, L.7).
3. **Ninguna vista incluye componentes sin spec.** Regla única que sustituye a todos los umbrales de orquestación y garantiza que nada llega a conversión sin especificar.

### L.9 — Gobierno de divergencia del DS (refina; retira la "regla dura" transitoria)

- El invariante **no** es "los componentes no amplían el DS"; es **"no hay divergencia silenciosa"**. Toda divergencia es decisión **clasificada y registrada**:
  - Aporte **general** (p. ej. token semántico reutilizable) → **amplía el DS** (`hueco`: el sistema crece).
  - Regla **específica** del componente que no debe subir a estilos de app → **vive local en el componente** (`excepción`: override marcado).
- Es el **gobierno del DS ante conflicto** de `metodologia-capa-diseno §5` aplicado *dentro* de la capa, y encaja fractalmente con la regla 3.3 (toda decisión que actualiza lo de arriba se registra/propaga): el DS hace de "capa superior" del componente.
- Lo único firme es el **registro**; ampliar o localizar son ambas legítimas.
- **[ABIERTO, sugerencia no adoptada]** sesgo "quedarse local hasta que un segundo uso pruebe que es general" (mismo principio de no fosilizar lo observado una vez).

### L.10 — Taxonomía de artefactos de especificación: dos plantillas + una hoja de requisitos

- **Plantillas** (molde, se rellenan por instancia → producen tier 3):
  - **Spec de componente** (átomo): nombre · función · elemento nativo · import/export · representación HF de estados · propiedades declaradas · tokens que lo constituyen · referencia al DS. *(Campos a afinar.)*
  - **Spec de vista** (compone): **referencia** specs de componente con su variante/props · estados propios de vista · navegación entrada/salida · layout. **No re-declara** componentes.
- **Hoja de requisitos de app** (norma, **no** es un spec — nombre acordado, deja de llamarse "spec de app"): ver L.12.
- Las plantillas pertenecen a la **metodología/proceso de `capa-diseno`** (tier 2), no al contrato. El contrato de handoff **exige** las specs rellenas como input; no las contiene como plantilla.

### L.11 — Anidamiento de specs

- **app → vistas → componentes → DS.** Cada nivel referencia hacia abajo; ninguno duplica lo del nivel inferior.

### L.12 — Hoja de requisitos de app: alcance y doble función

- **No es un molde**, es una **hoja normativa**: fija qué deben cumplir los documentos globales que definen técnicamente la app — **alcance mínimo del DS**, requisitos del **esquema de navegación**, **listado de componentes**, y el **ámbito compartido técnico↔diseño**. Es el DoD/contrato de los artefactos globales de la capa; se sitúa **aguas arriba** del handoff (garantiza que los docs globales estén completos antes de que el handoff los transporte).
- **Ámbito compartido técnico↔diseño (apunte de la sesión):** la ficha técnica no es solo del perfil técnico de claude-ai; hay decisiones que son a la vez técnicas y de diseño (app móvil/híbrida, breakpoints de media query mobile/tablet/desktop…). La hoja es su hogar y cumple **doble función**:
  - **(a)** registrar **decisiones de diseño globales de la app** que no viven en ningún otro documento;
  - **(b)** registrar **decisiones técnicas que afectan al diseño** para **propagarlas aguas arriba** (a perfil técnico / definición en claude-ai).
- Es, por tanto, un **nodo de registro y propagación**, no solo un auditor de documentos heredados. Coherente con el principio de gobierno (las decisiones de requisito/alcance suben a claude-ai) y con el tratamiento de deriva inversa.

### L.13 — Arquitectura de tokens en dos capas + regla de consumo  [firme la regla; andamiaje la profundidad]

- El DS separa **tokens primitivos** (valores crudos: paleta, escala) de **tokens semánticos** (nombran un uso: superficie, primario, espaciado-m). Habilita rebranding/tematización remapeando lo semántico **sin tocar los componentes**.
- **Regla de consumo (dura):** componentes y vistas usan **solo tokens semánticos, nunca primitivos** — referenciar un primitivo es una fuga. Afina la regla de conversión "ningún componente declara sus propios tokens" → "consume solo semánticos".
- **Cobertura semántica mínima** (exigida en la hoja de requisitos de app §1): color/superficie · tipografía · espaciado/rejilla · estados base. La **profundidad** escala con el proyecto; la **regla de consumo** es dura siempre.
- Un DS de framework (Material 3) ya trae la capa semántica; uno propio hay que autorarla.
- **Reemplaza** la postura anterior del corpus —tokens semánticos "solo si se anticipa una capa de marca futura" (metodologia-claude-code-im §5, T3.2)—: pasan a ser **por defecto**.
- **Origen:** revisión de la hoja de requisitos de app; conecta con el `_semantic-tokens.scss` creado vacío y el sistema de tokens solo-color detectado en las pruebas.
- **Aplicado ya esta sesión:** hoja de requisitos de app §1 (v0.2) y ficha de componente §5 (v1.1). Pendiente: metodologías de capa (ver propagación).

---

## Madurez de lo anterior

- **Firme (respaldado / decisión de método tomada):** L.1–L.5 (estructura y nomenclatura), L.6 el *modelo* de dos granos, L.7, L.8, L.9 el *invariante de registro*, L.10–L.12 la taxonomía, L.13 las dos capas de tokens + la regla de consumo.
- **Andamiaje (por validar en generación limpia):** los umbrales de cambio de grano (L.6), el sesgo general-vs-local (L.9), los campos exactos de cada plantilla (L.10), el listado exacto de requisitos de la hoja de app (L.12), la profundidad/cobertura semántica exacta (L.13).

## Propagación pendiente (qué documento toca cada decisión)

| Decisión | Documento(s) a tocar | Acción |
|---|---|---|
| L.1, L.2 | (nuevos) `metodologia-global`, `metodologia-aplicada`; renombrar carpetas de capa | crear / partir el sintético |
| L.3 | `metodologia-global` + `metodologia-aplicada` | repartir meta-plantilla y versionado |
| L.4 | `decisiones-consolidacion §G` | corregir el "tres documentos por capa" |
| L.5 | `metodologia-aplicada` + ambos `instrucciones-*` | subir el protocolo común; adelgazar instrucciones |
| L.6, L.7, L.8 | `metodologia-capa-diseno §2–§4`, `instrucciones-capa-diseno §1`, `metodologia-sintesis §3` | reescribir el proceso a dos granos; corregir orden T2.3/T2.4 |
| L.9 | `metodologia-capa-diseno §5 + §3` | reformular la regla del DS (registro, no prohibición) |
| L.10, L.11, L.12 | `metodologia-capa-diseno §4` (nuevo bloque de artefactos de spec) | definir plantillas + hoja de requisitos |
| L.13 | hoja-requisitos-app §1 ✓ · ficha-componente §5 ✓ (hechos) · `metodologia-capa-diseno` + `metodologia-capa-conversion` (regla de tokens) | reflejar dos capas + consumo solo-semántico en las metodologías de capa |

> **Contradicción viva a resolver al propagar:** `metodologia-sintesis §3` aún afirma "especificaciones antes que alta fidelidad". Hasta que se propague L.7, el sintético queda contradictorio con esta entrada. Marcado para no dejarlo como deriva silenciosa.
