# Tareas

> **Qué es.** Los trabajos **pendientes** del repositorio. Solo recoge el presente abierto: cuando una tarea se completa, se borra de aquí en el mismo commit que la resuelve, y Git conserva su historia.
> **Formato.** Identificador `T-NN` estable · qué hay que hacer · por qué · decisiones previas necesarias · documentos afectados.

---

## T-01 · Unificar `metodologia-aplicada` y `metodologia-aplicada-sintesis`

**Qué.** Fundir los dos documentos de `core/` en un único `metodologia-aplicada` y retirar la síntesis.

**Por qué.** Los dos describen el mismo proceso de tres capas, uno desde el gobierno y otro como mapa, y se solapan en torno a un 40 %. La síntesis tiene contenido que solo está en ella y no debe perderse:
- la tabla de los tres tiers (§1);
- dónde vive el tier 3 y la decisión L.16 de que este repo no lo aloja (§2b);
- las fases de las capas de definición e implementación (§3a), que no tienen documento propio;
- la tabla comparativa de las tres capas (§3b);
- la asimetría de los gates visuales entre diseño e implementación (§3b, Prueba C);
- el andamiaje pendiente.

**Qué no pasa a la versión unificada:**
- el árbol del repo (ya está en el README);
- los modos de fallo (ya están en `metodologia-global` §4);
- las fases de diseño antiguas (se sustituyen por un enlace a F1–F6 de `fases-proceso-diseno`);
- la nomenclatura «T1», «minigate» y «transición»;
- la carpeta pendiente `puentes/` (la cubre Warp).

**Incoherencias que hay que resolver al unificar:**
1. **Topología de diseño:** aplicada dice «cascada» y la síntesis «fases + bucles iterativos». Propuesta: fases en cascada con tareas iterativas dentro (`metodologia-global` §3).
2. **Coherencia entre capas:** aplicada y la síntesis la limitan al cierre de la capa de definición; `metodologia-global` v0.5 la exige en todo cierre de capa.
3. **Ciclo de fase:** la meta-plantilla de aplicada §4 (contexto → … → retorno) frente al ciclo de `metodologia-global` §3 (analizar → planificar → ejecutar/verificar → validar/iterar → cerrar).
4. **Vocabulario de cierres:** «minigate / gate / salto de capa» frente a «cierre de tarea / fase / capa».
5. **Nombre de la tercera capa:** «conversión» (síntesis) frente a «implementación» (aplicada y global).
6. **Referencias rotas en la síntesis:** `metodologia-capa-diseno §7`, `metodologia-capa-conversion §6` y `arquitectura-de-contextos`.
7. **Ámbito de aplicada:** dice que «no define el detalle operativo de ninguna capa», pero tendría que acoger las fases de definición e implementación mientras no exista su documento de capa.

**Decisiones previas:**
- ¿Las fases de definición e implementación entran en aplicada como provisionales o se abre ya un documento mínimo por capa en `domain/`?
- ¿Qué ciclo de fase se mantiene (incoherencia 3)?
- ¿«Implementación» o «conversión»?
- ¿La coherencia entre capas se exige en todo cierre de capa?

**Al cerrarla:**
- Hacer constar en el mensaje del commit (`R-00X`) que se revisa la decisión G de `evolucion/decisiones-consolidacion.md` (línea 113): mantener `metodologia-sintesis` como mapa permanente. Ese documento está congelado y no se edita.
- Actualizar el «Deriva de» de aplicada (global v0.5 + síntesis v0.14 absorbida) y el de `convenciones-repo`.
- Quitar la síntesis de los árboles de carpetas de los dos README.

**Documentos afectados:** `core/metodologia-aplicada.md`, `core/metodologia-aplicada-sintesis.md`, `core/convenciones-repo.md`, `README.md`, `README.es.md`.

---

## T-02 · Pasar a esta lista los pendientes de `decisiones-consolidacion` §H

**Qué.** Revisar uno a uno los pendientes del bloque H de `evolucion/decisiones-consolidacion.md` (congelado). Los que sigan abiertos pasan aquí como tareas propias; los que ya estén resueltos o superados por el método vigente se descartan, dejando constancia en el commit.

**Por qué.** Para que solo haya una lista de pendientes. `decisiones-consolidacion` ya no se amplía.

**Pendientes del bloque H:**
- desarrollar `ex` (código → diseño), separando T0 y la reconciliación de deriva;
- los dos orígenes de T0 (repo de código o Figma);
- el escenario de un proyecto que arranca desde código;
- la plantilla de proyecto nuevo (qué se copia y qué nace vacío);
- las paradas intermedias concretas por capa;
- a dónde va el «aviso suave»;
- la 4ª vía de madurez «propuesta estructural»;
- el contenido exacto del paquete de handoff en frío;
- medir el coste de la autocorrección;
- el agujero de trazabilidad por ediciones manuales, en diseño y en código.

**Documentos afectados:** `evolucion/TAREAS.md`.

---

## T-04 · Decidir si conviven las cabeceras por documento y los commits `R-00X`

**Qué.** Resolver la pregunta abierta de `CONTEXT_GIT.md` (última sección), que también recoge `decisiones-consolidacion` L.15: si conviven el versionado por documento (cabecera `v0.x` y «Deriva de») y el versionado por Git (`R-00X`), o si el segundo sustituye al primero.

**Por qué.** Afecta a `convenciones-repo`, a `CONTEXT_GIT` y al principio de trazabilidad de `metodologia-global`, que incluye «de qué deriva cada cosa y en qué versión». Warp evita mantener un segundo historial sobre Git y declara la procedencia solo cuando aporta significado.

**Documentos afectados:** `core/convenciones-repo.md`, `CONTEXT_GIT.md`.
