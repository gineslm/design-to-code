# Design to Code

> Investigación aplicada sobre cómo estructurar procesos asistidos por agentes de IA para que sean trazables, reproducibles y suficientemente definidos antes de llegar a implementación.

Este repositorio nació de una pregunta concreta:

> **¿Cuánto del trabajo de convertir diseño en código puede delegarse en agentes de IA, y con qué garantías?**

La investigación empezó en el flujo **documentación → diseño/prototipado → implementación frontend**, pero durante las pruebas aparecieron hallazgos más generales: el rendimiento del proceso dependía menos de «pedirle más» al agente y más de **cómo estaba definido, encadenado y validado el trabajo**.

De ahí surgieron dos resultados distintos:

1. una **metodología de procesos por etapas**, formulada primero desde el caso design-to-code y abstraída después como núcleo reutilizable;
2. un problema de segundo orden —la coordinación entre múltiples contextos que no comparten memoria— que abrió una línea arquitectónica propia y más tarde dio origen a **Warp**.

Este repositorio conserva la investigación, la metodología derivada y su aplicación al proceso de diseño → código.

---

## 1. La pregunta de partida

El objetivo inicial tenía dos frentes:

- evaluar cuánto podía automatizarse de la conversión de diseño a código;
- estudiar un flujo de diseño y prototipado asistido por IA con suficiente control y fidelidad.

El proceso estudiado se organizó en tres capas:

```text
definición
   ↓
diseño
   ↓
implementación
```

La hipótesis operativa era que cada capa podía apoyarse en agentes distintos siempre que las transiciones entre ellas estuvieran suficientemente especificadas.

La investigación se realizó sobre un caso real de frontend en Angular, comparando distintos modos de transferencia desde herramientas de diseño y ejecutando varias conversiones del mismo proyecto.

---

## 2. Qué se probó

Las pruebas no buscaban únicamente comprobar si un agente podía generar código. Buscaban aislar **qué condiciones hacían el proceso fiable y reproducible**.

### Prueba A — conversión en bruto

Importación directa de una vista para observar qué producía el sistema sin una metodología desarrollada alrededor.

Sirvió como diagnóstico inicial.

### Prueba B — conversión completa con contexto acumulado

Se ejecutó el flujo completo:

```text
estilos
→ componentes compartidos
→ esqueleto de aplicación
→ páginas
→ navegación
```

La ejecución alcanzó el objetivo funcional planteado y sirvió para consolidar el procedimiento.

### Prueba C — replicabilidad sin historial conversacional

La misma conversión se ejecutó mediante un agente que sólo disponía de:

- documentación;
- repositorio;
- artefactos del proceso.

No disponía del historial de conversación de las pruebas anteriores.

Esta prueba permitió estudiar si el método podía sostenerse en **artefactos persistentes**, en lugar de depender de memoria conversacional.

### Prueba D — conversión ciega con el método corregido

Tras detectar pérdidas de fidelidad visual en C se añadió un control visual al procedimiento y se repitió la ejecución.

El resultado fue especialmente útil porque **no mejoró de forma sustancial la fidelidad**.

Eso permitió descartar que el problema estuviera únicamente en el tramo final de conversión y desplazar el análisis aguas arriba.

---

## 3. Hallazgo principal: la definición condiciona el resultado

Las pruebas apuntaron a una conclusión operativa:

> **mejorar sólo la conversión no basta si las especificaciones que llegan a implementación siguen siendo incompletas.**

La fidelidad del resultado dependía directamente de la calidad de los artefactos previos:

- documentación;
- definición funcional;
- especificaciones de diseño;
- contratos entre etapas;
- fichas de componente.

El cuello de botella identificado fue, por tanto, el **contrato de especificación entre diseño e implementación**.

La consecuencia fue importante: el problema dejó de ser simplemente «cómo generar mejor código» y pasó a ser «cómo preparar un proceso para que un agente tenga que interpretar lo mínimo posible en cada transición».

---

## 4. De las pruebas a una metodología

De la investigación se extrajo un conjunto de principios que podían formularse con independencia del caso concreto.

El núcleo vive en:

[`core/metodologia-global.md`](core/metodologia-global.md)

Ese documento se define como un **núcleo agnóstico para procesos de transformación por etapas**. Su grado de universalidad se mantiene explícitamente acotado: parte de un único proceso y distingue entre reglas confirmadas, respaldadas e hipótesis.

Los principios principales son:

### Trazabilidad

Todo resultado debe poder seguirse hacia atrás hasta la decisión o fuente que lo originó, y toda decisión debe poder seguirse hacia delante hasta donde aterriza.

