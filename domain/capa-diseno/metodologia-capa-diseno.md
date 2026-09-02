# Metodología — capa de diseño

**Versión:** v0.23 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-capa-diseno.md v0.21 (remapeo de términos: tarea→fase, subpaso→tarea; fuera "grano/granularidad"), metodologia-aplicada.md v0.4, metodologia-global.md v0.4, entrada-decisiones-2026-08-06.md (L.6–L.13), plantillas de spec (componente v0.6, vista v0.2, hoja de requisitos de app v0.3), fases-proceso-diseno.md v0.1 (listado ejecutable).
**Tier:** 2 (capa `diseno`). Transversal y agnóstico de herramienta.

---

## 1 · Qué es y a qué pertenece

Este documento forma parte de un **proceso de desarrollo de aplicaciones web asistido por IA**. El proceso tiene tres capas: primero se **define** el proyecto (qué se construye y con qué restricciones), luego se **diseña** su forma visual, y por último se **implementa** en código. Este documento contiene la **metodología** de la capa intermedia: la **definición visual del proyecto** — su prototipado y diseño.

Esta capa **se nutre** de la capa de definición y **continúa** en la de implementación. Su trabajo es convertir la definición en forma visual (sistema de diseño, wireframes, componentes, vistas y prototipo navegable) y dejarla lista para implementar.

Las **transiciones** entre capas se rigen por **contratos** —qué debe transferirse de una a la siguiente— que se detallan más adelante. Todo el trabajo lleva un **registro** de las decisiones que se van tomando.

**Cómo usar este documento:** léelo **entero** primero — es el método completo de la capa. Después ejecuta el proceso **fase a fase** con el documento de fases (`fases-proceso-diseno`), que es la lista ordenada y numerada. Esta capa **no decide requisitos**: da forma visual a lo que la definición ya fijó (cómo se gobierna esa frontera, en §2).

**Si necesitas más** (no hace falta para operar, solo para el porqué o el detalle; así sabes qué pedir):
- Los **conceptos de fondo** (trazabilidad, modos de fallo, madurez) → documento de metodología general.
- La **vista de conjunto** de las tres capas y sus contratos → esquema del sistema.
- Las **plantillas** que rellenas aquí (componente · vista · requisitos de la aplicación) → carpeta `spec/`.
- El **qué específico de este proyecto** (pantallas, entidades, reglas) → el briefing de definición.

---

## 2 · Reglas del método

> Lo que debe cumplirse **siempre** en esta capa, independientemente de la fase.

### Contratos (qué entra, qué sale)
- **Entra:** la definición del proyecto + el **briefing** + este documento + el documento de fases.
- **Sale:** la **maqueta navegable aprobada** + el **paquete de entrega** (el *handoff*) con los extras que exige su contrato.
- **Criterio:** el paquete transporta el **resultado final consolidado**: **todo lo que especifican las specs** (la carpeta `spec/`; ver su índice `spec-vision-general`): DS, navegación, datos, componentes, vistas y requisitos globales; no el camino para llegar a él. Quien lo recibe en la capa de implementación trabaja en **contexto limpio** —no ha visto esta conversación— y solo puede aplicar lo que esté **escrito en el paquete**; por eso todo lo que forme parte del resultado debe estar volcado en él antes de entregar.

### Realización con la herramienta  *[específico]*
> Lo anterior es agnóstico de herramienta. Esto describe **cómo se materializa** con la herramienta actual; es lo que cambiaría al cambiar de herramienta. El detalle completo del contrato de salida vive en su contrato de handoff.

- **Entrada.** El briefing se genera en la capa de definición (Claude AI) y se **importa al proyecto de Claude Design**. Junto a él se importan **este documento**, **el documento de fases** y **las specs**.
- **Almacén.** Todo lo que se produce (DS, wireframes, alta fidelidad, fichas, prototipo) vive **dentro de Claude Design** y **no se extrae al repo**.
- **Salida.** La capa de implementación (Claude Code) accede a esos archivos por un **servidor MCP**, que lee un **handoff nativo** (lo que Claude Design entrega por defecto). Además, su procedimiento incluye **buscar un handoff ampliado** con los extras del contrato e instrucciones para manejar las specs y la información del proyecto de diseño.

### Normas de la capa
- **El proceso sigue este mapa** (esta norma señala dónde vive cada regla; no la repite):
  - El trabajo se organiza en **fases ordenadas** — listado en `fases-proceso-diseno`; el porqué del orden, en §3.
  - Cómo se **conduce** cada fase (y se calculan sus tareas) y qué hacer ante una **discrepancia** u observación → §4 (ciclo de vida).
  - Cuando una fase posterior obliga a **revisar una anterior ya cerrada** → **retroactividad**, §4.
