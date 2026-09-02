# Metodología — esquema del sistema

**Versión:** v0.12 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-sintesis.md v0.2 (reencuadrado a mapa del sistema), decisiones-consolidacion.md v0.5 (bloque L), specs de la capa de diseño (`spec-*`).

> **Qué es.** El **mapa de todo el sistema** en un solo documento: para verlo de un vistazo, **comparar** las fases de cada capa y **ubicar** cada documento. No es la norma detallada —esa vive en `metodologia-global`, `metodologia-aplicada` y las metodologías de capa—; este documento **orienta y organiza**.
> **Estado del modelo.** Refleja el orden vigente (fases en diseño, **HF → spec** dentro de la fase de componentes). Lo que sigue como **andamiaje** va marcado.

---

## 1 · Los tres tiers

| Tier | Qué es | Es metodología |
|---|---|---|
| **1 · Global** | Núcleo universal, agnóstico de proceso y herramienta. | Sí |
| **2 · Aplicada** | La metodología instanciada en *este* proceso (diseño→código, tres capas). | Sí |
| **3 · Proyecto** | Los datos que rellenan las instrucciones del tier 2. | **No** (datos) |

Cadena: **tier 1 → se instancia en tier 2 → se alimenta con tier 3.**

---

## 2 · Mapa de documentos (estructura de carpetas)

```
design-to-code/                         # repo de metodología (corpus MP4AI)
├── core/                               # universal + visión general
│   ├── metodologia-global.md           # núcleo agnóstico
│   ├── metodologia-aplicada.md         # visión general de las tres capas
│   ├── arquitectura-de-contextos.md    # exploratorio, no maduro
│   └── convenciones-repo.md            # versionado por documento
├── domain/                             # operativo por capa
│   └── capa-diseno/
│       ├── metodologia-capa-diseno.md  # metodología + procedimiento
│       ├── fases-proceso-diseno.md     # listado de fases (F1–F6)
│       └── spec/                       # sistema de especificaciones
│           ├── spec-vision-general.md  # índice
│           ├── spec-app.md · spec-ds.md · spec-navegacion.md
│           └── spec-entidades.md · spec-vista.md · spec-componente.md
│   (capa-definicion/ y capa-conversion/ · pendientes)
├── metodologia-sintesis.md             ← este esquema (mapa de entrada)
├── decisiones-consolidacion.md         # estado maestro de decisiones
├── entrada-decisiones-2026-08-06.md
├── CONTEXT_GIT.md                      # versionado por Git (R-00X)
└── README.md
```

- **`core/`** universal + visión general · **`domain/`** operativo por capa.
- **Pendiente de subir:** `capa-definicion/`, `capa-conversion/`, los `contratos/` (briefing · perfil técnico · handoff) y los `puentes/`.
- **Abierto (L.16):** hoy es un **repo de metodología independiente**. La idea previa era *MP4AI dentro del repo de código, por proyecto*. Reconciliar: ¿`design-to-code` es el **corpus reutilizable** (tier 3 en repos de proyecto/herramientas) o el repo **de un proyecto** (tier 3 aquí, por capa)? De eso depende §2b.

## 2b · Dónde viven los datos de proyecto (tier 3)

El tier 3 queda **local a cada capa**; **dónde** reside físicamente depende de la decisión abierta (L.16):

- **Definición:** documentos generados (alcance · entidades · historias · requisitos) + briefing + perfil técnico, con su registro.
- **Diseño:** todo se genera **en la herramienta de diseño** y no se vuelca al repo (DS · specs rellenas · prototipo · handoff · registro). El repo solo guarda **metodología + specs (moldes)**.
- **Implementación:** registro de actividad + informe final, junto al código.

> Lo no volcable —el diseño— se queda en su herramienta; coordinar esa frontera es el cometido de `arquitectura-de-contextos`.

---

## 3 · Las tres capas y sus fases

### 3a · Secuencia interna de cada capa

**Definición** — *columnas en paralelo*, con cascada interna en cada una; convergen en el salto de capa:
research · definición · análisis funcional · entidades · historias de usuario · arquitectura de información · requisitos · perfil técnico.

