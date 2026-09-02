# Decisiones de consolidación — estado

**Versión:** v0.5 · **Estado:** borrador (vivo) · **Fecha:** 2026-08-06
**Deriva de:** metodologia-sintesis.md v0.2+ (fuente más actualizada del modelo de cadena/gates), metodologia.md v0.1, entrada-consolidacion-ccode.md v0.1, investigacion/ (00-nucleo, pruebas A/B, recomendaciones), **Prueba C** (registro-implementacion.md + tabla de diagnóstico de desviaciones + triangulación B/C/prototipo)

> Registro compacto de las decisiones cerradas en la conversación de consolidación de metodología. Agrupadas por dónde impactan en el corpus. Es la materia prima para verter contenido en los documentos y el puente si se retoma el trabajo en otra conversación. No sustituye a los documentos de metodología; los alimenta.
>
> **Nota de vigencia:** el modelo de proceso (cadena de transiciones, tres niveles de parada, protocolo de gate) se rediseñó a fondo durante la revisión del sintético; `metodologia-sintesis.md` es hoy la versión más fiel de ese modelo. Los números de sección tipo §3.3.4 / §5.1 / §6.4 que aparezcan más abajo se refieren a la estructura de `metodologia.md` *previa* a la consolidación, no al sintético actual.

---

## A. Raíz (`metodologia.md`) — modelo del proceso

- **Cadena de transiciones (rediseñada desde la experiencia, no desde `00-nucleo`).** T = transición. Proceso **bidireccional** (diseño↔código), **no cíclico**: la producción avanza T1→T3; **T0 es vía de entrada alternativa (reenganche)**, no cierre de ciclo. Se abandonan las etiquetas **T2.5 y T4** del `00-nucleo`.
  - **claude-ai:** columnas en **paralelo** (research · definición · análisis funcional · entidades · historias de usuario · arquitectura de información · requisitos · perfil técnico), con cascada interna en cada columna.
  - **T1:** claude-ai → claude-design (traspaso de la definición).
  - **claude-design (cascada):** T2.1 establecer DS (**o** importar diseño existente = T0) · T2.2 wireframes / baja fidelidad + navegación · T2.3 especificaciones / definición funcional (spec-sheets, estados comunes, componentes compartidos, inputs) · T2.4 alta fidelidad.
  - **claude-code (cascada):** T3.1 informe-inventario · T3.2 DS/estilos · T3.3 shared+shell · T3.4 pages · T3.5 routing.
- **T0 reubicado dentro de T2.1** como origen alternativo (crear DS **o** importar diseño existente: repo de código o servidor de Figma). Deja de ser eslabón huérfano — el "reenganche" se resuelve solo.
- **Orden deliberado: especificaciones (T2.3) antes que alta fidelidad (T2.4).** Contradice el `00-nucleo` (donde la spec salía *de* la hifi); es un cambio de proceso decidido desde la experiencia — primero contrato funcional, luego píxeles.
- **Tres niveles de parada (redefinidos):**
  - **Minigate** — tarea dentro de una transición. Valida contenido; no comprueba versiones.
  - **Gate** — cierre de una transición completa. Validación humana + reconciliación del registro.
  - **Salto de capa** — gate reforzado que pasa a la capa siguiente: genera lo que baja, comprueba versiones y (en claude-ai) verifica coherencia cruzada.