- **Divergencia gobernada.** No se prohíbe ampliar el DS; se prohíbe **divergir en silencio**. Aporte general → amplía el DS; regla específica → vive local en el componente; siempre registrada y clasificada.
- **Las specs marcan los requisitos y el alcance.** Las **specs** (la carpeta `spec/`, con su índice `spec-vision-general`) definen los requisitos y el alcance mínimo: app, DS, navegación, datos, cada vista y cada componente. Rellenarlas por completo (**sin nada "pendiente"**) es condición para validar el contrato de salida. Lo que ellas ya exigen no se repite en estas normas.
- **Estructura y roles de archivos** — cada archivo declara su rol; la **taxonomía de roles** y la regla las define **`spec-app` (§2)**, con el documento de trazabilidad como clasificación concreta.
- **El handoff lo produce esta capa**, no la de implementación.
- **Reparto nativo / instruir.** La herramienta hace unas cosas de fábrica y otras no; el método reparte el trabajo según eso, para no rehacer lo que ya existe ni dar por hecho lo que no:
  - **Nativo — se invoca** (la herramienta lo hace sola, solo hay que activarlo): aplicar el DS, guardar reglas permanentes del proyecto, parametrizar lo que se repite.
  - **No nativo — se instruye** (no ocurre por defecto, hay que pedirlo): extraer patrones repetidos como componentes, montar el prototipo navegable, llevar la trazabilidad, generar el handoff con sus extras.
  - **Sanear:** si hay un DS ajeno vinculado que no es el del proyecto, neutralizarlo explícitamente, o se cuela.

### Registro
Es el **relato exhaustivo** del trabajo de la capa, y sirve para la **trazabilidad**: qué se decidió, **por qué**, y qué se evaluó y descartó. Incluye los **pasos intermedios** (iteraciones de wireframe, estructuras probadas y cambiadas), las **desviaciones del briefing**, los **huecos marcados** y las **divergencias del DS**. Se **abre vacío** al empezar la capa, se anota **en el momento** (no reconstruido al final) y se **reconcilia** contra el briefing al cerrar. A diferencia del paquete de entrega —que lleva solo el resultado—, en el registro **sí está todo**. No es nativo de la herramienta; se instruye.

> **TO-DO abierto — edición manual sin rastro.** El registro captura bien lo que pasa **por el agente** (vía prompt). Pero la herramienta permite **crear y editar elementos a mano** en su vista de diseño, y esa edición **no pasa por el agente**, dejando un **vacío en el registro**. Es el mismo problema que la edición directa de código en implementación. No se resuelve aquí (mecánica de la herramienta + arquitectura de contextos); está anotado en el registro maestro de pendientes. El método lo **acota** confinando la edición manual a la fase de alta fidelidad, pero solo la **disciplina del usuario** lo cierra.

### Gobierno de decisiones
Cuando durante el diseño surge algo que la definición no dejó resuelto, hay **dos caminos** según de qué se trate:

- **Decisión de requisito o alcance** (contradice la definición, o ella no lo previó): **no se resuelve aquí**; se devuelve a la capa de definición para que lo decida quien tiene esa responsabilidad.
- **Decisión propia del diseño**: se **resuelve aquí**, pero se **registra** y se **propaga a la capa de definición** de la que deriva. Sin ese registro y esa propagación, la definición queda como un fósil que aparenta vigencia.

Así el registro, la trazabilidad y la actualización se mantienen coherentes entre las capas del proyecto.

### Gate visual continuo
El humano **ve** el resultado. Por eso el gate visual es **continuo**: cada fase lleva revisión visual → ajuste → validación antes de pasar. No es una parada al final.

---

## 3 · Proceso

El proceso de esta capa es una **secuencia ordenada de fases**, no un conjunto. El orden no es arbitrario: cada fase **incrementa la definición del objetivo** sobre lo que dejó la anterior — el DS habilita los componentes, los componentes habilitan las vistas. Es el enriquecimiento acumulativo aplicado a la secuencia, y es lo que obliga a que las fases vayan **numeradas**.

Cada fase se resuelve con **una o varias tareas** —únicas, en cascada o **iterativas** (p. ej. una tarea por componente)—. **Cuántas tareas tiene una fase no se define aquí:** depende de la complejidad y las decisiones del proyecto (tier 3), y se **calcula al abrir la fase**, dentro de su ciclo de vida (§4). Lo fijo es el **objetivo de cada fase**, que es donde está su **gate**.

*[hipótesis: el modelo de fases y su secuencia están por validar en generación limpia.]*

### El listado de fases
El **listado ejecutable** —las fases numeradas y ordenadas, cada una con su plantilla (nombre · objetivo · resultado · requisitos de entrada · recomendaciones · verificación)— vive en el documento **`fases-proceso-diseno`**. Aquí se describe el proceso; allí se ejecuta. Todo lo que hable *sobre* el proceso está en esta sección; el documento de fases contiene **solo** el listado.

