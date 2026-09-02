# CONTEXT_GIT.md

> Contexto operativo del proyecto para la gestión documental y versionado mediante Git.

## Configuración del repositorio

**URL del repositorio**
```
https://github.com/gineslm/design-to-code
```

**Token de acceso**
```
NO se almacena en el repositorio. El token vive en la configuración local de Git
o en una variable de entorno (p. ej. GITHUB_TOKEN); nunca se commitea.
Debe tener únicamente los permisos necesarios sobre este repositorio
(Contents: Read and write).
```

---

# Objetivo

Este repositorio actúa como **registro de decisiones y evolución documental**.

La unidad de versionado **no es un documento**, sino una **decisión o revisión**. Un mismo commit puede modificar varios documentos siempre que todos los cambios respondan a una única causa.

---

# Principios de trabajo

1. **Un commit = una decisión.**
2. Una decisión puede afectar a uno o varios documentos.
3. Nunca mezclar decisiones independientes en un mismo commit.
4. El historial debe permitir reconstruir por qué cambió cada documento.
5. Los mensajes de commit deben describir la decisión funcional, no el proceso de edición.

---

# Información que registra Git automáticamente

No duplicar estos datos en los commits:

- Fecha y hora
- Autor
- Hash del commit
- Diferencias exactas (diff)
- Historial de versiones
- Archivos modificados

Los mensajes deben aportar únicamente el contexto que Git no conoce.

---

# Identificador de revisión

Cada decisión tendrá un identificador estable con el formato:

R-001
R-002
R-003
...

Este identificador representa una revisión funcional y puede citarse desde documentos, conversaciones o reuniones.

---

# Formato obligatorio del commit

```
docs(area): título declarativo de la decisión

Revision: R-00X
Estado: Borrador | En revisión | Aprobada

Decisión:
Explicación breve de la decisión adoptada.

Documentos afectados:
- docs/archivo1.md
- docs/archivo2.md
- docs/archivo3.md

Cambios:
- Modificación relevante 1.
- Modificación relevante 2.
- Modificación relevante 3.

Impacto:
Qué sustituye, amplía o modifica respecto a revisiones anteriores.
```

---

# Tipos de commit

| Tipo | Uso |
|------|-----|
| docs | Cambios documentales |
| feat | Nueva funcionalidad o documento importante |
| refactor | Reorganización sin cambiar el significado |
| fix | Corrección de errores o inconsistencias |
| chore | Organización, índices o metadatos |

El título debe expresar la **decisión**, por ejemplo:

- `docs(auth): unificar estrategia de autenticación`
- `refactor(core): reorganizar arquitectura modular`
- `feat(api): incorporar especificación de eventos`

No usar títulos como "editar documento" o "actualizar archivo".

---

# Criterios para agrupar cambios

## Correcto

Una revisión sobre autenticación modifica:

- requisitos.md
- arquitectura.md
- api.md

Todo pertenece a la misma decisión ⇒ **1 commit**.

## Incorrecto

El mismo commit incluye:

- cambios de autenticación
- rediseño de la base de datos
- correcciones tipográficas generales

Son decisiones distintas ⇒ **varios commits**.

---

# Objetivo del historial

Debe ser posible solicitar a un agente preguntas como:

- ¿Cuál es la evolución completa de `docs/arquitectura.md`?
- ¿Qué revisión introdujo este requisito?
- ¿Qué documentos fueron modificados por `R-014`?
- Resume los cambios entre `R-008` y `R-012`.
- ¿Qué decisión sustituyó la propuesta anterior?

Para ello, cada commit debe contener información suficiente sobre la **causa**, la **decisión** y el **impacto**.

---

# Política de generación de commits

Cuando una conversación produzca cambios consolidados:

1. Identificar la decisión principal.
2. Agrupar todos los documentos afectados.
3. Generar un único mensaje de commit siguiendo la plantilla.
4. Redactar un resumen claro orientado a lectura histórica.
5. Evitar referencias al diálogo o al proceso de trabajo; describir únicamente el resultado de la decisión.

---

# Relación con el versionado por documento (convenciones-repo)

Este documento gobierna el versionado **por Git** (la unidad es la **decisión**, `R-00X`, un commit). Es **complementario**, no sustituto, del versionado **por documento** de `convenciones-repo.md` (cada documento lleva su cabecera `versión · estado · Deriva de`). Son **dos ejes**:

- **Cabecera de documento** (`v0.x`, MAYOR/MENOR) — rastrea la evolución de *un* documento.
- **Commit / revisión** (`R-00X`) — rastrea una *decisión*, que puede tocar varios documentos y bumpear sus cabeceras.

*(Pendiente de confirmar por el usuario: si ambos ejes conviven o si `R-00X` sustituye a las cabeceras por documento.)*
