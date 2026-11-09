# Metodología global — núcleo universal · metodología de IA

**Versión:** v0.5 · **Estado:** borrador (en redacción) · **Fecha:** 2026-08-09
**Deriva de:** metodologia-global.md v0.4 (reestructuración **MAYOR**: de lista de principios a **tres registros** —principios · morfología · estructura—; trazabilidad absorbe versión/linaje y pasa a cierre del set; entran validación, suficiencia del traspaso, dirección de decisiones; sale reutilización/consistencia), metodologia-capa-diseno.md v0.22 (vocabulario proceso · fase · tarea · capa · contrato). **Reencuadre de alcance:** de «cualquier proceso por etapas» a «cualquier proceso asistido por IA» —agnóstico de herramienta/proceso/proyecto, no de la IA (§0)—.
**Tier:** 1 (universal).

> **En redacción, por secciones.** §1, §3 y §4 están desarrollados en prosa (estilo definición + ejemplo); §2 y §5 siguen como esqueleto —encabezados y una línea por ítem— hasta desarrollarse.
>
> **Cómo leer esto.** Para hacerse una idea de la metodología basta con **§1–§4**: principios, morfología, estructura y modos de fallo. §0 (encuadre) y §5 (madurez) son secundarios —tratan del método del documento más que de la metodología— y pueden dejarse para una segunda lectura.
>
> **Estilo.** Cada concepto se enuncia primero como **definición agnóstica**; cuando ayuda, sigue un **ejemplo concreto** en bloque aparte (`> *Ejemplo.*`). El ejemplo ilustra, no es norma: es intercambiable y no forma parte del núcleo.

---

## §0 · Qué es

- **Qué es esto.** El núcleo **tier-1** de una metodología para **implementar IA en procesos**: los principios y el modelo válidos para **cualquier** proceso asistido por IA, con independencia de la herramienta, el proceso y el proyecto concretos.
- **Qué significa «agnóstico» aquí.** Independiente de la **instancia** —la herramienta con nombre propio, el proceso específico, el proyecto—, **no de la IA**. Nombrar **IA, agente o herramienta de IA** es tier-1, porque son el objeto de la metodología; nombrar *una* herramienta concreta, *unas* capas o *unas* fases determinadas es tier-2.
- **Tres registros del documento:** **principios** (propiedades/valores) · **morfología** (dinámica de consolidación) · **estructura** (arquitectura de unidades y fronteras).
- **Vocabulario estructural.** Tier-1 nombra el patrón abstracto (capa · contrato · fase · tarea); su instancia —qué capas, qué herramienta, qué fases— es tier-2.
- **Método y caso:** el método es constante y reutilizable; lo variable es la **fuente** a la que se aplica (la definición del proyecto). Separarlos es la **razón de los tiers** y evita fosilizar las elecciones de un caso como método. *[ex «método constante, fuente variable»]*
- **Nota de madurez:** el núcleo se ha extraído de **un solo proceso**; lo clásico tiene respaldo externo, lo marcado *[extraído]* aún no está probado como universal.
- **Qué vuelve a global:** el **concepto abstracto de contrato** (su instancia —briefing, handoff, perfil técnico— sigue en tier-2).

---

## §1 · Principios
> Propiedades que el proceso y su resultado deben cumplir. Pocas; sostienen el resto del documento —las normas de §2–§3 se anclan a ellas—. Los tres primeros generan y disciplinan el conocimiento; el cuarto emerge de ellos y cierra el conjunto.

### Punto de partida
Esta es una metodología para **implementar IA en procesos**, y su enfoque nace de cómo trabaja un agente. Delegar una tarea en un agente **no es** fijar el objetivo y esperar a que él lo resuelva bien: el agente trabaja **solo con la información que se le da**, y **toda ambigüedad que esa información deja abierta la resuelve él mismo**, por su cuenta y sin avisar, camino del resultado. Ese es su límite y su riesgo —decidir en silencio allí donde falta contexto—, y es justo lo que el método tiene que contener.

Por eso el punto de partida de un proceso es una **unidad de incertidumbre** que hay que **ir informando**: en cada etapa donde el agente encuentre algo sin determinar, decidirá por sí mismo. La estrategia, entonces, no es **recortar etapas para ir más rápido**, sino **completarlas una a una y validarlas**, de modo que toda la información necesaria para fijar el objetivo quede **capturada en el proceso** antes de que un agente tenga que suplirla por su cuenta.

Los cuatro principios que siguen son las propiedades —válidas para cualquier proceso por etapas— que garantizan que eso ocurra.

