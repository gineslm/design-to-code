# spec-vista — ficha de vista

**Versión:** v0.3 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** plantilla-spec-vista.md v0.2 (renombrado; +clase, +referencia a entidad; grano→fase; nombres actualizados), spec-componente.md v0.7, metodologia-capa-diseno.md v0.22.
**Tier:** 2 (capa `diseno`) · **Clase:** molde (se rellena por cada vista). La ficha rellena es tier 3.

> **Qué es.** El molde de una **ficha de vista**: un artefacto de **diseño**, estilo **Storybook a nivel pantalla**. **Compone** fichas de componente; no las redefine. **No es un documento de texto.**
> **Para quién.** Diseñador (la construye) y desarrollador (la lee para convertir).
> **Cuándo se hace.** En la **fase de vistas**, cuando ya existen las fichas de los componentes que la forman.

---

## Cómo se usa el molde
- **Compone, no redefine.** Cada componente se referencia por su ficha; sus props y estados **no se copian**.
- **Ningún componente sin ficha.** Si aparece uno sin ficha, es **hueco bloqueante**.
- **Se ve, no se describe · nada "pendiente".** Cada estado se **muestra** con su render.
- **Anidamiento.** app → vista → componentes → DS. Referencia hacia abajo, no duplica.

---

## Apartados de la ficha  [ANDAMIAJE — a refinar con uso]

> **Convención:** un dato por línea; casilla ☐ para sí/no; ejemplo en cada campo; lista donde hay varias entradas.

### 1 · Identidad
- **Nombre** — *ej.: «Detalle de cita».*
- **Propósito** — qué permite hacer, en una frase.
- **Ruta** — pantalla/URL. *Ej.: /citas/:id.*
- **Punto de entrada** — desde dónde se llega. *Ej.: desde «Listado de citas».*
- **Datos/entidades que muestra** — (→ `spec-entidades`). *Ej.: «una Cita y su Paciente».*

### 2 · Componentes que la forman
- **Componentes** — una fila por pieza: componente → ficha → variante/props. *Ej.: «Selector de hueco → ficha* selector *· tamaño md».*
- **Todos tienen ficha** — ☐ sí. *(Si no, hueco bloqueante.)*

### 3 · Layout y responsive
- **Estructura** — regiones/zonas y su orden. *Ej.: cabecera · contenido · acciones.*
- **Recolocación** — cómo cambia por tamaño, **en palabras**; los renders por tamaño, en el apartado 4. *Ej.: «en móvil, las acciones pasan a pie fijo».*
- **Breakpoints** — se **aplican** los que fija `spec-app`; no se redefinen aquí.

### 4 · Vistas de la vista (estados)
> **Único apartado con imágenes.** Estados de la vista y, si aplica, tamaños.
- **Estados** — marca y **muestra**: ☐ con datos · ☐ carga · ☐ vacío · ☐ error.
- **Tamaños** — render en los breakpoints relevantes.

### 5 · Navegación
- **Entradas** — desde qué vistas se llega.
- **Salidas** — una fila por acción → destino. *Ej.: «Guardar → vuelve a Listado».*

### 6 · Comportamiento de la vista
> Lógica **a nivel vista**; la de cada componente vive en su ficha.
- **Qué desencadena qué** — orquestación entre componentes. *Ej.: «cambiar Centro → resetea Especialidad y Médico».*
- **Carga de datos** — qué se carga al entrar y qué se muestra mientras tanto.
- **Obligatorio no visible** — ☐ ninguno · ☐ sí → se describe.
- **Casos límite** — situación → respuesta.

### 7 · Accesibilidad
> Solo lo de nivel vista; las reglas globales viven en `spec-app`.
- **Landmarks / orden de encabezados** — *ej.: un solo h1.* · **Gestión del foco** — *ej.: foco al título al cargar.*

### 8 · Comentarios
- Notas que no encajan arriba.
- La ficha **define**, no registra decisiones. Una decisión anotada aquí **debe** quedar también en el registro de capa.
