# task.md — Tareas Trazables de la Aplicación Móvil de BusTrack

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-28  
**Referencia normativa:** [`constitution.md`](./constitution.md) | [`plan.md`](./plan.md)

> **Importante:** Las tareas de esta lista representan trabajo previsto. Ninguna tarea de implementación puede marcarse como COMPLETADA sin evidencia verificable. Las tareas de documentación pueden completarse cuando el artefacto documental correspondiente haya sido creado y pueda verificarse.

---

## Convenciones de estado

| Estado | Descripción |
|--------|-------------|
| `PENDIENTE` | No iniciada; puede comenzar una vez se resuelvan sus dependencias |
| `EN_PROGRESO` | Iniciada; hay trabajo activo sobre ella |
| `BLOQUEADA` | No puede iniciarse; tiene un bloqueo explícito |
| `COMPLETADA` | Finalizada con evidencia verificable |
| `CANCELADA` | Descartada con justificación documentada |

---

## Fase 1 — Validación de la documentación SDD

### TASK-MOV-DOC-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-001 |
| **Descripción** | Crear `constitution.md` de la aplicación móvil de BusTrack |
| **Dependencias** | Ninguna |
| **Criterios de aceptación** | El archivo `constitution.md` existe en la raíz del repositorio; contiene los principios normativos, restricciones de arquitectura móvil, separación de responsabilidades, seguridad, calidad, pruebas, mantenibilidad y coherencia documental; está alineado con los principios del backend |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `constitution.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-002 |
| **Descripción** | Crear `AGENTS.md` de la aplicación móvil de BusTrack |
| **Dependencias** | TASK-MOV-DOC-001 |
| **Criterios de aceptación** | El archivo `AGENTS.md` existe en la raíz del repositorio; define instrucciones para agentes y colaboradores; exige revisar la constitución, la memoria y las especificaciones antes de proponer cambios; prohíbe implementar código en la etapa documental; prohíbe seleccionar decisiones pendientes como definitivas |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `AGENTS.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-003

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-003 |
| **Descripción** | Crear `memoria.md` de la aplicación móvil de BusTrack |
| **Dependencias** | TASK-MOV-DOC-001 |
| **Criterios de aceptación** | El archivo `memoria.md` existe en la raíz del repositorio; registra el contexto del proyecto, las decisiones confirmadas, las decisiones pendientes (con identificadores únicos), los supuestos, los riesgos y el historial de decisiones; utiliza tablas con identificador, decisión, estado, justificación y próximo paso |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `memoria.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-004

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-004 |
| **Descripción** | Crear `spec.md` de la aplicación móvil de BusTrack |
| **Dependencias** | TASK-MOV-DOC-001, TASK-MOV-DOC-003 |
| **Criterios de aceptación** | El archivo `spec.md` existe en la raíz del repositorio; documenta la arquitectura base de Flutter incluyendo propósito y alcance, contexto e interacción con la API, capas de presentación/aplicación/datos, componentes compartidos, principios de navegación, estrategia general de gestión de estado, comunicación HTTP y procesamiento JSON, manejo de errores y estados de carga, configuración por entorno, seguridad, estrategia de pruebas, requisitos no funcionales, decisiones pendientes y criterios de aceptación verificables; no selecciona bibliotecas pendientes ni define endpoints no aprobados |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `spec.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-005

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-005 |
| **Descripción** | Crear `plan.md` de la aplicación móvil de BusTrack |
| **Dependencias** | TASK-MOV-DOC-001, TASK-MOV-DOC-004 |
| **Criterios de aceptación** | El archivo `plan.md` existe en la raíz del repositorio; organiza las fases futuras (Validación documental, Aprobación arquitectura, Preparación entorno, Contratos con backend, Implementación estructura base, Integración con API, Pruebas, CI/CD, Preparación entrega); indica dependencias, entregables, criterios de salida y bloqueos; no asigna fechas; no ejecuta las actividades descritas |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `plan.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-006

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-006 |
| **Descripción** | Crear `task.md` de la aplicación móvil de BusTrack |
| **Dependencias** | TASK-MOV-DOC-001, TASK-MOV-DOC-005 |
| **Criterios de aceptación** | El archivo `task.md` existe en la raíz del repositorio; desglosa el trabajo en tareas trazables; cada tarea tiene identificador, descripción, dependencias, criterios de aceptación, estado y referencia de origen; las tareas de implementación tienen estado BLOQUEADA o PENDIENTE; las tareas de documentación tienen el estado correcto |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivo `task.md` creado en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-007

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-007 |
| **Descripción** | Crear las definiciones de subagentes documentales en `subagents/` |
| **Dependencias** | TASK-MOV-DOC-001 |
| **Criterios de aceptación** | El directorio `subagents/` existe; contiene definiciones Markdown para los revisores de arquitectura móvil, documentación SDD y seguridad; los archivos no afirman que los subagentes estén ejecutándose en ninguna plataforma |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivos en `subagents/` creados en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-008

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-008 |
| **Descripción** | Crear los procedimientos de revisión en `skills/` |
| **Dependencias** | TASK-MOV-DOC-001, TASK-MOV-DOC-004 |
| **Criterios de aceptación** | El directorio `skills/` existe; contiene procedimientos Markdown para revisar la arquitectura Flutter, la coherencia SDD y la seguridad del cliente móvil; los procedimientos son ejecutables manualmente por cualquier agente o colaborador |
| **Estado** | `COMPLETADA` |
| **Evidencia** | Archivos en `skills/` creados en esta sesión — 2026-10-28 |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-009

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-009 |
| **Descripción** | Revisión de coherencia interna de todos los documentos SDD generados |
| **Dependencias** | TASK-MOV-DOC-001 a TASK-MOV-DOC-008 |
| **Criterios de aceptación** | Se ha ejecutado el procedimiento `skills/sdd-consistency-review.md`; no se detectan contradicciones entre documentos; los estados de las decisiones son coherentes en todos los documentos; el resultado de la revisión está documentado |
| **Estado** | `PENDIENTE` |
| **Bloqueo** | Requiere que todos los documentos estén creados |
| **Referencia** | Fase 1 de `plan.md` |

---

### TASK-MOV-DOC-010

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DOC-010 |
| **Descripción** | Revisión y aprobación formal de la documentación SDD por parte del responsable del proyecto (profesor) |
| **Dependencias** | TASK-MOV-DOC-009 |
| **Criterios de aceptación** | El responsable del proyecto ha revisado la documentación y ha dado su aprobación formal; la aprobación está registrada en `memoria.md` |
| **Estado** | `PENDIENTE` |
| **Bloqueo** | Requiere disponibilidad del responsable del proyecto |
| **Referencia** | Fase 1 de `plan.md` |

---

## Fase 2 — Aprobación de la arquitectura móvil

### TASK-MOV-ARCH-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-001 |
| **Descripción** | Evaluar y seleccionar la biblioteca de gestión de estado para Flutter (DEC-MOV-002) |
| **Dependencias** | TASK-MOV-DOC-010 (Fase 1 aprobada) |
| **Criterios de aceptación** | Se ha realizado una evaluación comparativa de las opciones (Riverpod, Bloc, Provider, u otro); la decisión está documentada con justificación en `memoria.md`; DEC-MOV-002 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 2 de `plan.md` |

---

### TASK-MOV-ARCH-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-002 |
| **Descripción** | Evaluar y seleccionar la biblioteca de navegación para Flutter (DEC-MOV-003) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | Se ha realizado una evaluación comparativa; la decisión está documentada con justificación en `memoria.md`; DEC-MOV-003 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 2 de `plan.md` |

---

### TASK-MOV-ARCH-003

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-003 |
| **Descripción** | Seleccionar el cliente HTTP para Flutter (DEC-MOV-004) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | La decisión está documentada con justificación en `memoria.md`; DEC-MOV-004 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 2 de `plan.md` |

---

### TASK-MOV-ARCH-004

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-004 |
| **Descripción** | Definir la estrategia de configuración por entorno en Flutter (DEC-MOV-013) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | La estrategia está documentada en `memoria.md`; DEC-MOV-013 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 2 de `plan.md` |

---

### TASK-MOV-ARCH-005

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-005 |
| **Descripción** | Definir las plataformas objetivo y versiones mínimas (DEC-MOV-015) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | Las plataformas y versiones mínimas están documentadas en `memoria.md`; DEC-MOV-015 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 2 de `plan.md` |

---

### TASK-MOV-ARCH-006

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ARCH-006 |
| **Descripción** | Definir la estructura definitiva de directorios del proyecto Flutter (DEC-MOV-014) |
| **Dependencias** | TASK-MOV-ARCH-001, TASK-MOV-ARCH-002 |
| **Criterios de aceptación** | La estructura de directorios está documentada y aprobada; DEC-MOV-014 marcada como confirmada; `spec.md` actualizado con la estructura aprobada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-002, DEC-MOV-003 no resueltas |
| **Referencia** | Fase 2 de `plan.md` |

---

## Fase 3 — Preparación del entorno Flutter

### TASK-MOV-ENV-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ENV-001 |
| **Descripción** | Confirmar y documentar la versión de Flutter y Dart a utilizar (DEC-MOV-001) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | La versión de Flutter y Dart está documentada en `memoria.md`; DEC-MOV-001 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 3 de `plan.md` |

---

### TASK-MOV-ENV-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ENV-002 |
| **Descripción** | Crear el proyecto Flutter con la configuración base aprobada |
| **Dependencias** | TASK-MOV-ARCH-001 a TASK-MOV-ARCH-006, TASK-MOV-ENV-001 |
| **Criterios de aceptación** | El proyecto Flutter existe con la estructura de directorios aprobada; `pubspec.yaml` tiene las dependencias aprobadas; el proyecto compila sin errores |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fases 1 y 2 no completadas; decisiones DEC-MOV-001 a DEC-MOV-015 no resueltas |
| **Referencia** | Fase 3 de `plan.md` |

---

### TASK-MOV-ENV-003

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-ENV-003 |
| **Descripción** | Configurar `.gitignore` para el proyecto Flutter |
| **Dependencias** | TASK-MOV-ENV-002 |
| **Criterios de aceptación** | El `.gitignore` excluye los archivos de compilación, archivos de configuración local sensibles y archivos específicos del IDE; ningún archivo sensible está en el repositorio |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | TASK-MOV-ENV-002 no iniciada |
| **Referencia** | Fase 3 de `plan.md` |

---

## Fase 4 — Definición de contratos con el backend

### TASK-MOV-API-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-API-001 |
| **Descripción** | Coordinar con el equipo del backend para definir los endpoints que la app móvil consumirá (DEC-MOV-006) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | Los contratos de API están documentados y aprobados por ambos equipos; DEC-MOV-006 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada; disponibilidad del equipo del backend |
| **Referencia** | Fase 4 de `plan.md` |

---

### TASK-MOV-API-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-API-002 |
| **Descripción** | Definir el mecanismo de autenticación del cliente móvil, alineado con el backend (DEC-MOV-010) |
| **Dependencias** | TASK-MOV-API-001 |
| **Criterios de aceptación** | El mecanismo de autenticación está documentado y alineado con la decisión del backend; DEC-MOV-010 marcada como confirmada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-006 del backend no resuelta; TASK-MOV-API-001 no completada |
| **Referencia** | Fase 4 de `plan.md` |

---

## Fase 5 — Implementación de la estructura base

### TASK-MOV-IMPL-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-001 |
| **Descripción** | Implementar la estructura de capas (Presentación, Aplicación, Datos) en el código Flutter |
| **Dependencias** | TASK-MOV-ENV-002, TASK-MOV-ARCH-006 |
| **Criterios de aceptación** | La estructura de directorios refleja las capas aprobadas; los criterios AC-MOV-ARCH-01, AC-MOV-ARCH-02, AC-MOV-ARCH-03 pasan |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fases 1, 2, 3 no completadas |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-002 |
| **Descripción** | Configurar el gestor de estado base (biblioteca seleccionada en DEC-MOV-002) |
| **Dependencias** | TASK-MOV-IMPL-001, DEC-MOV-002 resuelta |
| **Criterios de aceptación** | El gestor de estado está configurado e integrado; los criterios AC-MOV-ARCH-14 pasa |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-002 no resuelta |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-003

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-003 |
| **Descripción** | Configurar la navegación base (biblioteca seleccionada en DEC-MOV-003) |
| **Dependencias** | TASK-MOV-IMPL-001, DEC-MOV-003 resuelta |
| **Criterios de aceptación** | Las rutas base están configuradas y centralizadas; el criterio AC-MOV-ARCH-09 pasa |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-003 no resuelta |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-004

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-004 |
| **Descripción** | Configurar el cliente HTTP base y el manejo centralizado de errores de red |
| **Dependencias** | TASK-MOV-IMPL-001, DEC-MOV-004 resuelta, DEC-MOV-013 resuelta |
| **Criterios de aceptación** | El cliente HTTP está configurado con la URL base por entorno; el manejo de errores HTTP cubre todos los escenarios documentados en `spec.md`; los criterios AC-MOV-ARCH-04, AC-MOV-ARCH-12, AC-MOV-ARCH-13 pasan |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-004, DEC-MOV-013 no resueltas |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-005

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-005 |
| **Descripción** | Implementar los estados genéricos de carga, éxito, error y vacío |
| **Dependencias** | TASK-MOV-IMPL-002 |
| **Criterios de aceptación** | Existe un mecanismo genérico y reutilizable para representar los cuatro estados; los widgets pueden mostrar el estado correspondiente; el criterio AC-MOV-ARCH-06 pasa |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-002 no resuelta |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-006

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-006 |
| **Descripción** | Implementar el mecanismo de autenticación en el cliente (DEC-MOV-010) |
| **Dependencias** | TASK-MOV-IMPL-004, TASK-MOV-API-002 |
| **Criterios de aceptación** | Los tokens se almacenan usando mecanismos seguros del sistema operativo; los tokens se incluyen en las solicitudes HTTP; los tokens se eliminan al cerrar sesión; el criterio AC-MOV-ARCH-08 pasa |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | DEC-MOV-010 no resuelta |
| **Referencia** | Fase 5 de `plan.md` |

---

### TASK-MOV-IMPL-007

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-IMPL-007 |
| **Descripción** | Verificar todos los criterios de aceptación de la arquitectura base (AC-MOV-ARCH-01 al AC-MOV-ARCH-14) |
| **Dependencias** | TASK-MOV-IMPL-001 a TASK-MOV-IMPL-006 |
| **Criterios de aceptación** | Todos los criterios AC-MOV-ARCH-01 al AC-MOV-ARCH-14 están verificados y pasan |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Todas las tareas TASK-MOV-IMPL pendientes |
| **Referencia** | Fase 5 de `plan.md` |

---

## Fase 6 — Integración con la API

### TASK-MOV-INT-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-INT-001 |
| **Descripción** | Implementar los repositorios definidos en los contratos de la API (DEC-MOV-006) |
| **Dependencias** | TASK-MOV-IMPL-007, TASK-MOV-API-001 |
| **Criterios de aceptación** | Los repositorios implementan los contratos aprobados; los datos se parsean correctamente desde JSON; el criterio AC-MOV-ARCH-05 pasa |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fases 4 y 5 no completadas |
| **Referencia** | Fase 6 de `plan.md` |

---

## Fase 7 — Pruebas

### TASK-MOV-TEST-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-TEST-001 |
| **Descripción** | Definir el umbral mínimo de cobertura de pruebas (DEC-MOV-011) y seleccionar las herramientas (DEC-MOV-012) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | DEC-MOV-011 y DEC-MOV-012 marcadas como confirmadas en `memoria.md` |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada |
| **Referencia** | Fase 7 de `plan.md` |

---

### TASK-MOV-TEST-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-TEST-002 |
| **Descripción** | Crear pruebas unitarias para la lógica de la capa de aplicación y datos |
| **Dependencias** | TASK-MOV-IMPL-007, TASK-MOV-TEST-001 |
| **Criterios de aceptación** | Las pruebas pasan sin conexión de red; el criterio AC-MOV-ARCH-10 pasa; el umbral de cobertura DEC-MOV-011 se cumple |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 5 no completada; DEC-MOV-011, DEC-MOV-012 no resueltas |
| **Referencia** | Fase 7 de `plan.md` |

---

### TASK-MOV-TEST-003

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-TEST-003 |
| **Descripción** | Crear pruebas de widgets para los componentes de interfaz críticos |
| **Dependencias** | TASK-MOV-IMPL-007, TASK-MOV-TEST-001 |
| **Criterios de aceptación** | Los componentes de interfaz críticos tienen pruebas de widgets que verifican su comportamiento |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 5 no completada; DEC-MOV-012 no resuelta |
| **Referencia** | Fase 7 de `plan.md` |

---

## Fase 8 — Automatización de comprobaciones

### TASK-MOV-CI-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-CI-001 |
| **Descripción** | Configurar el pipeline de integración continua para la aplicación Flutter |
| **Dependencias** | TASK-MOV-TEST-002, TASK-MOV-TEST-003 |
| **Criterios de aceptación** | El pipeline ejecuta pruebas y análisis estático automáticamente; falla si hay errores |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 7 no completada |
| **Referencia** | Fase 8 de `plan.md` |

---

## Fase 9 — Preparación de la entrega

### TASK-MOV-DIST-001

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DIST-001 |
| **Descripción** | Definir la estrategia de publicación y distribución de la aplicación (DEC-MOV-009) |
| **Dependencias** | TASK-MOV-DOC-010 |
| **Criterios de aceptación** | DEC-MOV-009 marcada como confirmada en `memoria.md`; la estrategia está documentada |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fase 1 no completada; decisión de negocio pendiente |
| **Referencia** | Fase 9 de `plan.md` |

---

### TASK-MOV-DIST-002

| Campo | Valor |
|-------|-------|
| **ID** | TASK-MOV-DIST-002 |
| **Descripción** | Configurar el pipeline de entrega continua (CD) para generar artefactos distribuibles |
| **Dependencias** | TASK-MOV-CI-001, TASK-MOV-DIST-001 |
| **Criterios de aceptación** | El pipeline genera artefactos firmados (APK/AAB, IPA) sin errores; los secretos de firma no están en el repositorio |
| **Estado** | `BLOQUEADA` |
| **Bloqueo** | Fases 8 y decisión DEC-MOV-009 no completadas |
| **Referencia** | Fase 9 de `plan.md` |

---

## Resumen de estado de tareas

| ID | Descripción breve | Fase | Estado |
|----|------------------|------|--------|
| TASK-MOV-DOC-001 | Crear `constitution.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-002 | Crear `AGENTS.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-003 | Crear `memoria.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-004 | Crear `spec.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-005 | Crear `plan.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-006 | Crear `task.md` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-007 | Crear `subagents/` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-008 | Crear `skills/` | 1 | `COMPLETADA` |
| TASK-MOV-DOC-009 | Revisión de coherencia interna | 1 | `PENDIENTE` |
| TASK-MOV-DOC-010 | Aprobación del responsable del proyecto | 1 | `PENDIENTE` |
| TASK-MOV-ARCH-001 | Seleccionar gestión de estado (DEC-MOV-002) | 2 | `BLOQUEADA` |
| TASK-MOV-ARCH-002 | Seleccionar navegación (DEC-MOV-003) | 2 | `BLOQUEADA` |
| TASK-MOV-ARCH-003 | Seleccionar cliente HTTP (DEC-MOV-004) | 2 | `BLOQUEADA` |
| TASK-MOV-ARCH-004 | Definir configuración por entorno (DEC-MOV-013) | 2 | `BLOQUEADA` |
| TASK-MOV-ARCH-005 | Definir plataformas objetivo (DEC-MOV-015) | 2 | `BLOQUEADA` |
| TASK-MOV-ARCH-006 | Definir estructura de directorios (DEC-MOV-014) | 2 | `BLOQUEADA` |
| TASK-MOV-ENV-001 | Confirmar versión Flutter/Dart (DEC-MOV-001) | 3 | `BLOQUEADA` |
| TASK-MOV-ENV-002 | Crear proyecto Flutter base | 3 | `BLOQUEADA` |
| TASK-MOV-ENV-003 | Configurar `.gitignore` | 3 | `BLOQUEADA` |
| TASK-MOV-API-001 | Definir contratos de API (DEC-MOV-006) | 4 | `BLOQUEADA` |
| TASK-MOV-API-002 | Definir autenticación cliente (DEC-MOV-010) | 4 | `BLOQUEADA` |
| TASK-MOV-IMPL-001 | Implementar estructura de capas | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-002 | Configurar gestor de estado | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-003 | Configurar navegación base | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-004 | Configurar cliente HTTP y errores de red | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-005 | Implementar estados carga/éxito/error/vacío | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-006 | Implementar autenticación cliente | 5 | `BLOQUEADA` |
| TASK-MOV-IMPL-007 | Verificar criterios de aceptación AC-MOV-ARCH | 5 | `BLOQUEADA` |
| TASK-MOV-INT-001 | Implementar repositorios con la API | 6 | `BLOQUEADA` |
| TASK-MOV-TEST-001 | Seleccionar herramientas de prueba | 7 | `BLOQUEADA` |
| TASK-MOV-TEST-002 | Crear pruebas unitarias | 7 | `BLOQUEADA` |
| TASK-MOV-TEST-003 | Crear pruebas de widgets | 7 | `BLOQUEADA` |
| TASK-MOV-CI-001 | Configurar pipeline CI | 8 | `BLOQUEADA` |
| TASK-MOV-DIST-001 | Definir estrategia de distribución (DEC-MOV-009) | 9 | `BLOQUEADA` |
| TASK-MOV-DIST-002 | Configurar pipeline CD | 9 | `BLOQUEADA` |

---

*Este documento debe actualizarse cuando se inicie, complete o bloquee cualquier tarea. Las actualizaciones deben seguir el proceso de control de cambios descrito en `constitution.md`.*