- **Comprobación de versiones: SOLO en el salto de capa** (o a petición del usuario). Los gates de transición interna reconcilian el registro pero no comprueban versiones.
- **Confinamiento de la edición manual a T2.4:** las fases con IA (T2.1–T2.3) siempre dejan registro; la edición manual humana se restringe a T2.4 (ajuste visual), donde no daña la trazabilidad estructural/de contrato ya fijada. **Acota** (no cierra) el lado *diseño* del agujero de trazabilidad: confina *dónde* puede romperse, pero la edición manual en el lienzo durante T2.4 sigue sin registrarse salvo por disciplina del usuario (ver H para ambos lados).
- **Protocolo de interacción en el gate (§5, sección nueva):** guion del agente — anuncio → recepción → consulta → enrutado (corrige aquí / traslada a su nivel / registra-escala-busca opción con el usuario); reforzado en el salto de capa. Reutiliza la clasificación del bloque B, no la reinventa.
- **Enriquecimiento acumulativo (principio):** la información se traslada, amplía y valida en cada minigate y se consolida al cerrar capa; cada parada añade sobre la anterior sin descartarla.
- **Criterio de autosuficiencia a nivel de paquete de capa** (no de documento suelto): el conjunto metodología + instrucciones + doc de proyecto + registro basta para que un agente ejecute la capa de principio a fin sin más contexto.
- **Gobierno del DS en sentido inverso** (regla al raíz): el DS no cambia en código sin quedar registrado en diseño. Cambio de DS nacido en código = *contrabando inverso*: **bueno** si sube a diseño y se registra, **deuda silenciosa** si no.
- **Dirección código→diseño (deriva):** **no es una fase**; es tratamiento **transversal** de actualización entre capas (registro + versionado + disciplina), no parte de la cadena.
- **Principio de gobierno** (nuevo, a §2): Claude.ai es fuente única de decisiones de requisito/alcance; se ajusta arriba y desciende. Design y Code implementan. *Frontera con el gobierno del DS: las decisiones de sistema de diseño se resuelven en Design pero se registran; las de requisito/alcance suben a Claude.ai.* (Ver bloque C.)
- **Método constante, proyecto variable:** el método y su procedimiento son fijos; se aplican a una fuente variable — la definición del proyecto (técnica, funcional y estética), capturada en claude-ai. El stack es solo un caso particular de esa fuente variable.
- **Tres modos de fallo** (antes dos): contrabando y deriva son fallos *de transición* (entre capas/fases); **incoherencia** es el fallo *del paralelismo* (dos piezas definidas en paralelo se contradicen o no encajan) — aparece dentro de una capa con minigates paralelos, es decir claude-ai.
- **Coherencia cruzada en el salto de capa de claude-ai:** por el paralelismo de sus columnas, el salto que cierra claude-ai tiene una función extra que los otros no necesitan — verificar la compatibilidad entre columnas (stack ↔ objetivos del briefing, entidades ↔ historias de usuario…) antes de pasar a diseño. En cascada no hace falta.

## B. Registro por capa y reconciliación en gate (impacta raíz §3.3.4 y las tres metodologías de capa)

- **Registro por capa = libro de decisiones.** Toda decisión que la capa toma sin venir dictada desde arriba queda anotada (incluye desplazar/cambiar estructura en claude-design). Es el mecanismo que convierte contrabando en contrabando *bueno*. **No es nativo de claude-design** (ver bloque E) → hay que instruirlo.
- **Reconciliación en cada gate (variante 2):** el registro se contrasta contra el **documento-guía de la capa** (p. ej. `briefing-instrucciones-claude-design`), **no** contra la metodología transversal (sería caro y mal apuntado).
- **Clasificación de cada decisión:**
  - **Diferido intencional** — la guía dijo "decide tú" → se añade en local, no escala.
  - **Hueco accidental** — la guía calló pero debía opinar → se resuelve en local **+ aviso suave hacia arriba** (la guía quedó incompleta).
  - **Conflicto** — la guía decía X, se hizo Y → se **marca y escala**.
- **Escalada bifurcada:** conflicto de *instancia* → actualizar el documento de proyecto (frecuente); conflicto de *método* → actualizar `metodologia-claude-*`/raíz (raro). (= recomendación 1.)
- **El gate es forzador:** no se cierra con conflictos marcados sin escalar. Impide que la escalada diferida se pudra en deuda silenciosa.
- **El "aviso suave" necesita destino** — probablemente una sección del registro del gate ("huecos de guía detectados") que se revisa al diseñar el *siguiente* proyecto. *A concretar al definir la estructura del registro.*
- Esto **rellena `§3.3.4` (registro de implementación) para las tres capas**, no solo para código.
- **La herramienta se autocorrige:** los cuatro destinos (sin señal / local / instancia / global) son cuatro velocidades de aprendizaje. Es el lazo de retroalimentación del sistema.

## C. Marcador de madurez (impacta raíz + todas las reglas del corpus)

- **Tres niveles, adoptado** (= recomendación 4):
  - **Confirmado** — evidencia en **más de un proyecto o stack**. *(Hoy: nada.)*
  - **Respaldado** — contrastado en A vs B, **un solo proyecto**. Se aplica por defecto; se revisa si otro proyecto lo contradice. *(Hoy: spec sheets (T2.3), blueprint de navegación.)*
  - **Hipótesis** — sin evidencia propia. No se aplica por defecto. *(Hoy: spec-views, informe de alcance.)*
- Reconcilia la contradicción entre `00-nucleo` ("necesario por defecto") y `entrada-consolidacion` ("provisional, observado 1 vez").
- **La Prueba C es lo que puede subir "respaldado" → "confirmado".**
- *Abierto:* posible 4ª vía **"propuesta estructural"** para lo que entra por necesidad de diseño y no se valida por experimento. Quedó sin uso concreto tras descartar las vistas de exposición del DS; se deja anotada por si reaparece.