**Diseño** — *organizado en fases*:
- **Fase app** (una vez): DS → esquema de navegación → wireframes.
- **Fase componentes** (tareas iterativas): por componente, WF → HF → **spec**.
- **Fase vistas** (tareas iterativas): montar con componentes ya spec'd → HF de vista → spec de vista si la requiere.
- **Cierre**: prototipo navegable → handoff.

> En diseño **cada fase** lleva su **revisión visual** implícita (el humano ve la propuesta, ajusta y valida antes de pasar): el gate visual es **continuo y nativo**, no una parada final.

**Implementación (im, diseño→código)** — *cascada*:
T3.1 informe-inventario → T3.2 estilos/tokens → T3.3 shared + shell → T3.4 páginas → T3.5 routing.

### 3b · Comparación

| Dimensión | Definición | Diseño | Implementación |
|---|---|---|---|
| **Topología** | columnas paralelas | fases (app + bucles iterativos) | cascada |
| **Unidad de avance** | columna | componente / vista | vista / artefacto |
| **Parada de cierre** | salto de capa (+ coherencia cruzada) | handoff (gate visual continuo, en cada fase) | gate visual por render + DoD |
| **Qué baja** | definición · briefing · perfil técnico | maqueta navegable · paquete de handoff | código · registro |
| **Modo de fallo dominante** | incoherencia (entre columnas) | contrabando / deriva | contrabando / deriva |

> **Dos gates visuales, no el mismo.** En **diseño** es **continuo y nativo**: en cada fase el humano ve la propuesta, ajusta y valida antes de pasar. En **implementación** el agente es **ciego**, así que debe **renderizar y comparar** al cerrar (navegador / pixel-diff) — el gate que la Prueba C mostró imprescindible. La asimetría es el punto: diseño lo tiene en todas partes por naturaleza; implementación no lo tiene en ninguna hasta fabricarlo. Detalle en `metodologia-capa-diseno §7` y `metodologia-capa-conversion §6`.

---

## 4 · Niveles de parada

- **minigate** — tarea dentro de una transición · **gate** — cierre de una transición · **salto de capa** — gate reforzado que pasa a la capa siguiente.
- **Validación humana en todas.**
- **Comprobación de versiones:** solo en el **salto de capa**.
- **Coherencia cruzada:** solo en el salto de la capa de **definición** (por su paralelismo).

---

## 5 · Modos de fallo

- **Contrabando** — aparece algo que ninguna etapa autorizó.
- **Deriva** — se pierde o contradice algo ya cerrado.
- **Incoherencia** — dos piezas definidas en paralelo no encajan.
- Lo que separa **contrabando bueno** de **deuda silenciosa**: si queda **registrado**.

---

## 6 · Contratos entre capas

Tres flujos, no dos:
- **Definición → Diseño:** el **briefing** — qué debe hacer diseño en cada paso.
- **Definición → Implementación:** el **perfil técnico** (ficha técnica) — baja al repo de código y **crece desde la implementación** (bidireccional: los cambios técnicos con impacto propagan aguas arriba; es donde se origina el ámbito compartido técnico↔diseño).
- **Diseño → Implementación:** el **handoff** — el **paquete ampliado** (specs rellenas de componente/vista + spec-app + extras: mapeo a nativo, rutas, trazabilidad, reglas globales). La implementación lo **lee conectándose** al proyecto de diseño (o de una copia congelada en el repo) y con él **conecta todos los documentos de diseño** y se orienta. No está listo hasta que spec-app está completa.

---

## 7 · La cadena completa, de un vistazo

**Definición** (columnas en paralelo) → **T1** → **Diseño** (fases) → **salto de capa** → **Implementación** (T3.1–T3.5) → **código**.

- **Bidireccional** (diseño↔código): `im` (diseño→código) y `ex` (código→diseño, pendiente).
- **T0 (reenganche):** importar diseño existente como origen alternativo de la fase app; se mide aparte de la generación de código.

---

## Andamiaje (por validar en generación limpia)

- Los **umbrales de cambio de fase** en diseño (cuántos componentes antes de montar una vista, si toda vista genera spec).
- La capa de **definición**, poco desarrollada.
- La dirección **`ex`** (código→diseño) y **T0**.
