# Metodología — esquema del sistema

**Versión:** v0.11 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-sintesis.md v0.2 (reencuadrado de "andamio de borrador" a "mapa del sistema"), entrada-decisiones-2026-08-06.md (bloque L), plantillas de spec (componente v1.1, vista v1.0, hoja de requisitos de app v1.0).

> **Qué es.** El **mapa de todo el sistema** en un solo documento: para verlo de un vistazo, **comparar** las fases de cada capa y **ubicar** cada documento. No es la norma detallada —esa vive en `metodologia-global`, `metodologia-aplicada` y las metodologías de capa—; este documento **orienta y organiza**.
> **Estado del modelo.** Refleja el orden vigente (dos granos en diseño, **HF → spec** dentro del grano de componente). Lo que sigue como **andamiaje** va marcado.

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
repo-de-codigo/                            # el repo del proyecto: código + documentación
├── MP4AI/                                 # raíz de documentación del proyecto (todos los niveles)
│   ├── metodologia-sintesis.md            ← este esquema (mapa de entrada)
│   │
│   ├── core/                              # Tier 1 · universal, agnóstico
│   │   ├── metodologia-global.md
│   │   └── arquitectura-de-contextos.md   # exploratorio, no maduro
│   │
│   ├── domain/                           # Tier 2 · metodología aplicada a este proceso
│   │   ├── metodologia-aplicada.md        # raíz: capas · cadena T · protocolo común de agente/gate · derivación
│   │   ├── capa-definicion/
│   │   │   ├── metodologia-capa-definicion.md     # metodología + procedimiento: qué conversaciones abrir (placeholder)
│   │   │   ├── docs/                              # tier 3 · documentos generados: alcance · entidades · historias · requisitos + briefing + perfil-técnico
│   │   │   └── registro.md                        # registro de actividad de la capa
│   │   ├── capa-diseno/                           # tier 3 NO volcable: DS · specs · prototipo · handoff · registro viven en la herramienta de diseño
│   │   │   ├── metodologia-capa-diseno.md         # metodología + procedimiento
│   │   │   └── spec/                              # plantillas de spec (moldes) — lo único que el repo guarda de esta capa
│   │   │       ├── plantilla-spec-componente.md
│   │   │       ├── plantilla-spec-vista.md
│   │   │       └── plantilla-hoja-requisitos-app.md
│   │   ├── capa-conversion/
│   │   │   ├── metodologia-capa-conversion.md     # dirección im (ex pendiente)
│   │   │   ├── registro.md                        # registro de actividad
│   │   │   └── informe-final.md                   # informe final de conversión
│   │   └── contratos/                             # contratos entre capas (moldes)
│   │       ├── contrato-definicion-diseno.md      # puente definición → diseño · briefing
│   │       ├── contrato-definicion-conversion.md  # puente definición → conversión · perfil técnico (crece desde conversión)
│   │       └── contrato-diseno-conversion.md      # puente diseño → conversión · handoff
│   │
│   └── puentes/                          # coordinación entre hilos/contextos
│       └── (puente-transferencia-hallazgos · puente-incorporacion · …)
│
├── src/ · …                              # el código de la aplicación
└── CLAUDE.md                             # apunta al perfil técnico en capa-definicion/docs/
```

- **`MP4AI/` es el repo del proyecto** (por proyecto, de momento), anidado en el repo de código como **raíz de documentación a todos los niveles**: un agente encuentra aquí las fuentes que necesite.
- La **metodología** (`core/` + los `metodologia-*.md` + los moldes de `spec/` y `contratos/`) es el **esqueleto heredable** que se copia al arrancar un proyecto; `docs/`, `registro` e `informe` **nacen vacíos** y se rellenan.
- Al vivir dentro del repo de código, el **perfil técnico**, el **registro de conversión** y el **informe** ya están aquí. La única pieza externa es el **tier 3 de diseño** (en su herramienta).

## 2b · Dónde viven los datos de proyecto (tier 3)

Como `MP4AI/` vive **dentro del repo de código**, casi todo el tier 3 queda documentado en el repo; solo el de diseño queda fuera:

- **Definición:** los documentos que genera cada hilo (alcance · entidades · historias · requisitos) + el **briefing** + el **perfil técnico** se guardan en `capa-definicion/docs/`, con su `registro`.
- **Diseño:** todo se genera **dentro de la herramienta de diseño** y no hay forma de volcarlo al repo. En el repo solo viven **metodología + plantillas**; DS, specs rellenas, prototipo, handoff y registro **permanecen en la herramienta de diseño**.
- **Conversión:** no genera documentos de definición; su **registro de actividad** e **informe final** viven en `capa-conversion/` (dentro del repo), junto al código y al perfil técnico, que crece aquí.

> El tier 3 queda **local a cada capa**, y como el repo es del proyecto, casi todo está documentado en él. Lo único no volcable —el diseño— se queda en su herramienta; coordinar esa frontera es el cometido de `arquitectura-de-contextos`.

---

## 3 · Las tres capas y sus fases

### 3a · Secuencia interna de cada capa

**Definición** — *columnas en paralelo*, con cascada interna en cada una; convergen en el salto de capa:
research · definición · análisis funcional · entidades · historias de usuario · arquitectura de información · requisitos · perfil técnico.

**Diseño** — *modelo de dos granos*:
- **Grano app** (una vez): DS → esquema de navegación → wireframes.
- **Grano componente** (bucle): WF → HF → **spec**.
- **Grano vista** (bucle): montar con componentes ya spec'd → HF de vista → spec de vista si la requiere.
- **Cierre**: prototipo navegable → handoff.

> En diseño **cada fase** lleva su **revisión visual** implícita (el humano ve la propuesta, ajusta y valida antes de pasar): el gate visual es **continuo y nativo**, no una parada final.

**Conversión (im, diseño→código)** — *cascada*:
T3.1 informe-inventario → T3.2 estilos/tokens → T3.3 shared + shell → T3.4 páginas → T3.5 routing.

### 3b · Comparación

| Dimensión | Definición | Diseño | Conversión |
|---|---|---|---|
| **Topología** | columnas paralelas | granos (app + bucles) | cascada |
| **Unidad de avance** | columna | componente / vista | vista / artefacto |
| **Parada de cierre** | salto de capa (+ coherencia cruzada) | handoff (gate visual continuo, en cada fase) | gate visual por render + DoD |
| **Qué baja** | definición · briefing · perfil técnico | maqueta navegable · paquete de handoff | código · registro |
| **Modo de fallo dominante** | incoherencia (entre columnas) | contrabando / deriva | contrabando / deriva |

> **Dos gates visuales, no el mismo.** En **diseño** es **continuo y nativo**: en cada fase el humano ve la propuesta, ajusta y valida antes de pasar. En **conversión** el agente es **ciego**, así que debe **renderizar y comparar** al cerrar (navegador / pixel-diff) — el gate que la Prueba C mostró imprescindible. La asimetría es el punto: diseño lo tiene en todas partes por naturaleza; conversión no lo tiene en ninguna hasta fabricarlo. Detalle en `metodologia-capa-diseno §7` y `metodologia-capa-conversion §6`.

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
- **Definición → Conversión:** el **perfil técnico** (ficha técnica) — baja al repo de código y **crece desde la conversión** (bidireccional: los cambios técnicos con impacto propagan aguas arriba; es donde se origina el ámbito compartido técnico↔diseño).
- **Diseño → Conversión:** el **handoff** — el **paquete ampliado** (specs rellenas de componente/vista + hoja de requisitos de app + extras: mapeo a nativo, rutas, trazabilidad, reglas globales). La conversión lo **lee conectándose** al proyecto de diseño (o de una copia congelada en el repo) y con él **conecta todos los documentos de diseño** y se orienta. No está listo hasta que la hoja de requisitos de app está completa.

---

## 7 · La cadena completa, de un vistazo

**Definición** (columnas en paralelo) → **T1** → **Diseño** (dos granos) → **salto de capa** → **Conversión** (T3.1–T3.5) → **código**.

- **Bidireccional** (diseño↔código): `im` (diseño→código) y `ex` (código→diseño, pendiente).
- **T0 (reenganche):** importar diseño existente como origen alternativo del grano app; se mide aparte de la generación de código.

---

## Andamiaje (por validar en generación limpia)

- Los **umbrales de cambio de grano** en diseño (cuántos componentes antes de montar una vista, si toda vista genera spec).
- La capa de **definición**, poco desarrollada.
- La dirección **`ex`** (código→diseño) y **T0**.