## D. Capa Claude Design (impacta `metodologia-claude-design` + instrucciones)

- **Tres artefactos desenredados** (antes mezclados en raíz §5.1):
  - **`navigation`** (carpeta/archivo: esquema + prototipo navegable) — **RESPALDADO, por defecto**. Su ubicación y función son **contrato conocido por claude-code**. Resuelve de raíz el hallazgo A (rutas vacías).
  - **`spec-views`** (ficha a nivel de página) — **HIPÓTESIS**. Fuera del paquete de C. Se activa solo si se detectan fallos de interpretación libre a nivel de página en T3. Si algún día se prueba: primero como *proyección derivada* (barata, no diverge), no como fuente autorizada.
  - **Vistas de exposición del DS** — **DESCARTADO**. claude-design ya trae sistema nativo de carga de DS; usarlo en vez de reinventar.
- **Catálogo de artefactos de claude-design** — pieza a consolidar en `metodologia-claude-design`: por artefacto, **nombre + función + cómo crear**, con el filtro nativo-vs-instruir (bloque E). Es el contrato de importación completo que claude-code reutiliza.
- **La revisión visual es una capacidad de gate exclusiva de claude-design** (claude-code no la tiene; sus fallos "no rompen build ni tests" → necesita mecanismos explícitos). Gates asimétricos.

## E. Reparto nativo-vs-instruir de claude-design (línea base en frío — alimenta el catálogo D)

| Capacidad | claude-design de fábrica | En `metodologia-claude-design` |
|---|---|---|
| Aplicar DS vinculado | Automático | **Invocar** + sanear (Industry ≠ Material 3) |
| Componentes reutilizables | Semi (1 componente por defecto) | **Instruir** extracción/parametrización |
| Prototipo navegable | Explícito (bajo petición) | **Instruir** (el `navigation`) |
| Trazabilidad / bitácora | **No nativo** (versiona duplicando archivos) | **Instruir** entera |
| Reglas permanentes | `CLAUDE.md` | **Invocar** con contenido nuestro |
| Handoff a Claude Code | Nativo pero **agnóstico de framework** | **Instruir** extras: MAPPING.md Angular, esquema de rutas, porqué/prioridades, stack |
| Import GitHub | Nativo, bidireccional | **Invocar** para `ex` (a validar) |

- **Handoff por defecto NO genera routing ejecutable** (navegación va como prosa) ni impone framework (dice a claude-code "elige tú"). Por eso el stack debe entrar a C como dato duro, no confiado a un spec sheet.
- **Import GitHub copia lo que la página renderiza (assets/estilos), no la lógica del bundler.** Límite a medir cuando se valide `ex`.
- **Delta historial (medido):** el paquete por defecto trae el *qué* (pantallas, tokens, medidas, copy), no el *porqué* ni las reglas tácitas. La brecha es lo que la metodología debe **forzar a volcar**.
- **Filtro de método:** para saber qué hace claude-design en limpio, preguntar en proyecto/hilo **sin historial**. Toda respuesta sobre un hilo con historial hereda sesgo.

## F. Capa Claude Code y Prueba C (impacta `metodologia-claude-code-im` + diseño de C)

- **La frontera claude-design→claude-code es de plataforma, no metodológica:** claude-design nunca produce código ejecutable, en ningún camino. Entrega HTML fiel + mapeo documentado; el build es de claude-code.
- **Propósito real del corpus:** ser el **contexto limpio** con que el método se autovalida. `metodologia-claude-code-im` + `guia-conversion` = paquete autosuficiente → **agente ciego** convierte una feature nueva = **Prueba C**.
- **Ambición: limpio en las tres capas.** C es primero para código; claude-design análogo después. El listón de autosuficiencia sube para todos los documentos.
- **Criterio de calidad de cada documento:** "¿un agente que solo lee esto, sin nada más, hace lo correcto?"
- **C es prueba de dos lados:** (1) generar el handoff sin sesgo de historial, con extras fijos (no opt-in); (2) evaluar el paquete desde contexto limpio; (3) claude-code ciego convierte. Saltar (2) daría un resultado engañosamente optimista.
- **Los cinco extras opt-in del handoff pasan a obligatorios** en el contrato: MAPPING.md Angular completo, esquema de rutas Angular, copiar brief congelado + Trazabilidad.md, nota anti-Industry, screenshots (decidir).
- **Saneamiento previo a C:** "Industry huérfano" → instrucción fija "Material 3, ignora el DS Industry vinculado" (no recordatorio humano).
- **Coste de la autocorrección: sin medir** → métrica a registrar en C (coherente con dossier §1: coste/latencia se registran, no evalúan).

