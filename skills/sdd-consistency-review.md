# sdd-consistency-review.md — Skill: Revisión de Coherencia SDD Móvil

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`../constitution.md`](../constitution.md)

> **Aviso:** Este archivo describe un procedimiento de revisión reutilizable. No es un script ejecutable ni depende de ninguna plataforma específica. Cualquier agente o colaborador puede seguir este procedimiento manualmente.

---

## 1. Objetivo

Verificar que los documentos SDD del repositorio `bustrack_app` son coherentes entre sí, están completos según los requisitos de la metodología SDD y no contienen contradicciones con `constitution.md`.

---

## 2. Cuándo utilizarlo

- Al finalizar la generación o actualización de documentos SDD.
- Antes de solicitar revisión externa (al profesor o responsable del proyecto).
- Antes de aprobar el inicio de una nueva fase del plan.
- Cuando se detecta una posible inconsistencia entre documentos.
- Periódicamente durante el desarrollo para detectar desviaciones.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `constitution.md` | Norma suprema | Sí |
| `AGENTS.md` | Instrucciones operativas | Sí |
| `memoria.md` | Registro de decisiones | Sí |
| `spec.md` | Especificación de arquitectura base | Sí |
| `plan.md` | Plan de implementación | Sí |
| `task.md` | Lista de tareas | Sí |
| `subagents/*.md` | Definiciones de subagentes | Si existen |
| `skills/*.md` | Procedimientos de revisión | Si existen |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar la presencia de todos los documentos

1. Listar los archivos en la raíz del repositorio.
2. Confirmar que existen: `constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md`, `task.md`.
3. Confirmar que existen los directorios `subagents/` y `skills/` con al menos un archivo cada uno.
4. Registrar cualquier documento faltante como hallazgo.

### Paso 2: Verificar la coherencia de decisiones

Para cada decisión listada en la tabla de historial de `memoria.md`:

1. Verificar que el estado (Confirmado / Propuesto / Pendiente) es correcto.
2. Verificar que ningún otro documento contradice ese estado.
3. En particular verificar que las siguientes decisiones aparecen como **pendientes** en todos los documentos:
   - DEC-MOV-002: Biblioteca de gestión de estado.
   - DEC-MOV-003: Biblioteca de navegación.
   - DEC-MOV-004: Cliente HTTP.
   - DEC-MOV-005: Almacenamiento local.
   - DEC-MOV-006: Contratos de API.
   - DEC-MOV-009: Distribución.
4. Verificar que las siguientes decisiones aparecen como **confirmadas**:
   - Flutter como framework móvil.
   - Dart como lenguaje.
   - API REST HTTPS+JSON como protocolo de comunicación.
   - Sin acceso directo a la base de datos.

### Paso 3: Verificar la coherencia entre `spec.md` y `plan.md`

1. Verificar que cada fase del plan tiene fundamento en `spec.md`.
2. Verificar que las dependencias entre fases son coherentes con los bloqueos por decisiones pendientes.
3. Verificar que las fases bloqueadas corresponden a decisiones realmente pendientes en `memoria.md`.

### Paso 4: Verificar la coherencia entre `plan.md` y `task.md`

1. Verificar que cada tarea hace referencia a una fase existente en `plan.md`.
2. Verificar que el estado de cada tarea es coherente con el estado de su fase.
3. Verificar que ninguna tarea de implementación tiene estado `COMPLETADA` o `EN_PROGRESO` sin evidencia.
4. Verificar que las tareas `BLOQUEADAS` tienen documentados sus bloqueos.

### Paso 5: Verificar la coherencia con `constitution.md`

1. Verificar que `AGENTS.md` es coherente con los principios de `constitution.md`.
2. Verificar que `spec.md` no añade principios que contradigan `constitution.md`.
3. Verificar que los subagentes no tienen actividades prohibidas por `constitution.md`.
4. Verificar que las skills no proponen procedimientos contrarios a la constitución.