### 1 · Reducción de ambigüedad
Cada transición entre etapas es un punto donde la interpretación puede divergir. Toda ambigüedad que un artefacto deja abierta la resuelve quien lo recibe después —y cuando ese receptor es un agente, la resuelve **de forma literal y silenciosa**: en vez de preguntar, genera la respuesta que le parece plausible y sigue—. El principio: en cada punto se hace explícito lo que estaba implícito, para que el receptor interprete menos y ejecute más, y para que las decisiones se tomen donde hay contexto para tomarlas bien, no por descarte más abajo. No se trata de eliminar todo juicio, sino de no delegarlo por omisión en quien no puede pedir aclaración. *Mira un estado: ¿es este punto lo bastante explícito para quien venga detrás?*

> *Ejemplo.* Un plano de pieza que deja un taladro sin cotar no elimina la decisión: la traslada al taller, que al fabricar elegirá un diámetro cualquiera. La cota no estaba, así que la puso —quizá mal— el eslabón peor situado para decidirla.

> *Con IA.* Se le pide a un agente «una tabla de clientes» sin decir qué columnas. No pregunta: inventa un conjunto plausible y sigue. La ambigüedad no se detuvo, la resolvió él —y quizá no como querías—.

### 2 · Enriquecimiento acumulativo
La información no solo atraviesa las etapas sin cambiar: en cada parada se traslada, se amplía con más detalle y se valida, sin descartar nada de lo ya fijado. Cada parada añade sobre la anterior. Es una propiedad de la trayectoria completa, no de un punto: la cadena debe hacerse más rica al avanzar, nunca perder fidelidad ni volver a derivar lo que ya estaba resuelto. *Mira la trayectoria: ¿la secuencia solo gana, nunca pierde?*

> *Ejemplo.* Un guion pasa a storyboard y luego a rodaje: cada etapa añade encuadre, luz e interpretación, pero ninguna reescribe en secreto los diálogos ya aprobados. Si el rodaje necesita cambiar una línea, no la borra por su cuenta: la devuelve al guion.

> *Con IA.* A un agente se le da una estructura ya acordada para que la amplíe con detalle. Añade lo nuevo, pero no rebautiza ni recorta lo ya fijado para «mejorarlo»: si algo cerrado debe cambiar, lo devuelve en vez de reescribirlo a escondidas.

### 3 · Validación
Nada se trata como consolidado hasta que un juicio lo valida. Conviene separar dos actos que a menudo se confunden: la **verificación** comprueba mecánicamente que algo cumple los criterios declarados; la **validación** juzga que es lo correcto respecto a la intención, parte de la cual nunca llegó a escribirse como criterio. Un **agente puede verificar** —ejecutar las comprobaciones— pero **no validar**: la verificación es necesaria pero no suficiente, puede dar todo en verde y el resultado seguir siendo el equivocado. Por eso el cierre de cada etapa reserva el juicio a una **validación humana**, no a las comprobaciones automáticas.

> *Ejemplo.* Un texto pasa el corrector ortográfico sin una sola marca (verificación) y aun así dice lo contrario de lo que su autor quería (falla la validación). Que no salten alertas no garantiza que el sentido sea el correcto.

> *Con IA.* Un agente entrega un resultado que supera todas las comprobaciones automáticas (verifica) y aun así resuelve mal lo pedido, porque el criterio que de verdad importaba nunca se escribió. Hace falta que un humano lo mire (valide).

### 4 · Trazabilidad
El camino que llevó hasta el conocimiento es reconstruible en ambos sentidos y sin huecos: todo elemento del resultado puede seguirse hacia atrás hasta la decisión o la fuente que lo originó, y toda decisión de origen hacia delante hasta dónde aterrizó. Incluye su dimensión temporal —de qué deriva cada cosa y en qué versión—, lo que permite detectar cuándo un derivado ha quedado desfasado respecto a su fuente. No es documentar por documentar: es lo que hace la cadena auditable y corregible, porque cuando algo falla aguas abajo se puede localizar dónde entró —incluida cada decisión que un agente tomó por su cuenta, que sin rastro quedaría invisible—. Emerge de los tres anteriores —una cadena que reduce ambigüedad, solo enriquece y valida cada paso es, por construcción, rastreable— y cierra el conjunto.

> *Ejemplo.* Cuando una pieza defectuosa aparece al final de una línea de montaje, su número de lote permite retroceder hasta el turno, la máquina y el material que la produjeron. Sin ese rastro, el defecto es indiagnosticable y solo queda descartar el lote entero.

> *Con IA.* Un agente eligió por su cuenta, tres pasos atrás, cómo formatear las fechas. Si esa decisión quedó registrada, se localiza y se corrige **en su origen** —el documento donde se anotó—. Si no, no hay forma de rastrearla hasta quién la tomó ni por qué; y si la parcheas con una **instrucción nueva** de formato sin tocar la vieja, ambas quedan vivas: **dos instrucciones contradictorias conviviendo**.

