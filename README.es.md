# Design to Code

Metodología para trabajar con agentes de IA en procesos por etapas, desarrollada a partir de una investigación práctica sobre cómo llevar un producto digital desde su definición hasta el código.

> Este README está también disponible en inglés → [Read in English](README.md)

---

## 1. Qué es este repositorio

Este repositorio contiene una **metodología**: un conjunto de principios, reglas y plantillas para organizar un proceso de trabajo en el que intervienen agentes de IA, de forma que el resultado sea fiel a lo que se pidió, reproducible y trazable.

La metodología nació de un caso concreto, el paso de **definición → diseño → implementación** de una aplicación web, y está escrita en dos niveles:

- un **núcleo universal** (tier 1), válido para cualquier proceso asistido por IA, con independencia de la herramienta o del proyecto;
- su **aplicación a este proceso** (tier 2): las tres capas, cómo se traspasa el trabajo entre ellas y, con más detalle, la capa de diseño y su sistema de especificaciones.

Lo que el repositorio **no** contiene son datos de un proyecto concreto (lo que en la metodología se llama tier 3), código de aplicación ni herramientas. Es el método que un proyecto adopta, no un proyecto.

**Por dónde empezar.** Si buscas la idea general, este README basta. Si quieres el método, lee primero [`core/metodologia-global.md`](core/metodologia-global.md) y después [`core/metodologia-aplicada.md`](core/metodologia-aplicada.md). Si vas a aplicarlo a la capa de diseño, sigue con [`domain/capa-diseno/`](domain/capa-diseno/).

---

## 2. Qué se quería averiguar

La investigación partió de una pregunta práctica: **¿cuánto del trabajo de convertir un diseño en código puede delegarse en agentes de IA, y con qué garantías?**

Para responderla se estudió un proceso completo en tres capas:

- **Definición**: qué se construye y con qué restricciones (requisitos, entidades, historias de usuario, perfil técnico).
- **Diseño**: la forma visual (sistema de diseño, wireframes, componentes, vistas y prototipo navegable).
- **Implementación**: el código.

La hipótesis de trabajo era que cada capa podía apoyarse en un agente distinto, siempre que el paso de una capa a la siguiente estuviera bien especificado. El caso de estudio fue una aplicación real de frontend en Angular, trabajada con herramientas de diseño y de código asistidas por IA.

---

## 3. Cómo se evaluó

Las pruebas no buscaban comprobar si un agente es capaz de generar código, sino aislar **qué condiciones hacen que el proceso sea fiable**. Cada una cambiaba una variable respecto a la anterior.

- **Prueba A: conversión en bruto.** Se importó una vista directamente desde la herramienta de diseño, sin método alrededor, para ver qué producía el sistema por sí solo. Sirvió de diagnóstico inicial.
- **Prueba B: conversión completa con contexto acumulado.** Se recorrió el flujo entero (estilos, componentes compartidos, estructura de la aplicación, páginas y navegación) con un agente que tenía delante todo el historial de trabajo previo. Alcanzó el objetivo funcional y sirvió para consolidar el procedimiento.
- **Prueba C: conversión ciega.** La misma conversión, pero con un agente **sin acceso al historial**: solo disponía de la documentación del método, el repositorio y el paquete entregado por la capa de diseño. Es lo que en la metodología se llama trabajar en **contexto limpio**, y es la prueba decisiva: si el método funciona, tiene que funcionar con lo que está escrito, no con lo que el agente recuerda de conversaciones anteriores.
- **Prueba D: conversión ciega con el método corregido.** Tras los resultados de C se añadió un control visual al procedimiento de conversión y se repitió el ejercicio.

---

## 4. Qué se comprobó

**El método funciona cuando obliga a no improvisar.** En la conversión ciega, el agente no rellenó los huecos por su cuenta: los registró y consultó cada uno. Lo que estaba escrito de forma explícita en el diseño (textos, atributos de accesibilidad, formatos, comportamiento) llegó al código con alta fidelidad.