### Versionado y linaje

Los artefactos derivados deben permitir detectar cuándo quedan desfasados respecto a sus fuentes.

### Reducción de ambigüedad

Cada fase debe hacer explícito lo que estaba implícito para que el actor aguas abajo **interprete menos y ejecute más**.

### Reutilización y consistencia

Los patrones repetidos deben definirse una vez y reutilizarse, en lugar de duplicarse y divergir.

### Cascada con iteración

Una fase se valida antes de construir sobre ella, pero puede iterarse internamente y revisarse si aparece conocimiento nuevo.

### Retroactividad

Volver a una fase cerrada no se considera un fallo. Si una fase posterior descubre un problema aguas arriba, se corrige en origen, se registra y se evalúa su impacto hacia delante.

### Enriquecimiento acumulativo

Cada fase añade información sin perder lo ya establecido.

### Método constante, fuente variable

El método debe poder mantenerse estable mientras cambia el proyecto al que se aplica.

---

## 5. Gates y validación humana

La metodología introduce puntos explícitos de parada.

No todos tienen el mismo alcance:

```text
tarea
  ↓
parada de contenido

fase
  ↓
gate de consolidación

cambio de capa
  ↓
gate reforzado
```

El propósito del gate no es añadir burocracia, sino impedir que un error o una contradicción siga propagándose silenciosamente.

La validación humana forma parte del modelo: el cierre de una fase no se reduce a una comprobación mecánica porque el contenido necesita juicio.

---

## 6. La metodología aplicada al flujo Design to Code

La aplicación concreta del núcleo vive en:

[`core/metodologia-aplicada.md`](core/metodologia-aplicada.md)

La metodología aplicada organiza el proceso en tres capas con responsabilidades distintas.

### Definición

Razona, documenta y orquesta.

Es la fuente de las decisiones de requisito y alcance.

### Diseño

Transforma la definición en forma visual.

No debería introducir requisitos nuevos silenciosamente: los huecos deben devolverse hacia arriba o registrarse.

### Implementación

Transforma diseño y especificaciones en código.

Su responsabilidad es implementar con fidelidad, no redefinir requisitos o diseño por defecto.

El principio de gobierno es:

> **las decisiones deben tomarse donde existe el contexto para tomarlas.**

Una capa inferior puede descubrir algo que obligue a revisar una superior, pero ese cambio debe registrarse y propagarse.

---

## 7. Contratos entre capas

Las transiciones no se tratan como simples entregas de archivos.

Funcionan como **contratos** que deben permitir que el receptor opere sin necesitar el historial conversacional del emisor.

En el modelo actual:

```text
Definición ──briefing──→ Diseño

Definición ──perfil técnico──→ Implementación

Diseño ──handoff──→ Implementación
```

La prueba fuerte de suficiencia es:

> **¿puede un receptor sin acceso al historial ejecutar correctamente usando sólo lo que cruza la frontera?**

Ese criterio fue precisamente el que motivó las pruebas con agentes «ciegos».

---

## 8. Artefactos de diseño y especificación

El repositorio contiene además una capa específica de diseño y una familia de specs que materializan el contrato diseño → implementación.

Entre ellas:

- `spec-app.md`
- `spec-componente.md`
- `spec-ds.md`
- `spec-entidades.md`
- `spec-navegacion.md`
- `spec-vision-general.md`
- `spec-vista.md`

Estas fichas no son un catálogo decorativo: intentan reducir la cantidad de decisiones implícitas que quedarían en manos de implementación.

La investigación actual señala precisamente esta frontera como el principal ámbito que todavía necesita madurar.

---

## 9. Registro, deriva y modos de fallo

La metodología identifica tres modos de fallo relevantes:

### Contrabando

Aparece una decisión que ninguna etapa había autorizado.

Puede ser un hallazgo legítimo, pero debe registrarse.

### Deriva

Se pierde o contradice algo ya validado aguas arriba.

### Incoherencia

Dos piezas producidas en paralelo dejan de encajar entre sí.

En los tres casos, el registro es la diferencia entre un cambio auditable y una deuda invisible.

Por eso las decisiones que aparecen durante el proceso no deberían quedar únicamente en una conversación.

---

## 10. Madurez: qué sabemos y qué no

Este repositorio distingue deliberadamente entre:

- **confirmado** — demostrado por evidencia suficiente dentro de la investigación;
- **respaldado** — apoyado por la evidencia disponible, pero todavía no cerrado;
- **hipótesis** — plausible, pendiente de probar.

Entre los resultados actuales:

- el flujo asistido por agentes es viable de extremo a extremo;
- las pruebas respaldan que la calidad de documentación y especificaciones condiciona directamente la fidelidad;
- mejorar únicamente la conversión no resolvió las desviaciones;
- el contrato diseño → código sigue siendo el principal ámbito pendiente;
- la extrapolación del núcleo metodológico a otros procesos sigue siendo una hipótesis, porque todavía se ha probado sobre un único dominio.

Este repositorio debe leerse como **investigación en evolución**, no como un estándar terminado.

---

## 11. El problema que la metodología no resolvía

Mientras se desarrollaba la investigación apareció un problema diferente.

El trabajo empezó a repartirse entre múltiples conversaciones y herramientas:

- unas investigaban;
- otras ejecutaban pruebas;
- otras consolidaban metodología;
- otras trabajaban diseño o implementación.

Esos contextos no compartían memoria.

La consecuencia era que el conocimiento del proyecto quedaba repartido y podía desincronizarse.

El primer intento de modelar este problema vive en:

[`core/arquitectura-de-contextos.md`](core/arquitectura-de-contextos.md)

Ese documento está marcado explícitamente como **exploratorio**. Describe un mecanismo inicial basado en:

- documentos-puente;
- responsabilidades de edición;
- estados;
- retorno de información;
- sincronización humana.

No forma parte del núcleo metodológico maduro.

Fue la señal de que había aparecido un problema de otro nivel.

---

## 12. De aquí nace Warp

La metodología responde principalmente a:

> **¿cómo debe avanzar y validarse un proceso asistido por agentes?**

La nueva pregunta era:

> **¿cómo se mantiene conocimiento y responsabilidad coherentes cuando varias instancias trabajan sobre ese proceso sin compartir memoria?**

Esa segunda pregunta se separó posteriormente de este repositorio y evolucionó como una investigación arquitectónica propia:

**Warp — arquitectura de conocimiento para colaboración humano–IA**

Warp desarrolla ese problema alrededor de ideas como:

- responsabilidades persistentes;
- THREADs;
- MANIFESTs;
- HANDOFFs;
- autoridad documental;
- corpus común;
- agentes intercambiables;
- Git como historia del conocimiento;
- carga progresiva de contexto;
- validación estructural.

Design to Code y Warp son por tanto proyectos relacionados, pero no equivalentes:

```text
Design to Code
→ investiga un proceso
→ extrae una metodología
→ descubre un problema de coordinación

Warp
→ toma ese problema
→ lo abstrae
→ desarrolla una arquitectura de conocimiento
```

**Repositorio de Warp:** añadir enlace cuando esté publicado.

---

## 13. Estructura del repositorio

```text
.
├── core/
│   ├── metodologia-global.md
│   ├── metodologia-aplicada.md
│   ├── arquitectura-de-contextos.md
│   └── convenciones-repo.md
│
├── domain/
│   └── capa-diseno/
│       ├── metodologia-capa-diseno.md
│       ├── fases-proceso-diseno.md
│       └── spec/
│           ├── spec-app.md
│           ├── spec-componente.md
│           ├── spec-ds.md
│           ├── spec-entidades.md
│           ├── spec-navegacion.md
│           ├── spec-vision-general.md
│           └── spec-vista.md
│
├── metodologia-sintesis.md
├── decisiones-consolidacion.md
├── entrada-decisiones-2026-08-06.md
└── CONTEXT_GIT.md
```

La estructura refleja tres niveles distintos:

```text
núcleo metodológico
        ↓
aplicación al proceso
        ↓
artefactos específicos de cada capa
```

---

## 14. Estado

La investigación sigue abierta.

Las líneas pendientes principales son:

1. mejorar el contrato de especificación entre diseño e implementación;
2. completar al mismo nivel las capas de definición y diseño/prototipado;
3. seguir validando qué principios del núcleo son realmente transferibles a otros procesos;
4. separar progresivamente del repositorio los problemas arquitectónicos de contexto que ya pertenecen a Warp;
5. medir en un piloto real impacto en tiempo, coste, consistencia y retrabajo.

---

## Autor

**Ginés López Montalbán**

Frontend / UX-UI · Design Systems · procesos asistidos por IA

---

## Nota sobre el alcance

Este repositorio documenta una investigación y una metodología en evolución.

No pretende presentar como universales conclusiones obtenidas todavía de un único proceso, ni afirmar que el flujo actual elimine la necesidad de criterio humano.

El objetivo es hacer explícitas las decisiones, las pruebas, los límites y el grado de madurez de cada hallazgo.
