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

---

## T-05 · Corregir los fallos internos de `metodologia-global` v0.5

**Qué.** Resolver las incoherencias internas de la nueva versión del núcleo:

1. **Referencia a un principio inexistente.** §2, «Dirección y autoridad de las decisiones», termina en `[P6]`, pero §1 solo tiene cuatro principios. Decidir a cuál se ancla (probablemente P1, reducción de ambigüedad, o P4, trazabilidad).
2. **La suficiencia del traspaso no está en §1.** La cabecera dice que «entra» como principio y §3 dice «§1 lo trata como propiedad; aquí es su instrumento», pero §1 no la recoge. Decidir si es un quinto principio, si se integra en uno de los cuatro (p. ej. en reducción de ambigüedad) o si se corrige la referencia de §3.
3. **Alcance con dos versiones.** §0 reencuadra el núcleo a «cualquier proceso asistido por IA», pero el «Punto de partida» de §1 («válidas para cualquier proceso por etapas») y §4 («un proceso por etapas falla») siguen con el encuadre anterior.
4. **Cuándo se registra.** §2 («Registro y versión») pide anotar «en el momento (no reconstruido al final)», y §3 («Niveles de cierre») dice que el registro ocurre al cerrar la fase y no en cada tarea. Aclarar la relación: por ejemplo, se anota en el momento y se consolida en el gate.
5. **Cabecera:**
   - el «Deriva de» cita `metodologia-capa-diseno` v0.22, pero la vigente es la v0.23;
   - el estado «borrador (en redacción)» no es uno de los tres que admite `convenciones-repo` (`borrador` · `congelado` · `obsoleto`);
   - se declara una reestructuración MAYOR y se numera v0.5. Dentro de borrador la convención lo permite, pero no deja claro si los documentos derivados (`metodologia-aplicada`, `convenciones-repo`, `metodologia-capa-diseno`) quedan desactualizados.

**Además, contenido de la v0.4 que la v0.5 deja sin sitio:**
- la **clasificación de decisiones** (diferido intencional · hueco accidental · conflicto) y la **escalada bifurcada** (instancia → documento del caso; método → metodología). La v0.5 dice que su mecánica es tier 2, pero ningún documento tier 2 la recoge todavía;
- el principio de **reutilización y consistencia**, que sale del núcleo y solo pervive como «divergencia gobernada» del sistema de diseño en `metodologia-capa-diseno`.

Decidir si van a `metodologia-aplicada` (ver T-01), a la capa, o se descartan.

**Documentos afectados:** `core/metodologia-global.md` y, según lo que se decida, `core/metodologia-aplicada.md`.

---

## T-06 · Revisión de coherencia entre la global, la aplicada y la metodología de diseño

**Qué.** Revisar de arriba abajo la cadena `metodologia-global` (tier 1) → `metodologia-aplicada` (tier 2, visión general) → `metodologia-capa-diseno` + `fases-proceso-diseno` (tier 2, capa), y alinearla con la global v0.5: que cada concepto viva en un solo nivel, que los niveles inferiores instancien y no redefinan lo de arriba, y que el vocabulario sea el mismo.

**Por qué.** La global se reestructuró (v0.5) después de que se escribieran la aplicada (v0.5, deriva de global v0.4) y la metodología de diseño (v0.23, deriva de global v0.4). La global absorbe ahora conceptos que antes vivían en los niveles inferiores, y hay solapamientos y contradicciones.

**Puntos ya detectados:**
1. **Ciclo de fase duplicado y distinto.** La global §3 define el ciclo (analizar → planificar → ejecutar/verificar → validar/iterar → cerrar); la aplicada §4 mantiene la meta-plantilla (contexto → alcance → requerimiento → … → retorno), y `metodologia-capa-diseno` §4 tiene su propio ciclo de vida (apertura → ejecución → cierre). Decidir cuál es la norma y cómo la instancian los otros (relacionado con T-01, incoherencia 3).
2. **Vocabulario redefinido.** `metodologia-capa-diseno` §4 define proceso · fase · tarea · gate, que ahora define la global §3 (proceso → capa → fase → tarea, niveles de cierre). La capa debería remitir a la global y añadir solo lo propio.
3. **Niveles de cierre.** La global fija tres (tarea sin registro · fase con registro · capa reforzado); comprobar que la aplicada y la capa de diseño dicen lo mismo, incluida la comprobación de versiones solo en el cierre de capa.
4. **Coherencia entre capas.** La global la exige en todo cierre de capa; la aplicada la limita al cierre de la capa de definición (relacionado con T-01, incoherencia 2).
5. **Contratos y suficiencia del traspaso.** La global §3 define el contrato abstracto; la aplicada §3 y `metodologia-capa-diseno` §2 («Contratos») lo instancian. Comprobar que el criterio de suficiencia se formula igual en los tres niveles.
6. **Validación frente a verificación.** Es un principio nuevo de la global (P3). Comprobar que el «gate visual continuo» de la capa de diseño y las verificaciones de `fases-proceso-diseno` («Verificación antes de validar») usan la distinción con el mismo sentido.
7. **Retroactividad.** Está en la global §2, en la aplicada §5 y en `metodologia-capa-diseno` §4 (cuatro reglas). Que cada nivel diga solo lo suyo: el principio, las dos direcciones y la aplicación en la capa.
8. **Edición manual.** `metodologia-capa-diseno` §2 dice que la edición manual se confina a la fase de alta fidelidad; `fases-proceso-diseno` F3 la prohíbe en wireframes, pero ni F4 ni F5 dicen si se permite.
9. **La aplicada afirma una simetría que no existe.** Dice que «las tres capas tienen documento propio», pero en `domain/` solo está la de diseño.
10. **Referencias y cabeceras desfasadas:**
    - `metodologia-capa-diseno` §1 remite al «documento de metodología general» y al «esquema del sistema», que hoy son `metodologia-global` y `metodologia-aplicada`;
    - su «Deriva de» y el de la aplicada citan global v0.4;
    - `fases-proceso-diseno` cita `metodologia-capa-diseno` v0.22, y la vigente es la v0.23.

**Orden recomendado:** después de T-05 (la global tiene que estar estable) y junto con T-01 o justo después (la aplicada se reescribe al unificar).

**Documentos afectados:** `core/metodologia-global.md`, `core/metodologia-aplicada.md`, `domain/capa-diseno/metodologia-capa-diseno.md`, `domain/capa-diseno/fases-proceso-diseno.md`.