---

## 4 · Cómo trabaja el agente

> Cómo el agente **conduce** cada fase del proceso (§3). Se apoya en las fases ya definidas; no las redefine.

### Vocabulario: proceso · fase · tarea · gate
- **Proceso** — la secuencia completa de **fases** de la capa (§3).
- **Fase** — cada bloque del proceso, con su **objetivo** y su **gate**. Se resuelve con una o varias tareas.
- **Tarea** — cada **acción validable** dentro de una fase. Cuántas hay depende del proyecto (tier 3); pueden ser únicas, en cascada o iterativas.
- **Gate** — el **paso adelante** al **cerrar una fase**: **valida y registra**. Reforzado si es cambio de capa (comprueba versiones y coherencia).
- En una frase: *el proceso se divide en fases; cada fase se resuelve con una o varias tareas; y cada gate es el cierre de una fase, con validación y registro.*

### Ciclo de vida de una fase
Hay **dos checkpoints ligeros** (sin registro) y **un gate** (con registro, al cerrar la fase).

**Apertura — calcular y validar el plan** *(antes de ejecutar nada; sin registro)*
1. **Entra:** lee la fase (objetivo, requisitos) y revisa la documentación e itinerarios.
2. **Anuncia y pregunta:** dice qué va a hacer; si tiene dudas, las lanza **ahora**.
3. **Expone la hoja de ruta:** **calcula las tareas** de la fase para este proyecto (una única, en cascada o iterativas, según complejidad y decisiones) y las lista como plan a validar. Cada tarea = **una sola acción validable**.
4. **Checkpoint del plan:** el usuario lee, pregunta o corrige. El agente **no ejecuta hasta que el usuario valida el plan** — así no se gastan tokens en un camino equivocado. *(No es un gate: no se registra. Si el plan se replantea a media fase, registrar el plan viejo sería registrar algo que ya no existe.)*

**Ejecución — tarea a tarea** *(sin registro)*
5. Por cada tarea: la resuelve, **explica cómo la resolvió** y **propone qué comprobar** en ese punto.
6. El usuario confirma (habiendo corregido o no) o pide ajuste; se itera hasta el ok.

**Cierre — el gate** *(con registro)*
7. Con todas las tareas validadas y el **objetivo de la fase cumplido**, se alcanza el **gate de la fase**: validación final + **registro consolidado** (con visión de conjunto de lo que pasó y lo relevante) + transición a la siguiente. Reforzado si es cambio de capa.

> **El registro es al cerrar la fase**, no en cada iteración de plan o tarea: es cuando hay visión de conjunto. La unidad del registro es la **fase**.

**Regla de oro:** lo no cubierto por el método ni por el briefing se **registra como hueco y se pregunta**; decidir en silencio es contrabando. **Versiones:** se comprueban solo al **cerrar la capa** (salto a implementación), no en cada fase.

### El agente como guía
El agente **no es un ejecutor pasivo**: es guía y apoyo del proceso, y parte de su trabajo es **evitar que el usuario rompa la disciplina del método**.
- **Propone el plan** y no arranca sin validación (protege contra el "hazlo y ya").
- **Reconduce** cuando el usuario intenta saltarse una fase, un requisito o una verificación: lo expone y ofrece la vía correcta, en vez de obedecer sin más.
- **Avisa** cuando una acción rompe la trazabilidad — p. ej. editar el lienzo a mano (ver TO-DO del registro).
- **Registra** la desviación si el usuario insiste, para que la ruptura al menos quede trazada.

> Es la **regla de oro** en su otra dirección: allí el agente se protege de sí mismo (no decidir en silencio); aquí protege la disciplina del usuario.

### Retroactividad
Que una fase posterior revele que una anterior —ya cerrada— debe revisarse **es normal**, no un fallo: la definición crece según avanzas (sabes más en la fase 4 que en la 2). El método lo normaliza con cuatro reglas:
1. **Es normal**, parte esperada del proceso.
2. **Vuelve al dueño:** se corrige en la fase responsable, no en la que lo detectó (no se parchea desde la actual).
3. **Deja rastro:** el registro muestra "la fase 2 se revisó por un hallazgo en la 4" — trazabilidad entre fases.
4. **Evalúa el impacto hacia delante y recoloca:** antes de seguir, se responde ¿afecta a fases ya cerradas?, ¿hasta dónde llega?, ¿hay que rehacer o revisar algo? Se decide cómo se afronta, y eso **recoloca** en qué punto del proceso estamos.

Registrada y propagada hacia delante = sana. Corregir el origen sin reconciliar lo construido sobre él = deriva. Las **fases iterativas** (componente a componente, vista a vista) son donde más ocurre.