### Paso 6: Verificar la coherencia con los principios del backend

1. Verificar que los principios de comunicación (HTTPS, REST, JSON) son coherentes con `BusTrack_Back/constitution.md`.
2. Verificar que no se propone acceso directo a la base de datos.
3. Verificar que no se asume un contrato de API específico sin que esté aprobado.
4. Verificar que las restricciones de alcance funcional son coherentes entre ambos repositorios.

### Paso 7: Verificar la ausencia de contenido prohibido

Buscar en todos los documentos:

- [ ] Contraseñas, tokens, claves de API o cadenas de conexión con credenciales.
- [ ] Nombres de bibliotecas de gestión de estado, navegación o cliente HTTP marcados como seleccionados (sin aprobación).
- [ ] Endpoints funcionales específicos de la API marcados como definitivos.
- [ ] Fechas inventadas en `plan.md`.
- [ ] Tareas marcadas como completadas sin evidencia (excepto las de generación documental).
- [ ] Seguimiento GPS continuo contemplado como funcionalidad.
- [ ] Acceso directo a la base de datos desde la app.

### Paso 8: Verificar la completitud de los documentos

| Documento | Secciones mínimas requeridas |
|-----------|------------------------------|
| `constitution.md` | Secciones 1 a 16 |
| `AGENTS.md` | Secciones 1 a 13 |
| `memoria.md` | Secciones 1 a 9 |
| `spec.md` | Secciones 1 a 15 |
| `plan.md` | Fases 1 a 9 |
| `task.md` | Al menos una tarea por fase del plan |

---

## 5. Criterios de aceptación

La revisión resulta en estado **SIN OBSERVACIONES** cuando:

- Todos los documentos requeridos están presentes.
- No se detectan contradicciones entre documentos.
- Ningún documento contiene contenido prohibido.
- Los estados de decisiones en `memoria.md` son coherentes con lo expresado en los demás documentos.
- Los estados de tareas en `task.md` son coherentes con las fases de `plan.md`.
- Los criterios de aceptación de `spec.md` son verificables objetivamente.
- Los principios son coherentes con los del repositorio del backend.

---

## 6. Errores que debe evitar

| Error | Descripción |
|-------|-------------|
| Omitir documentos de la revisión | Todos los documentos listados en la entrada son obligatorios |
| Marcar como coherente sin evidencia | Cada criterio debe verificarse explícitamente |
| Modificar documentos sin documentar el cambio | Cualquier corrección debe registrarse en `memoria.md` |
| Resolver contradicciones arbitrariamente | Las contradicciones deben documentarse, no resolverse sin aprobación |
| Seleccionar decisiones pendientes para resolver una contradicción | Las decisiones pendientes requieren aprobación |

---

## 7. Formato esperado del resultado

```markdown
# Resultado de Revisión de Coherencia SDD — App Móvil BusTrack

**Fecha:** YYYY-MM-DD
**Documentos revisados:** [lista]
**Revisado por:** [agente o colaborador]

## Resumen

Estado general: SIN OBSERVACIONES / CON OBSERVACIONES / CON ERRORES CRÍTICOS

## Hallazgos por paso

### Paso 1: Presencia de documentos
[resultado]

### Paso 2: Coherencia de decisiones
[resultado]

### Paso 3: Coherencia spec.md ↔ plan.md
[resultado]

### Paso 4: Coherencia plan.md ↔ task.md
[resultado]

### Paso 5: Coherencia con constitution.md
[resultado]

### Paso 6: Coherencia con principios del backend
[resultado]

### Paso 7: Ausencia de contenido prohibido
[resultado]

### Paso 8: Completitud
[resultado]

## Observaciones y recomendaciones

[Lista de observaciones con referencia al documento y sección afectados]

## Próximos pasos recomendados

[Acciones a tomar antes de considerar la revisión superada]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