**Los tests en verde no garantizan fidelidad.** En C toda la verificación fue compilar y pasar tests; el agente nunca abrió un navegador. Los tests comprobaban texto y comportamiento, no apariencia, y dieron una falsa sensación de corrección. De doce desviaciones visuales, diez correspondían a cosas que **estaban en el diseño y no se trasladaron**. La metodología recoge esta lección como la diferencia entre **verificar** (comprobar mecánicamente) y **validar** (juzgar si el resultado es el correcto).

**Lo que no viaja en el paquete no existe para el agente.** Existía una regla para verificar los cambios de interfaz en el navegador, pero vivía en la configuración general del usuario y no en los documentos que recibió el agente. Un agente en contexto limpio solo aplica lo que está escrito en lo que se le entrega.

**Los fallos nacen aguas arriba y aparecen aguas abajo.** El fondo blanco que mostró la conversión no era un error de implementación: la especificación declaraba un color de superficie distinto del que usaba el prototipo. Del mismo modo, el selector que el agente resolvió con un componente equivocado no estaba tipificado en la especificación, que lo dejaba como «pendiente». La comparación entre B, C y el prototipo lo confirmó: **ninguna de las dos conversiones reprodujo el prototipo**, y cada una ganó y perdió fidelidad en sitios distintos. El problema era del proceso, no del modo ciego.

**El diseño generado con IA cubre bien el camino feliz y deja incompletos los estados de borde**: carga, vacío, error y validación quedaban a medio definir aunque el briefing los exigiera.

**Mejorar la conversión no basta.** La Prueba D añadió control visual a la implementación y la fidelidad no mejoró de forma sustancial. Eso descartó que el problema estuviera en el último tramo y llevó el análisis a lo que llega a ese tramo.

La conclusión de todas las pruebas es la misma: **el agente que implementa solo puede ser fiel a lo que recibe escrito**. Todo lo que el traspaso deja abierto lo resuelve él, en silencio y a su manera. El punto débil del proceso era el **contrato de especificación entre diseño e implementación**.

---

## 5. La solución: las specs como contrato entre diseño e implementación

La respuesta que encontró la investigación es **trasladar a plantillas de especificación (specs) todo el conocimiento que la implementación necesita**, en lugar de dejarlo repartido entre la definición, la investigación, el prototipo y las conversaciones de diseño.

Las specs se rellenan durante la capa de diseño. Recogen lo que viene de la definición (el modelo de datos, los requisitos, las restricciones técnicas) y lo que se decide al diseñar (componentes, estados, tokens, navegación), y lo dejan **determinado y escrito**. El paquete de entrega a implementación (el *handoff*) las transporta completas. Así, el agente que implementa recibe todo lo necesario para **implementar sin interpretar**: las decisiones se toman arriba, donde hay contexto para tomarlas bien, y no por descarte en la conversión.

El sistema tiene siete documentos, en [`domain/capa-diseno/spec/`](domain/capa-diseno/spec/):

| Spec | Qué recoge |
|---|---|
| [`spec-app`](domain/capa-diseno/spec/spec-app.md) | Requisitos globales de la aplicación: listado de componentes, estructura de archivos, decisiones compartidas entre diseño y técnica (p. ej. puntos de ruptura), reglas globales. |
| [`spec-ds`](domain/capa-diseno/spec/spec-ds.md) | Qué debe exponer el sistema de diseño: tokens en dos capas (valores primitivos y nombres semánticos de uso) y su alcance mínimo. |
| [`spec-navegacion`](domain/capa-diseno/spec/spec-navegacion.md) | Pantallas y transiciones (origen → acción → destino). Es la base del enrutado. |
| [`spec-entidades`](domain/capa-diseno/spec/spec-entidades.md) | El modelo de datos. Nace en la capa de definición y se registra aquí para que vistas y componentes lo referencien. |
| [`spec-vista`](domain/capa-diseno/spec/spec-vista.md) | Cada pantalla: qué componentes la forman, layout y responsive, estados, navegación, comportamiento y datos. |
| [`spec-componente`](domain/capa-diseno/spec/spec-componente.md) | Cada pieza reutilizable: componente nativo al que corresponde, propiedades, estados dibujados, tokens, comportamiento y accesibilidad. |
| [`spec-vision-general`](domain/capa-diseno/spec/spec-vision-general.md) | El índice que conecta las anteriores y fija el criterio de aceptación del conjunto. |

