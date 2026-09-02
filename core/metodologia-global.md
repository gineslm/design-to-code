# Metodología global — núcleo universal

**Versión:** v0.4 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-sintesis.md v0.2 (principios), metodologia.md v0.1 (prosa atemporal), entrada-decisiones-2026-08-06.md (L.1, L.3), decisiones-consolidacion.md v0.3.
**Tier:** 1 (universal).

> **Qué es.** El núcleo **agnóstico**: principios y valores válidos para **cualquier** proceso de transformación por etapas. No menciona capas, agentes ni herramientas, y no describe la *maquinaria* de un proceso concreto (eso es tier 2). Su instanciación vive en `metodologia-aplicada`.
> **Nota de madurez.** Este núcleo se ha extraído de **un solo proceso**. Los principios clásicos tienen respaldo externo; lo marcado *[extraído de un proceso]* (§3) aún no está probado como universal.
> **Qué salió de aquí.** El *contrato entre etapas* y la *meta-plantilla de procedimiento* se trasladaron a `metodologia-aplicada` (maquinaria de proceso). Del *versionado* se conserva aquí el **principio** (§1); su **mecánica** concreta (numeración, cabeceras, «Deriva de») vive en `convenciones-repo`.

---

## 1 · Principios

**Trazabilidad.** En un proceso por etapas, la salida de cada fase deriva de la anterior. Trazabilidad significa que todo elemento del resultado final puede seguirse hacia atrás hasta la decisión o la fuente que lo originó, y que toda decisión de origen puede seguirse hacia delante hasta dónde aterriza. No es documentar por documentar: es lo que hace el proceso **auditable y corregible** — cuando algo va mal aguas abajo, se puede localizar dónde entró. Sin ella, los errores se vuelven indiagnosticables y la cadena es una caja negra. Es la precondición del resto: no se puede reconciliar ni detectar deriva sobre lo que no se puede rastrear.

**Versionado y linaje.** Todo lo que se produce lleva una **versión** y registra su **linaje** —de qué deriva y en qué versión—. Esto extiende la trazabilidad al tiempo: permite saber cuándo un derivado queda **desfasado** respecto a su fuente. Es principio, no mecánica: *cómo* se implementa (numeración, cabeceras) vive en `convenciones-repo`, no aquí.

**Reducción de ambigüedad.** Cada transición entre fases es un punto donde la interpretación puede divergir. La ambigüedad que se deja en un artefacto la resuelve —de forma distinta y a menudo en silencio— quien lo consume después. El principio: en cada fase, hacer explícito lo que estaba implícito, para que el receptor interprete menos y ejecute más. No se trata de eliminar todo juicio, sino de que las decisiones se tomen **donde corresponde** (arriba, con contexto) y no caigan por defecto en el actor peor informado de aguas abajo. Previene justo eso: decisiones tomadas por descarte río abajo, donde ya no existe el contexto para tomarlas bien.

**Reutilización y consistencia.** Cuando un patrón aparece más de una vez, se define **una** vez y se reutiliza parametrizado, no se replica. La réplica multiplica el mantenimiento y deja que las copias se separen entre sí; una fuente única parametrizada las mantiene consistentes por construcción. Aplica a componentes, tokens, reglas. Previene la divergencia entre copias que deberían ser idénticas y la incoherencia silenciosa que le sigue.

**Cascada con iteración.** El proceso avanza en cascada —una fase se cierra, validada, antes de abrir la siguiente— pero no es cascada rígida: se itera dentro de una fase hasta que está bien, y la cadena entera vuelve a iterar cuando aparece un alcance nuevo. La cascada protege cada fase de construir sobre terreno no validado; la iteración evita que sea frágil. Previene edificar aguas abajo sobre cimientos que no estaban firmes, y el retrabajo en cascada que dispara un error descubierto tarde.

**Retroactividad.** Un proceso por etapas admite **volver a una fase ya cerrada** cuando una posterior revela que debe revisarse; es **normal**, no un fallo: el conocimiento crece según se avanza. La revisión hacia atrás se corrige en su origen, **deja rastro**, y **evalúa su impacto hacia delante** —qué de lo ya construido sobre esa fase queda afectado—, recolocando el proceso donde el cambio obligue. Es el complemento de la cascada: aquella avanza, esta permite retroceder sin romper. Registrada y reconciliada hacia delante = sana; corregir el origen sin reconciliar lo que se apoyaba en él = deriva sembrada.