---

## §2 · Morfología del proceso
> La **dinámica**: cómo se consolida el conocimiento a lo largo del tiempo, sobre las unidades intuitivas (proceso → fases → tareas). Cada norma se ancla a un principio de §1.

- **Avance en cascada con iteración** — cerrar una etapa **validada** antes de abrir la siguiente; iterar dentro de la etapa hasta que está bien; re-iterar la cadena cuando aparece alcance nuevo.
- **Paradas que validan · ejecución que verifica** — la **tarea** verifica (mecánico); la **parada** valida (juicio) y es **forzadora**: no cierra con un conflicto marcado sin escalar. *(Ancla en P3; niveles y ciclo concretos en §3.)*
- **Retroactividad** — volver a una etapa cerrada es **normal**: corregir en el **origen**, dejar **rastro**, evaluar **impacto hacia delante** y **recolocar** el punto del proceso.
- **Dirección y autoridad de las decisiones** — cada tipo de decisión tiene un **origen autoritativo único**; desciende desde él y **no se muta lateralmente**; quien necesite cambiarla la **devuelve al origen** (→ retroactividad). *[P6]*
- **Registro y versión** — la **práctica que realiza la trazabilidad**: anotar **en el momento** (no reconstruido al final) y **reconciliar** contra la guía al cerrar la etapa. *(La mecánica concreta —numeración, clasificación/escalada— es tier-2.)*

---

## §3 · Estructura del proceso
> La **arquitectura**: cómo el proceso se organiza en unidades anidadas con **contexto propio** y cómo se gobiernan sus **fronteras**. §2 describe el *movimiento*; aquí se definen las *unidades* y los *cierres* donde ese movimiento se detiene y consolida.

### Anatomía: proceso → capa → fase → tarea
El proceso se descompone en unidades anidadas de grano decreciente:

- **Proceso** — la cadena completa, de la primera fuente al resultado final.
- **Capa** — un **subproceso ligado a un instrumento y contexto propios**, con su medio y su tipo de resultado; típicamente, el ámbito donde un agente trabaja con su propio contexto. Una capa **no comparte estado** con las demás —el contexto de una no alcanza a otra—: lo que se establece dentro de una no lo conoce otra salvo que se le **transmita**. Por eso cada capa queda **delimitada por dos contratos** —uno de **entrada** (lo que debe llegarle para operar) y uno de **salida** (lo que entrega a la capa siguiente)—, mantiene un **registro interno** mientras trabaja —lo que ocurre dentro no es visible fuera, así que debe anotarse o se pierde la traza— y, al cerrarse, **sincroniza con el resto del proceso** —propaga lo decidido para que el conocimiento común no quede desfasado—. *(Qué instrumento concreto encarna cada capa es tier-2.)*
- **Fase** — cada bloque **ordenado** dentro de una capa, con un **objetivo** propio. **Cuáles son las fases —y cuántas— no lo fija el método**: las determina la **naturaleza del proceso** al que se aplica la metodología (tier-2). Lo que el método fija es la *forma*: una secuencia ordenada donde cada fase **incrementa la definición** sobre la anterior (enriquecimiento acumulativo aplicado a la secuencia), y por eso van numeradas.
- **Tarea** — cada **acción validable** dentro de una fase. **Cuántas tareas tiene una fase no lo fija el proceso**: las determina el **proyecto concreto** (tier-3) al ejecutar sobre él la metodología aplicada, y se **calculan al abrir la fase**.

### Ciclo de trabajo: analizar → planificar → ejecutar/verificar → validar/iterar → cerrar
Dentro de una fase, el **agente** recorre este ciclo, con el **humano** validando en los puntos marcados:

1. **Análisis de información** — antes de planificar, el agente cruza la **metodología aplicada** (tier-2, el método de esta capa) con las **instrucciones y datos del proyecto** para esta capa (tier-3): de ese cruce sale qué exige la fase y con qué material se cuenta.
2. **Planificación** — con eso, el agente **calcula el plan** (qué tareas, de qué tipo) y lo somete a **validación** antes de ejecutar nada.
3. **Ejecución y verificación** — el agente resuelve cada tarea y la **verifica** contra sus criterios (comprobación mecánica).
4. **Validación e iteración** — el **humano** juzga el resultado y se itera hasta el visto bueno (verificación ≠ validación, §1·3).
5. **Cierre de tarea** — la tarea queda validada. Cierre ligero, sin registro.

### Niveles de cierre: tarea · fase · capa
Los cierres **anidan** en tres niveles de refuerzo creciente. Lo que los separa es qué consolidan:

- **Cierre de tarea** — validación de una sola acción. **Sin registro.**
- **Cierre de fase** — el **gate**: cuando las tareas de la fase se dan por **terminadas** y su conocimiento por **consolidado**, se valida el conjunto, se **registran las acciones tomadas** en esas tareas y se transita a la fase siguiente. El registro ocurre aquí, no en cada tarea, porque es donde hay **visión de conjunto**.
- **Cierre de capa** — gate **reforzado**: además del registro, **comprueba versiones** y **coherencia con el resto de capas** antes de cruzar la frontera hacia la capa siguiente.

### Contratos entre capas y suficiencia del traspaso
Como cada capa vive en su propio contexto, el paso de una a otra se gobierna por un **contrato**: qué debe **cruzar** la frontera. El contrato transporta el **resultado consolidado**, no el camino para llegar a él.

De ahí el principio que lo sostiene, la **suficiencia del traspaso** *(§1 lo trata como propiedad; aquí es su instrumento)*: el receptor **opera solo sobre lo que cruza** —no comparte el contexto del emisor—, y cuando ese receptor es un **agente en contexto limpio**, que no ha visto nada del trabajo previo, **solo existe para él lo que está escrito en el traspaso**. Así que todo lo establecido que sea necesario aguas abajo debe estar **volcado** antes de entregar, esté o no bien decidido: una regla puede estar resuelta y conservada en su capa de origen y, aun así, **perderse si no viaja**. *Conservación ≠ suficiencia*, y el contrato es lo que cierra esa brecha.

> *Ejemplo.* Un cocinero deja su turno y pasa un plato a medias al siguiente. Si escribe la receta completa, el otro la termina igual. Si guarda en la cabeza "sal al final" y no lo anota, el turno siguiente —que no estuvo— sirve el plato soso: la decisión existía y era correcta, pero no cruzó.

> *Con IA.* Un agente en contexto limpio recibe el paquete de la etapa anterior. Si una regla se decidió pero no se escribió en él, para el agente no existe: no vio la conversación donde se acordó, así que la aplicará a su manera o no la aplicará.

---

## §4 · Modos de fallo  *[extraído de un proceso]*

Tres formas típicas en que un proceso por etapas falla:

**Contrabando** — aparece algo que ninguna etapa autorizó —un agente introduce un patrón, una dependencia o una decisión que nadie pidió—. No es malo en sí: puede revelar un requisito real que emergió durante el trabajo. Lo decide el registro: **hallazgo sano** si queda anotado, **deuda silenciosa** si no.

> *Ejemplo.* Un albañil añade una viga que el plano no preveía porque la estructura la pedía. Si lo anota en el plano, es un hallazgo sano —el diseño estaba incompleto—; si no dice nada, quien luego se fíe del plano tendrá una casa que no coincide con su documentación.

> *Con IA.* Un agente, al resolver una tarea, incorpora una herramienta o un patrón que nadie pidió porque «le venía bien». Si lo anota, es un hallazgo; si no, queda una decisión que nadie tomó ni revisó.

**Deriva** — se pierde o se contradice algo ya cerrado aguas arriba —el agente se aparta de una decisión fijada, a menudo sin advertirlo—. Es el reverso del enriquecimiento acumulativo: en vez de conservar y añadir, la cadena pierde fidelidad.

> *Ejemplo.* Un patrón de costura fija el largo de la manga. Al cortar la tela, alguien la acorta un poco para aprovechar el retal y no lo anota. La prenda final no coincide con el patrón aprobado, y la decisión de acortarla no consta en ningún sitio.

> *Con IA.* Una instrucción ya cerrada reaparece alterada varios pasos después porque al agente le pareció mejor, sin avisar. Lo fijado quedó contradicho en silencio.

**Incoherencia** — dos piezas producidas en paralelo no encajan: dos agentes (o dos ramas del trabajo) deciden distinto desde el mismo encargo y sus resultados no casan. Solo posible donde hay trabajo paralelo, no en cascada.

> *Ejemplo.* Dos equipos diseñan cada mitad de un puente desde el mismo encargo, pero eligen alturas de barandilla distintas. Cada mitad es correcta por separado; al unirlas, no coinciden.

> *Con IA.* Dos agentes trabajan en paralelo desde el mismo encargo, pero cada uno interpreta una convención a su manera. Cada resultado es correcto por separado; juntos, no casan.

**Línea divisoria de los tres:** el **registro**. Lo registrado es auditable y corregible; lo no registrado es deuda invisible.

---

## §5 · Madurez de las reglas
> Ortogonal a los tres registros; se aplica de forma mínima mientras la metodología no madura en práctica.

- **Tres niveles:** confirmado (>1 caso) · respaldado (1 caso) · hipótesis (sin evidencia propia).
- **Dos ejes:** *respaldo externo/clásico* vs. *extraído de este proceso*.
- **Hoy:** nada confirmado; el núcleo procede de un solo proceso.