Las specs se **anidan** de lo global a lo atómico (aplicación → vistas → componentes → sistema de diseño) y cada nivel referencia al inferior sin repetirlo. Algunas son **moldes** que se rellenan una vez por elemento (cada componente, cada vista) y otras son **hojas de requisitos** que fijan una norma para toda la aplicación.

Tres reglas las hacen eficaces:

- **Se rellenan después del alta fidelidad.** La ficha de un componente se completa cuando sus estados ya están dibujados, de modo que recoge valores reales y no queda nada como «pendiente».
- **Ninguna vista usa componentes sin ficha.** Así no llega a implementación ninguna pieza sin especificar.
- **Los componentes consumen solo tokens semánticos.** Nunca valores crudos, lo que permite cambiar el tema o la marca sin tocar los componentes.

El caso del selector muestra el efecto. Mientras la especificación lo dejaba abierto, la conversión tuvo que elegir un componente y eligió mal. En cuanto la ficha declaró el componente nativo leído del prototipo, la decisión desapareció de la implementación: ya no había nada que interpretar. Como la ficha describe cada componente por su función, sus estados y sus tokens, y declara a qué componente nativo corresponde, puede trasladarse a frameworks distintos sin que la implementación tenga que reinventarlo.

**Criterio de aceptación:** con las siete specs completas, alguien que no ha visto nada del trabajo de diseño tiene todo lo necesario para traducirlo a código.

---

## 6. La metodología que lo sostiene

Las specs funcionan porque se inscriben en un método que decide cuándo se rellenan, quién valida y qué pasa cuando algo no encaja. Ese método está en [`core/`](core/).

**El punto de partida.** Un agente trabaja solo con la información que recibe, y **toda ambigüedad que esa información deja abierta la resuelve él mismo**, sin avisar. Por eso la estrategia no es recortar etapas para ir más rápido, sino completarlas y validarlas una a una, de forma que la información necesaria quede capturada en el proceso antes de que un agente tenga que suplirla.

**Cuatro principios** ([`metodologia-global`](core/metodologia-global.md) §1):

- **Reducción de ambigüedad**: en cada traspaso se hace explícito lo que estaba implícito, para que quien recibe interprete menos y ejecute más.
- **Enriquecimiento acumulativo**: cada etapa añade detalle sin perder ni volver a decidir lo que ya estaba fijado.
- **Validación**: un agente puede verificar, pero el cierre de cada etapa lo valida una persona.
- **Trazabilidad**: todo resultado puede seguirse hasta la decisión que lo originó, y toda decisión hasta donde aterrizó.

**Una estructura** que organiza el proceso en unidades anidadas: **proceso → capa → fase → tarea**. Cada **capa** trabaja con su propio contexto y no comparte memoria con las demás, así que el paso entre capas se gobierna con **contratos** que fijan qué debe cruzar. Dentro de cada fase, el agente analiza, propone un plan, ejecuta y verifica, y una persona valida. Los cierres se refuerzan a medida que se sube de nivel: una tarea se valida, una fase se cierra con un **gate** que registra lo decidido, y una capa se cierra con un gate reforzado que comprueba versiones y coherencia.

**Una dinámica** para cuando las cosas no salen en orden: volver a una fase ya cerrada es normal, siempre que se corrija en su origen, deje rastro y se evalúe a qué afecta hacia delante.

**Su aplicación a este proceso** ([`metodologia-aplicada`](core/metodologia-aplicada.md)) define el papel de cada capa y sus tres contratos: el *briefing* (definición → diseño), el *perfil técnico* (definición → implementación) y el *handoff* (diseño → implementación), que es el que transporta las specs. La capa de diseño, la más desarrollada, tiene su método en [`metodologia-capa-diseno`](domain/capa-diseno/metodologia-capa-diseno.md) y sus seis fases en [`fases-proceso-diseno`](domain/capa-diseno/fases-proceso-diseno.md): sistema de diseño, navegación, wireframes, componentes, vistas y prototipo con handoff.