## G. Ejes documentales, nomenclatura y estructura

> **Actualizado por el bloque L** (abajo): un documento de metodología por capa; nomenclatura agnóstica; estructura `core/`+`domain/`; `metodologia-aplicada` como visión general en `core/`.

- **Simetría de capas.** La capa de **definición** tiene funciones propias (research, análisis funcional, requisitos, perfil técnico) — no es solo orquestador → tiene su propia metodología de capa, simétrica a diseño e implementación.
- **Un documento de metodología por capa** (revisa el "tres documentos"): cada capa tiene **un** documento que reúne **metodología + procedimiento**. El **registro** es tier 3 (dato de instancia), no un documento de método. *(Al extraer el protocolo común, la frontera metodología/instrucciones se volvía artificial — L.4.)*
- **Nomenclatura agnóstica de herramienta:** `metodologia-capa-diseno`, `metodologia-capa-conversion`… (sin nombres de herramienta). La tercera capa se llama **implementación**.
- **Estructura en disco (real, repo `design-to-code`):**
  - `core/` — universal + visión general: `metodologia-global`, `metodologia-aplicada` (visión general de las tres capas), `arquitectura-de-contextos`, `convenciones-repo`.
  - `domain/` — operativo por capa: `capa-diseno/` (metodología + fases + `spec/`); `capa-definicion/` y `capa-conversion/` pendientes.
  - Raíz: `metodologia-sintesis` (esquema), `decisiones-consolidacion`, `entrada-decisiones`, `CONTEXT_GIT`.
  - *(Sustituye a la estructura anterior `metodologia/`+`proyecto/`. El tier 3 no se centraliza: vive por capa o en la herramienta.)*
- **`im` = diseño→código (actual)** · **`ex` = código→diseño (pendiente)**.
- **`metodologia-sintesis` = esquema/mapa del sistema** (reconvertido; ya no es un andamio que desaparece).
- **Raíz canónico = `metodologia-global` + `metodologia-aplicada`** (el antiguo `metodologia.md` detallado queda superado; `00-nucleo` archivado en investigación).

## H. Pendientes anotados (no cerrados)

- **`claude-code-ex`:** desarrollar, separando sus **dos procesos** — T0 (fase) y reconciliación de deriva (transversal). Ambos se apoyan en el import nativo de claude-design (GitHub/`github.md`).
- **T0 tiene dos orígenes** (repo de código o servidor de Figma): al validarlo, hacerlo por origen — pueden comportarse distinto. Solo el origen "repo de código" conecta con el import nativo ya observado; Figma no se ha explorado.
- **Escenario "proyecto que arranca desde código" (código→diseño de entrada):** fuera de alcance por ahora; apuntado.
- **Plantilla "proyecto nuevo":** la estructura ya separa heredar/generar, pero falta montar el mecanismo de instanciación (qué se copia, qué nace vacío).
- **Minigates concretos por capa:** por declarar (Claude.ai: entidades, historias, alcances, vistas, navegación, perfil técnico; claude-code: análisis de archivos claude-design, informe previo, informe de resultados…).
- **Destino del "aviso suave":** concretar dentro de la estructura del registro.
- **4ª vía de madurez "propuesta estructural":** abierta, sin uso concreto tras descartar exposición del DS.
- **Contenido exacto del paquete de handoff en frío:** caracterizado a alto nivel; convertir los extras opt-in en obligatorios al redactar el contrato.
- **Medir coste de la autocorrección en C.**
- **Agujero de trazabilidad — ediciones manuales fuera del chat IA:** si el humano modifica algo directamente en la herramienta (editor de claude-design, o código en claude-code), el agente no se entera y no lo anota en el registro = deuda silenciosa por vía no-IA.
  - **Lado diseño — ACOTADO, NO CERRADO** (corrige el "RESUELTO" anterior): el confinamiento a T2.4 (bloque A) acota *dónde* puede ocurrir —la trazabilidad estructural/de contrato de T2.1–T2.3 queda a salvo— pero **no cierra** el agujero: crear o editar elementos a mano en la vista de diseño durante T2.4 no pasa por el agente y no se registra. Cerrarlo depende de **disciplina del usuario** (declarar la edición), no de garantía mecánica. Estrategias a explorar (paralelas al lado código): (a) el agente registra el estado del archivo y detecta cambios no suyos; (b) pregunta al detectar una modificación externa; (c) alguna captura del cambio manual.
  - **Lado código — ABIERTO:** un desarrollador que toca el código a medio proceso sigue sin quedar registrado. Opciones a explorar: (a) reconciliar el estado real contra el registro al reanudar / en el salto de capa (diff); (b) apoyarse en git para detectar cambios no registrados; (c) disciplina humana (declarar la edición antes de cerrar el gate); (d) paso explícito en el salto de capa "¿hubo cambios manuales sin registrar?". Ninguna verificada.

