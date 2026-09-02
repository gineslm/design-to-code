# spec-componente — ficha de componente

**Versión:** v0.7 · **Estado:** borrador · **Fecha:** 2026-08-06
**Deriva de:** plantilla-spec-componente.md v0.6 (renombrado; +clase, +referencia a entidad; grano→fase; sin cita de prueba), metodologia-capa-diseno.md v0.22, entrada-decisiones-2026-08-06.md (L.10–L.13).
**Tier:** 2 (capa `diseno`) · **Clase:** molde (se rellena por cada componente). La ficha rellena es tier 3.

> **Qué es.** El molde de una **ficha de componente**: un artefacto de **diseño** (página del lienzo), estilo **Storybook** — se *ve* el componente y sus estados, con texto breve. **No es un documento de texto**; este `.md` describe qué apartados debe tener la ficha.
> **Para quién.** Diseñador (la construye) y desarrollador (la lee para convertir): visual primero, anotaciones claras.
> **Cuándo se hace.** En la **fase de componentes**, después del alta fidelidad — así los estados ya están dibujados y la ficha se rellena con material real, sin nada "pendiente".

---

## Cómo se usa el molde
- **Se ve, no se describe.** Cada estado y variación se **muestra** con su render; el texto acompaña.
- **Nada "pendiente".** Un campo se rellena o se marca **"no aplica"** con motivo.
- **Decisión resuelta.** El equivalente nativo está **decidido**; si no, **hueco explícito** — no se deja para quien programa.
- **Un patrón, una ficha.** Un patrón repetido tiene **una** ficha; las vistas la referencian.

---

## Apartados de la ficha  [ANDAMIAJE — a refinar con uso]

> **Convención:** un dato por línea; casilla ☐ para sí/no; ejemplo en cada campo; lista donde hay varias entradas.

### 1 · Identidad
- **Nombre** — *ej.: «Selector de hueco».*
- **Función** — qué resuelve, en una frase.
- **Uso** — cuándo usarlo y cuándo no.
- **Tipo** — la naturaleza del componente. *Ej.: toast · selector · tarjeta.*
- **Equivalente nativo** — el componente de la librería. *Ej.: material-toast · material-radio.* **Decidido**; si no, **hueco**.
- **Interactivo** — ☐ sí · ☐ no.
- **Datos que representa** — la entidad/campos que muestra, si aplica (→ `spec-entidades`). *Ej.: «un hueco de Cita».*

### 2 · Componentes
- **Es atómico** (no usa otras fichas) — ☐ sí.
- **Compuesto por** — una fila por pieza: nombre → ficha que referencia. *Ej.: «Icono → ficha* icono*».*

### 3 · Propiedades
- **Entradas** (props) — nombre · valores admitidos · valor por defecto. *Ej.: «tamaño · sm/md/lg · md».*
- **Salidas** (eventos) — nombre · cuándo se emite. *Ej.: «selección · al elegir una opción».*
- **Sin propiedades** — ☐.

### 4 · Vistas de estados y variaciones
> El corazón visual. **Único apartado con imágenes**; los demás referencian estos estados por su nombre.
- **Estados** — marca y **muestra** cada uno con su render; casilla vacía = no aplica:
  ☐ normal · ☐ hover · ☐ foco · ☐ activo · ☐ deshabilitado · ☐ error · ☐ carga · ☐ vacío.
- **Variaciones** — una fila por variante, con su render. *Ej.: «con icono» · «compacta».*

### 5 · Estilos y tokens
- **Tokens** — una fila por propiedad: propiedad → token **semántico** del DS. **Solo semánticos, nunca un primitivo.** *Ej.: «fondo → --surface».*
- **Divergencias del DS** — ☐ ninguna · ☐ aporte general (amplía el DS) · ☐ regla específica local. Si hay, se describe.
- **Microanimaciones** — ☐ no · ☐ sí → se **describe y se muestra**. *Ej.: «entrada: fundido 150 ms».*

### 6 · Comportamiento
> Qué hace, en palabras. Las imágenes están en el apartado 4.
- **Qué desencadena qué** — interacción con lógica → estado o resultado. *Ej.: «clic → estado* seleccionado*».*
- **Validaciones** — condición → **texto literal** del mensaje. *Ej.: «vacío → "Selecciona una hora"».*
- **Comportamiento obligatorio no visible** — ☐ ninguno · ☐ sí → se describe. *Ej.: modal de confirmación.*
- **Casos límite** — situación → respuesta. *Ej.: «doble disparo → ignora el segundo».*

### 7 · Accesibilidad
> Solo lo propio del componente; las reglas globales viven en `spec-app`.
- **Rol** — *ej.: radiogroup.* · **Etiqueta** (literal) — *ej.: "Elige un hueco".* · **Orden de foco** — *ej.: de arriba abajo.* · **Contraste/táctil mínimos** — ☐ cumple.

### 8 · Comentarios
- Notas que no encajan arriba.
- La ficha **define**, no registra decisiones. Una decisión anotada aquí **debe** quedar también en el registro de capa.