---

## 7. Alcance

**Desarrollado:**

- el núcleo universal de la metodología;
- la visión general de las tres capas y sus contratos;
- la capa de diseño completa: método, fases y sistema de specs.

**No desarrollado todavía:**

- las capas de definición e implementación no tienen documento propio; su descripción está en la visión general;
- la dirección inversa, de código a diseño, está identificada pero no desarrollada;
- la edición manual en las herramientas sigue siendo un punto ciego para el registro: lo que se cambia a mano sin pasar por el agente no queda anotado.

**Separado en otro proyecto:** la coordinación entre conversaciones y agentes que no comparten memoria. Ver el apartado 10.

**Un límite general:** el núcleo se ha extraído de un solo proceso. La metodología distingue lo que tiene respaldo externo de lo que se ha observado aquí, y no presenta como universal lo que aún no lo es.

---

## 8. Estado actual

La metodología está en **borrador** y sigue evolucionando:

- el núcleo universal está en una versión nueva (v0.5) que reestructura los principios y todavía tiene apartados en redacción;
- la visión general de las capas convive con un documento de síntesis anterior que hay que unificar con ella;
- los trabajos pendientes están en [`evolucion/TAREAS.md`](evolucion/TAREAS.md).

Las líneas abiertas son completar las capas de definición e implementación al nivel de la de diseño, seguir comprobando qué principios del núcleo se sostienen en otros procesos, y desarrollar la dirección de código a diseño.

---

## 9. Cómo está organizado el repositorio

```text
.
├── core/                        método vigente: núcleo y visión general
│   ├── metodologia-global.md
│   ├── metodologia-aplicada.md
│   ├── metodologia-aplicada-sintesis.md
│   └── convenciones-repo.md
├── domain/                      método por capa
│   └── capa-diseno/
│       ├── metodologia-capa-diseno.md
│       ├── fases-proceso-diseno.md
│       └── spec/                sistema de especificaciones
├── evolucion/                   cómo ha llegado a ser el método
│   ├── TAREAS.md
│   ├── decisiones-consolidacion.md
│   └── entrada-decisiones-2026-08-06.md
└── CONTEXT_GIT.md               reglas de versionado con Git
```

- **`core/`** contiene el método vigente: el núcleo universal, la visión general del proceso y las convenciones con que se mantienen los documentos.
- **`domain/`** contiene el método de cada capa. Hoy solo la de diseño.
- **`evolucion/`** no es método: recoge los trabajos pendientes y el registro histórico de las decisiones y pruebas que dieron forma a la metodología. Es útil para entender por qué el método es como es. Ante cualquier discrepancia, manda lo que está en `core/` y `domain/`.

Cada documento lleva una cabecera con su versión, su estado y los documentos de los que deriva. El historial de cambios se guarda en Git, con un commit por decisión.

---

## 10. Relación con Warp

Durante la investigación, el trabajo se repartió entre muchas conversaciones y herramientas que no compartían memoria, y el estado del proyecto empezó a desincronizarse. Ese problema es distinto del que estudia esta metodología: no trata de cómo avanzar y validar un proceso, sino de cómo mantener coherente el conocimiento cuando varios agentes trabajan sobre él a lo largo del tiempo.

Se exploró primero aquí y después se separó en un proyecto propio, **Warp**: una arquitectura de conocimiento basada en Git para coordinar personas y agentes, organizada en líneas de responsabilidad persistentes, con autoridad explícita sobre cada documento.

→ [github.com/gineslm/warp](https://github.com/gineslm/warp)

---

## 11. Licencia y autor

Licencia dual: el código, bajo **MIT**, y la documentación y la metodología, bajo **CC BY-SA 4.0**. Ver [`LICENSE`](LICENSE), [`LICENSE-CODE`](LICENSE-CODE) y [`LICENSE-DOCS`](LICENSE-DOCS).

**Ginés López Montalbán**
Design Engineer · Frontend / UX-UI · Design Systems · procesos asistidos por IA
[Perfil online](https://www.dsigncloud.es/dosier/es/)