**Enriquecimiento acumulativo.** La información no solo atraviesa las fases sin cambiar: en cada parada se traslada, se **amplía** (se añade detalle) y se valida — y, crucialmente, no se descarta nada de lo ya establecido. Cada parada añade sobre la anterior. Es el reverso positivo de la deriva: la cadena debe hacerse más rica, no perder fidelidad. Previene la pérdida de detalle ya fijado al avanzar (que es deriva) y la re-derivación redundante de lo que ya estaba resuelto.

**Método constante, fuente variable.** El método y sus procedimientos son fijos y reutilizables; lo que cambia de un caso a otro es la **fuente** a la que se aplican — la definición concreta del proyecto (técnica, funcional, estética). Separar lo constante (el método) de lo variable (el caso) es lo que hace el método reutilizable entre proyectos en vez de reinventado cada vez. Previene confundir las decisiones de un caso con el método mismo, lo que lo volvería irreutilizable y fosilizaría las elecciones de un proyecto como si fueran reglas universales.

## 2 · Paradas y validación

Un proceso por etapas necesita puntos de control, y no todos son iguales. Hay **tres niveles anidados**: la parada dentro de una tarea (de grano fino, valida contenido), la que cierra una etapa completa (consolida y reconcilia), y la que cruza una **frontera mayor** hacia otra fase — la reforzada, donde se comprueban coherencia y versiones antes de entregar.

Toda parada lleva **validación humana**: el cierre no se automatiza, porque el sentido de la parada es el juicio, no el paso mecánico. Y la parada es **forzadora**: no cierra mientras haya un conflicto marcado sin escalar. Esto previene el paso silencioso de trabajo no validado a través de una frontera, y los conflictos que se entierran en vez de resolverse.

## 3 · Modos de fallo  *[extraído de un proceso]*

Tres formas típicas en que un proceso por etapas falla:

- **Contrabando** — aparece algo que ninguna etapa autorizó. No es malo por sí mismo: puede revelar un requisito real que emergió durante el trabajo. Lo que decide si es **hallazgo sano** o **deuda silenciosa** es si queda **registrado**.
- **Deriva** — se pierde o se contradice algo ya cerrado aguas arriba. Es el reverso del enriquecimiento acumulativo.
- **Incoherencia** — dos piezas producidas en paralelo no encajan (solo posible donde el trabajo es paralelo, no en cascada).

La línea divisoria de los tres es la misma: **el registro**. Lo registrado es auditable y corregible; lo no registrado es deuda invisible.

## 4 · Registro y decisiones

El registro es el **libro de decisiones** del proceso: toda decisión no dictada desde arriba se anota **en el momento** en que se toma, no reconstruida de memoria al final — la reconstrucción pierde precisión y es el primer paso hacia el contrabando silencioso. Al cerrar cada etapa, el registro se **reconcilia** contra el documento-guía de esa etapa.

Cada decisión se **clasifica**: diferido intencional (local, deliberado), hueco accidental (local, con un aviso suave hacia arriba) o conflicto (se marca y se escala). La **escalada bifurca**: un conflicto sobre la instancia va al documento del caso; un conflicto sobre el método va a la metodología. Todo esto previene que una decisión viva solo en una cabeza o en un historial de conversación, indistinguible después del contrabando, y protege la trazabilidad.

## 5 · Madurez de las reglas

No toda regla tiene la misma autoridad, y fingir lo contrario es peligroso. Cada regla se marca según su evidencia: **confirmado** (se sostiene en más de un caso), **respaldado** (contrastado en un solo caso) o **hipótesis** (sin evidencia propia todavía).

La marca es honestidad epistémica: una hipótesis disfrazada de regla firme fosiliza una sola observación como ley; una regla confirmada tratada como tentativa desperdicia conocimiento ganado. El marcado previene ambos errores — dar a una observación de un caso la autoridad de un universal, y lo contrario.
