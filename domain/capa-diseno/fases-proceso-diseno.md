# Fases — proceso de la capa de diseño

**Versión:** v0.2 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** metodologia-capa-diseno.md v0.22 (el método que gobierna estas fases), tareas-proceso-diseno.md v0.1 (renombrado y remapeado a fases).
**Tier:** 2 (capa `diseno`).

> **Qué es.** El **listado ejecutable** del proceso de diseño: las **fases numeradas y en orden**. Se recorre fase a fase; el orden importa (cada fase incrementa la definición sobre la anterior).
> **Fase vs. tarea.** Aquí se definen las **fases** (fijas, con su objetivo y su gate). Las **tareas** concretas de cada fase —una única, en cascada o iterativas— **no** se listan aquí: se **calculan por proyecto** (tier 3) al abrir la fase, dentro de su ciclo de vida (ver `metodologia-capa-diseno §4`).
> **Qué NO es.** No explica el método. El *por qué* del orden, el ciclo de vida, la retroactividad y las reglas viven en `metodologia-capa-diseno`. Aquí **solo** el listado. Si algo no cabe en un campo de la plantilla, pertenece a la metodología.
> **Plantilla de cada fase:** nombre · objetivo · resultado · requisitos de entrada · recomendaciones · verificación antes de validar. *(El objetivo y la verificación son de fase — es donde está el gate.)*

---

### F1 · Sistema de diseño
- **Objetivo:** establecer o importar el DS base sobre el que se construye todo.
- **Resultado:** un DS con dos capas de tokens (primitivos + semánticos) que cubre el alcance mínimo, y todo DS ajeno saneado.
- **Requisitos de entrada:** la definición del proyecto + el alcance mínimo del DS (`spec-ds`); identificar cualquier DS ajeno vinculado.
- **Recomendaciones:** si hay un DS de framework adecuado, preferirlo a autorar uno desde cero; sanear explícitamente cualquier DS ajeno **antes** de empezar.
- **Verificación antes de validar:** ¿cubre el alcance mínimo (color · tipografía · espaciado · estados base)? ¿están las dos capas de tokens? ¿sin contaminación de un DS ajeno?
- **Tareas:** normalmente única.

### F2 · Esquema de navegación
- **Objetivo:** fijar qué pantallas existen y cómo se transita entre ellas.
- **Resultado:** mapa de pantallas + transiciones con sus disparadores.
- **Requisitos de entrada:** la definición (historias de usuario, arquitectura de información) + el DS (F1).
- **Recomendaciones:** derivar del flujo de las historias de usuario; no inventar pantallas que la definición no soporta.
- **Verificación antes de validar:** ¿los flujos cubren las historias de usuario? ¿sin pantallas inalcanzables ni acciones sin destino?
- **Tareas:** normalmente única.

### F3 · Wireframes
- **Objetivo:** la estructura y jerarquía de cada vista, sin estilo.
- **Resultado:** wireframes trazables a la definición, con los estados no-felices (vacío · carga · error) cubiertos.
- **Requisitos de entrada:** el esquema de navegación (F2) + la definición.
- **Recomendaciones:** trabajar por prompt; **no editar los wireframes a mano en el lienzo** (no deja registro). Cubrir los estados no-felices, no solo el camino feliz.
- **Verificación antes de validar:** ¿la estructura responde a la definición? ¿están todos los elementos necesarios y su orden es correcto? ¿los tres estados no-felices?
- **Tareas:** iterativas si conviene (una por vista o grupo de vistas), según el proyecto.

### F4 · Componentes
- **Objetivo:** los componentes compartidos completos, cada uno con su ficha.
- **Resultado:** cada componente en alta fidelidad + su **ficha completa** (nativo decidido, tokens semánticos, estados renderizados, comportamiento), **sin nada "pendiente"**.
- **Requisitos de entrada:** los wireframes (dónde aparece cada patrón) + el DS + `spec-componente`.
- **Recomendaciones:** cerrar cada componente entero antes de pasar al siguiente; consumir solo tokens semánticos; clasificar y registrar cualquier divergencia del DS.
- **Verificación antes de validar:** ¿cada ficha está completa? ¿los componentes nativos están decididos? ¿las divergencias del DS clasificadas y registradas?
- **Tareas:** **iterativas** — una por componente (el número lo fija el proyecto).

### F5 · Vistas
- **Objetivo:** componer las vistas con componentes ya spec'd.
- **Resultado:** cada vista en alta fidelidad + su ficha (si la requiere), **referenciando** componentes sin redefinirlos.
- **Requisitos de entrada:** los componentes con ficha (F4) + los wireframes de las vistas + `spec-vista`.
- **Recomendaciones:** no incluir en una vista ningún componente sin ficha; referenciar los componentes, no redibujarlos.
- **Verificación antes de validar:** ¿ninguna vista incluye componentes sin ficha? ¿cada vista responde a su wireframe y a la navegación?
- **Tareas:** **iterativas** — una por vista.

### F6 · Prototipo navegable y handoff
- **Objetivo:** cerrar la capa y producir el paquete que baja a implementación.
- **Resultado:** prototipo navegable + **paquete de handoff válido** (según el criterio de aceptación del paquete, en `spec-vision-general`), con versiones comprobadas.
- **Requisitos de entrada:** todas las vistas listas (F5) + todas las specs completas + el contrato de handoff.
- **Recomendaciones:** comprobar el criterio de aceptación del paquete (`spec-vision-general`) antes de entregar; es un salto de capa (comprobar versiones y coherencia).
- **Verificación antes de validar:** ¿el paquete cumple el criterio de aceptación (un lector sin esta conversación se apaña)? ¿las versiones están al día?
- **Tareas:** cascada (prototipo → verificación → handoff).
