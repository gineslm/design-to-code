# Metodología aplicada — visión general del proceso

**Versión:** v0.5 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-global.md v0.4, metodologia-sintesis.md (esquema), entrada-decisiones-2026-08-06.md (bloque L), decisiones-consolidacion.md v0.4.
**Ubicación:** `core/` · **Reconvertida** de "raíz operativa de tier 2" a **visión general de las tres capas**: el detalle operativo ya no vive aquí, sino embebido en cada documento de capa (autosuficiente).

> **Qué es.** La **visión general** de nuestro proceso —tres capas: **definición → diseño → implementación**—. Describe cómo encajan: sus roles, cómo fluye el trabajo entre ellas, el ciclo común con que se conduce cada una y cómo se gobierna. **No define el detalle operativo** de ninguna capa (eso vive en su documento). Instancia el núcleo de `metodologia-global` en este proceso concreto.

---

## 1 · Las tres capas y sus roles

Cada capa tiene un rol que no invade el de las otras; mezclarlos es el origen de la mayoría de los fallos entre capas.

- **Definición** — razona, documenta y **orquesta**. Es la **fuente de las decisiones** de requisito y alcance: produce la especificación de *qué* construir y con qué restricciones.
- **Diseño** — vuelve esa definición **forma visual**. No decide requisitos; lo que la definición no cubre, se devuelve hacia arriba.
- **Implementación** — vuelve el diseño **código**, fiel a la spec, sin introducir ni perder nada.
- **Frontera de plataforma:** la capa de diseño no produce código ejecutable; entrega diseño + mapeo, y la de implementación construye.

## 2 · Principio de gobierno

La **definición es la fuente única de decisiones** de requisito y alcance: cuando algo debe cambiar, cambia **ahí** y **desciende**; nunca se decide lateralmente en una capa inferior. Si diseño o implementación decidieran requisitos por su cuenta, las capas se desalinearían y la definición quedaría como un **fósil** que aparenta vigencia.

La dirección inversa es legítima —una decisión de una capa inferior que actualiza lo que fijó una superior— pero solo si **se registra y se propaga** hacia arriba (ver §5).

## 3 · Cómo fluye el proceso

- **Topología:** en **definición**, varios hilos en **paralelo** (research, entidades, historias de usuario, perfil técnico…) que **convergen** al cerrar la capa; en **diseño** e **implementación**, **cascada**.
- **Transiciones entre capas, gobernadas por contratos** (tres flujos):
  - **Definición → Diseño:** el **briefing**.
  - **Definición → Implementación:** el **perfil técnico** (baja al repo y **crece desde la implementación**; bidireccional).
  - **Diseño → Implementación:** el **handoff** (paquete ampliado; la implementación lo lee y se orienta).
- **Criterio de suficiencia:** un receptor sin acceso al historial debe poder operar **solo** con lo que el contrato transfiere.
- **Coherencia cruzada:** por el paralelismo, el cierre de la capa de definición verifica que sus hilos **no se contradigan** entre sí.
- **Bidireccional:** `im` (diseño→código) y `ex` (código→diseño, pendiente). **Reenganche:** importar un diseño existente como origen alternativo.

## 4 · El ciclo común (fase · tarea · gate)

Cada capa organiza su trabajo en una **secuencia de fases**. Cada **fase** se resuelve con **una o varias tareas** (calculadas por proyecto según complejidad) y se cierra en un **gate** que **valida y registra** — reforzado en el **salto de capa** (comprueba versiones y coherencia).

Toda fase sigue la **meta-plantilla de procedimiento**: **contexto → alcance → requerimiento → definición/implementación → validación → registro → retorno al contexto** (circular). El retorno al contexto es donde el registro se propaga hacia arriba y cierra el ciclo.

**El *cómo* el agente conduce cada fase** (ciclo de vida, checkpoints, rol de guía) está **embebido en cada documento de capa**, que es autosuficiente. Aquí solo se describe el **patrón común**; no se define.

## 5 · Retroactividad — dos direcciones

Revisar hacia atrás lo ya cerrado es normal (principio en `metodologia-global`). En este proceso se da en dos direcciones:

- **Entre capas:** una decisión de una capa inferior que **actualiza o supera** lo que fijó una superior → se **registra y se propaga hacia arriba**, o la superior queda desfasada. Es el gobierno inverso (§2).
- **Entre fases** (dentro de una capa): una fase posterior revela que una anterior ya cerrada **debe revisarse** → vuelve a su **fase dueña**, deja rastro, y se **evalúa el impacto hacia delante**, recolocando el proceso donde el cambio obligue.

Registrada y reconciliada = sana; corregir el origen sin propagar/reconciliar = deriva.

## 6 · Mapa de derivación

- **Cadena:** `metodologia-global` (universal) → **esta visión general** → **un documento por capa** (autosuficiente) + sus **specs** + sus **contratos**.
- **Simetría:** las tres capas tienen documento propio; ninguna se gobierna solo desde aquí.
- **Lo que baja (tier 3):** definición + briefing → specs + handoff → código + registro + informe.
- **Nomenclatura:** nombres completos y **agnósticos de herramienta**.