---

## I. Hallazgos de la Prueba C (conversión ciega diseño→código)

> **Qué fue C:** primera conversión en limpio — agente sin historial, solo con el paquete de método (`metodologia-claude-code-im` + `instrucciones-claude-code-im` + `contrato-handoff`), el perfil técnico del repo vía `CLAUDE.md`, y el paquete de handoff generado desde claude-design. Cobertura completa (DS/estilos → shared → shell → páginas → routing), como la Prueba B. Diferencia con B: B tenía todo el historial de A delante; C fue ciega.
> **Estado:** evidencia sólida (registro con decisiones/huecos escalados + tabla de diagnóstico con evidencia citada por fila + triangulación B/C/prototipo del desarrollador). Madurez de los hallazgos: **respaldado** (un proyecto).

### I.1 Lo que C validó del método (funcionó)

- El agente ciego **escaló cada hueco en vez de rellenarlo en silencio** (huecos #1–#10 del registro, todos resueltos con el desarrollador). El protocolo de gate y la "regla de oro" funcionaron.
- Respetó la variante descartada (`single`) sin implementarla; siguió el orden T3.2→T3.5 por su cuenta; cerró con el DoD **verificado por grep, no de palabra** (0 `@Input`, 0 `*ngIf`, 0 hex hardcodeado, 98 tests).
- **Fidelidad textual/estructural/de comportamiento: alta** (microcopy exacto, aria-labels, formatos de fecha, cascada de reseteo, modos de la tarjeta, fuente Material Symbols con eje FILL). Lo explícito en el markup sobrevivió.

### I.2 El hallazgo central — no hay gate visual en la conversión, y la regla que lo suplía no viajó al paquete

- **Causa raíz confirmada por el propio agente:** toda la verificación fue `ng build` + `ng test`; **nunca se abrió un navegador**. Los tests verifican texto/atributos/comportamiento, no layout visual → **dieron falsa confianza**. 10 de 12 desviaciones visuales son causa (B) *"estaba en el origen y no se portó"*: no se perdieron por falta de definición, sino porque **nada verificó la fidelidad visual**.
- **Mecanismo del fallo (patrón recomendación 6 + 7):** existía una regla del usuario ("para cambios de UI, verificar en navegador") que **no estaba en el paquete de C** — vivía en el `CLAUDE.md` general / reglas globales, no en los documentos de método. El agente ciego solo aplica lo que está en su paquete → no la conoció → construyó sin gate visual → los tests verdes lo confirmaron en falso.
- **Confirma la asimetría de gates ya prevista** (§6.2 del sintético): claude-design tiene gate visual (el humano ve); claude-code no. C lo vuelve empírico.

### I.3 Decisiones de método que C obliga a tomar (para la próxima conversión ciega)

1. **Añadir un gate visual a la conversión** (o su sustituto operativo: obligación explícita de verificar en navegador antes de cerrar cada página/T3.4 y el salto de capa). Sin él, los tests verdes mienten sobre la fidelidad. → impacta `metodologia-claude-code-im` + `instrucciones-claude-code-im`.
2. **Las reglas de verificación del usuario deben viajar al paquete.** Una regla que vive solo en el `CLAUDE.md` general no la aplica un agente ciego. El contrato de handoff / las instrucciones deben **incorporar explícitamente las reglas de verificación**, no darlas por heredadas. → impacta `contrato-handoff` + `instrucciones-claude-code-im`.
3. **La regla "componentes nativos, no markup reconstruido" necesita una pauta de reconciliación de valores:** qué hacer cuando el componente nativo (Material) no reproduce los valores exactos del hi-fi (paddings, alturas, gaps). Hoy el método dice *qué* componente usar, no *cómo* casar sus valores con el hi-fi. (Desviaciones 2 y 9.) → impacta `metodologia-claude-code-im` §4.
4. **El DoD verifica lo prohibido pero no lo obligatorio:** comprueba "nada hardcodeado" pero no "aplica el token de superficie a la raíz". Un checklist de "no hagas" sin su "haz" correspondiente deja huecos. (Desviación 1: fondo blanco.) → impacta el DoD del perfil técnico + la idea general de checklists (recomendación 7: "¿falla en silencio pese a que lo automático dice OK?").
5. **Hallazgo hacia arriba (deriva inversa T3→T2.3):** el MAPPING reveló que el spec sheet no tipificaba varios patrones (bottom-nav, skeleton, estados, y sobre todo los bloques de hora como botón/chip — desviación 11). La conversión destapó un hueco de la especificación. → impacta `metodologia-claude-design` (el spec debe cubrir comportamiento nativo de más componentes) + el nº de componentes que abarca el spec sheet.

### I.4 Triangulación B/C/prototipo (instrumento del desarrollador — reordena la conclusión)

Comparar los tres, no solo C vs prototipo, parte las desviaciones en tres clases con causas distintas:

- **Clase 1 — falla en C, bien en B** (fondo, posición del botón, color): la definición era la misma para ambos → la causa **no es falta de definición**, es que **C perdió lo que el historial de B aportaba** (y probablemente B miró el render). Apunta a qué debe llevar el paquete de handoff para que una conversión ciega iguale a B.
- **Clase 2 — falla en B y en C** (stepper, color de botón): fallo **aguas arriba de la conversión** (spec o hi-fi); si B con todo el contexto tampoco lo clavó, el detalle no estaba disponible para ninguno.
- **Clase 3 — C acierta y B falla** (botones de acción en footer, botón de perfil centrado): **C fue más fiel que B en varios puntos.** Conclusión corregida: no es que "el modo ciego degrade" — **ni B ni C clavaron el prototipo; perdieron y ganaron fidelidad en sitios distintos.** El problema es sistémico del pipeline diseño→código, no del modo ciego.

### I.5 Matices y no-hallazgos (para no atribuir mal)

- **Los radios del selector (desviaciones 10/11) NO son violación del agente:** el agente **escaló** (hueco #8) y **el desarrollador decidió** `MatRadioButton` (registro T3.1). El punto de escalado funcionó; lo que falló fue que **la decisión humana en el gate fue visualmente infiel** porque se decidió sobre una descripción, sin ver el resultado. Es un fallo del *gate humano*, no del agente. → refuerza I.3.1 (hace falta ver el render también al decidir en el gate).
- **El stepper hecho a mano (desviación 6) SÍ fue fallo de ejecución del agente:** tenía el mapeo correcto (`MatStepper`) disponible en el handoff y se desvió sin registrarlo. Único caso donde el agente falló a su propio método. Fallo de ejecución, no de método.
- **El bug Chrome/Firefox (horas no visibles en Chrome) NO es desviación de diseño:** es un bug de render, afecta a B y C por igual → del código base/Material, no del método. Se trata aparte.
- **Cero causas (A) en la tabla:** el agente sometió su explicación más cómoda ("no estaba definido") al test de doble verificación y la descartó con evidencia en los 3 casos dudosos. La tabla es fiable.

### I.6 Separación proyecto vs. método (para no mezclar tareas)

- **9 desviaciones de proyecto** (fixes concretos, varios de una línea): arreglo de la conversión de C, en pasada aparte.
- **3–4 de método** (I.3): cambios al corpus para que la próxima conversión ciega no repita el fallo.
- **Orden recomendado:** arreglar el método **antes** que C — el fix del gate visual cambia *cómo* se corrigen los 9 de proyecto (con verificación en navegador esta vez). Arreglar C sin el gate reintroduciría desviaciones que los tests no cazan.

---

## J. Saneamiento documental de la capa de diseño (post-C, pre-D)

> **Qué fue:** tras C se saneó la documentación del proyecto de diseño para alinearla a `metodologia-claude-design` **sin tocar el prototipo** (límite duro). Objetivo: dejar un input limpio para D. La capa de diseño no tenía registro vivo ni tipificación exhaustiva; el brief original quedó marcado como **desfasado** (valor histórico, no fuente de verdad).

### J.1 Confirmación de la tesis "dependemos de la documentación de la capa superior"

- La trazabilidad existía pero es **manual, parcial y unidireccional** (WF→HF): registra decisiones pero no tiene canal de vuelta al briefing ni tipificación exhaustiva. El saneamiento encontró **seis desincronizaciones trazabilidad↔prototipo** (variante descartada aún en código, barra de navegación triplicada no extraída, "4 estados por vista" inexacto, snackbar de error no ejecutable, discrepancia de token `--surface`, "spec visual pendiente" obsoleto).
- **Hallazgo de raíz documental de un fallo de C:** el spec declaraba `--surface: #ffffff` mientras el prototipo usa `#fef7ff` → es la causa documental del fallo "fondo blanco" de C. Una desincronización de token en la capa de diseño se manifestó como desviación visual en la conversión. Confirma que los fallos nacen aguas arriba y se manifiestan aguas abajo.
- **Conclusión afinada:** el problema no era ausencia de registro, sino que al registro le faltaban **dos funciones** — propagación hacia arriba (regla 3.3) y tipificación exhaustiva elemento→componente (regla 3.1). Son exactamente las que la metodología nueva añade.

### J.2 El selector: causa raíz del fallo estrella de C, resuelta en su capa

- El fallo de los radios en C (decisión de componente tomada en la conversión) tenía su origen en que **el spec no tipificaba el selector** — lo dejaba como "select/desplegable/pendiente" mientras el prototipo ya era radios+chips.
- El saneamiento lo tipificó **leído del prototipo**: Centro/Especialidad/Médico → `MatRadioButton`; Hueco → `MatChipListbox`; excluyendo explícitamente `MatSelect`/`MatAutocomplete` porque cambiarían la apariencia.
- **Valida el fix de método I.3 + regla 3.1 de diseño:** cuando el spec declara el componente nativo (leído del diseño, no elegido), la decisión desaparece de la capa de conversión. D no heredará este hueco.

### J.3 Criterio "definible por lectura vs. decisión de diseño" (frontera operativa)

- Al cerrar huecos sin tocar el prototipo se fijó un criterio reutilizable: **se define ahora si la respuesta se *lee* del prototipo** (una sola respuesta, no cambia nada visible — traducción a `mat-*`); **no se define si se *elige*** (varias respuestas, alteraría apariencia/comportamiento/contenido — es diseño).
- Regla de sesgo: ante la duda, es decisión de diseño (no se decide, se marca). Protege la invariancia del prototipo.

### J.4 El diseño generado dejó incompletos los estados no-felices (material para v2/E)

- El "Grupo B" (huecos que son decisión de diseño, no traducción) tiene un patrón: **todos son estados no-felices o infraestructura de UI** — barra de navegación (H2), skeleton de carga (H3), estado vacío/error (H4), literal de error (H7), validación (H8).
- **El prototipo diseñó a fondo el camino feliz y dejó a medio definir carga/vacío/error**, pese a que el brief §10 los hacía regla obligatoria. Hallazgo: la generación de diseño asistida cubre bien el happy path y deja incompletos los estados de borde aunque el brief los exija. → material directo para afinar `metodologia-claude-design` (capa de diseño en generación, no solo documentación).
- **Dos subtipos dentro del Grupo B:** decisión de *estrategia de componente* (H2/H3/H4 — roza implementación, cuidado con la frontera código/diseño) y decisión de *contenido* (H7/H8 — texto que no existe, puramente diseño). Los segundos son los más limpios de cerrar en v2.

### J.5 Marco experimental D / E (fijado)

- **D** = conversión ciega sobre prototipo **v1** (saneado, huecos de diseño sin rellenar) + método mejorado. Mide **solo el método mejorado**; variable única frente a C.
- **E** = conversión ciega sobre prototipo **v2** (Grupo B completado en iteración de diseño propia, con registro) + mismo método. Mide el pipeline sobre diseño entero.
- **E vs D** aísla cuánto aportó completar el diseño (única variable que cambia). Exige mantener v1 intacto → por eso saneamiento y completado van separados.
- **v2 será la primera vez que la capa de diseño toma decisiones de diseño bajo la metodología nueva** (anticipo del afinamiento de la capa de diseño en generación).
- **Orden:** registrar → aplicar fixes de método de código (I.3, agnósticos) → **D** (sobre v1) → iteración de diseño a v2 → **E**. Los fixes de método son idénticos en D y E, para que E vs D aísle limpio la variable "diseño completo".

---

## K. Hallazgos tempranos de la Prueba D (antes de convertir código)

> D aún no ha convertido nada, pero su arranque ya ha destapado huecos de método — igual que C los destapó en la verificación. Esto confirma el patrón: cada prueba en limpio revela un eslabón que las sesiones con historial daban por hecho.

- **K.1 — El eslabón "de dónde sale el handoff" no estaba documentado.** El agente ciego encontró el repo con solo el esqueleto de `ng new`, sin paquete de handoff, y **sin instrucción de cómo obtenerlo**. Paró correctamente (registró el hueco y consultó, según `instrucciones §1.3`) — el método funcionó en su parte de "no improvisar" — pero faltaba decir que el handoff vive en el proyecto de Claude Design y se obtiene por MCP. En C no se notó porque el handoff se generó en la misma sesión. **Corregido:** añadido §0 bis en instrucciones, §0 en el contrato, y nota en `CLAUDE.md` — vía MCP (por defecto) o paquete congelado; si no se puede obtener, hueco bloqueante.
- **K.2 — Decisión de alcance: D no exige aislamiento estricto.** Se acepta que el agente lea documentos de metodología/proceso del proyecto de diseño por MCP. Razón: el trabajo es afinamiento incremental del método, no un experimento controlado; C↔D ya no es comparación exacta (entre ambas cambiaron spec saneado + fixes de código + DoD nuevo). Se mantiene solo la cláusula anti-arqueología de git (no copiar código de conversiones anteriores), por evitar atajos, no por pureza.
- **K.3 — Dos desincronizaciones perfil-técnico↔repo detectadas por el agente** (a registrar/resolver, no bloqueantes): (a) `styles.scss` trae el theme Material por defecto (azure/blue) en vez de la semilla M3 `#6750A4` que fija el perfil técnico; (b) `angular.md` da por existente un `AppButtonComponent` que no está en `src/`. Mismo tipo de fallo que venimos viendo: documentación que asume un estado del repo que no coincide con el real.


---

## L. Estructuración del corpus (tiers), proceso de la capa de diseño y sistema de specs

> Fusión condensada del bloque L. Detalle en `entrada-decisiones-2026-08-06.md` (L.1–L.13); L.14–L.16 son decisiones posteriores de la misma línea.

- **L.1 · Tres tiers.** Tier 1 global (universal, agnóstico) · tier 2 aplicado (proceso de tres capas) · tier 3 datos de proyecto (no es metodología). Cadena: global → se instancia en aplicada → se alimenta con tier 3.
- **L.2 · Nomenclatura agnóstica de capas** (`capa-definicion/diseno/conversion`). La tercera capa: **implementación**.
- **L.3 · Partición global↔aplicado:** el núcleo abstracto va a global; el detalle atado al proceso, a aplicada.
- **L.4 · Un documento por capa** (metodología + procedimiento); el registro es tier 3. Revisa el "tres documentos" de §G.
- **L.5 · Protocolo común de agente/gate** — con el enfoque autosuficiente queda **embebido en cada documento de capa**; `metodologia-aplicada` (en `core/`) pasa a *describirlo*, no a definirlo.
- **L.6 · Proceso de la capa de diseño = fases** (revisa "dos granos"): fase app · fase componentes (tareas iterativas) · fase vistas · cierre. Una **fase** = una o varias **tareas**, calculadas por proyecto; el **gate** cierra la fase.
- **L.7 · Orden HF → spec** en la fase de componentes (supersede "especificaciones antes que alta fidelidad"): la spec recoge valores visuales ya asentados; elimina el "Spec visual: pendiente".
- **L.8 · Reglas firmes de diseño:** DS-first + referencia; **ninguna vista incluye componentes sin ficha**.
- **L.9 · Gobierno de divergencia del DS:** no divergencia silenciosa; aporte general → amplía DS, específico → local; siempre registrado.
- **L.10–L.12 · Sistema de specs (`spec/`):** moldes (componente, vista, entidades) + hojas de requisitos (app, ds, navegación) + índice (`spec-vision-general`). Anidamiento app → vistas → componentes → DS; entidades transversal (nace en definición). Nomenclatura `spec-*`; separación requisitos (specs) ↔ proceso (método).
- **L.13 · Tokens en dos capas** (primitivos + semánticos), consumo **solo semántico**, por defecto (reemplaza "solo si se anticipa rebrand").
- **L.14 · Retroactividad** (cuatro reglas: normal · vuelve al dueño · deja rastro · evalúa impacto hacia delante y recoloca), en dos direcciones: **entre capas** y **entre fases**. Principio en global; mecanismo en aplicada; aplicación en la capa.
- **L.15 · Versionado en dos ejes:** por **documento** (cabecera `v0.x`, mecánica en `convenciones-repo`) y por **Git** (decisión = commit, `R-00X`, en `CONTEXT_GIT`). *(Abierto: si ambos ejes conviven o si `R-00X` sustituye a las cabeceras por documento.)*
- **L.16 · Repo:** el corpus vive en `design-to-code` (subido). *(Abierto: reconciliar con la idea previa de "MP4AI dentro del repo de código / repo por proyecto" — hoy es un repo de metodología independiente.)*
