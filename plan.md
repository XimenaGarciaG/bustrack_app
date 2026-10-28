# plan.md — Plan de Implementación de la Aplicación Móvil de BusTrack

**Versión:** 1.0.0  
**Estado:** Borrador — Pendiente de revisión y aprobación  
**Última actualización:** 2026-10-28  
**Referencia normativa:** [`constitution.md`](./constitution.md) | [`spec.md`](./spec.md)

> **Importante:** Este documento describe las fases de implementación previstas. Ninguna actividad descrita aquí ha sido ejecutada. Este plan no autoriza el inicio de ninguna fase. Cada fase debe ser aprobada antes de comenzarse. No se asignan fechas; los plazos se acordarán al aprobar cada fase.

---

## Convenciones del plan

| Símbolo | Significado |
|---------|-------------|
| 🔴 BLOQUEADA | No puede iniciarse; depende de una decisión pendiente o fase anterior |
| 🟡 PENDIENTE | Puede iniciarse una vez aprobada la fase anterior |
| 🟢 ACTIVA | En curso (ninguna fase está activa actualmente) |
| ✅ COMPLETADA | Finalizada con evidencia |

---

## Fase 1 — Validación de la documentación SDD

**Objetivo:** Garantizar que la documentación SDD de la aplicación móvil es coherente, completa y está aprobada antes de iniciar cualquier implementación.

**Estado:** 🟡 PENDIENTE de revisión y aprobación

### Actividades previstas

1. Revisión de coherencia interna entre `constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md` y `task.md`.
2. Verificación de coherencia con los principios del backend BusTrack (`BusTrack_Back/constitution.md`).
3. Revisión de coherencia por parte del responsable del proyecto (profesor).
4. Identificación y resolución de contradicciones o vacíos en la documentación.
5. Aprobación formal de la especificación arquitectónica (`spec.md`).
6. Actualización de `memoria.md` con el resultado de la revisión.

### Dependencias

- Ninguna (esta es la primera fase).

### Entregables esperados

- Documentos SDD revisados y aprobados.
- Registro de decisiones actualizado en `memoria.md`.
- Lista de elementos pendientes de resolución antes de la Fase 2.

### Criterios de salida

- Los documentos `constitution.md`, `spec.md`, `plan.md` y `task.md` han sido revisados y no contienen contradicciones detectadas.
- La especificación (`spec.md`) ha sido aprobada formalmente.
- Todas las decisiones críticas para la Fase 2 están resueltas o documentadas como bloqueos aceptados.

### Decisiones que bloquean el avance a la Fase 2

- DEC-MOV-014: Estructura definitiva de directorios del proyecto Flutter.

---

## Fase 2 — Aprobación de la arquitectura móvil

**Objetivo:** Validar y aprobar las decisiones arquitectónicas clave de la aplicación móvil antes de preparar el entorno técnico.

**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Fase 1.

### Actividades previstas

1. Revisión y aprobación de la estructura de capas propuesta (Presentación / Aplicación / Datos).
2. Evaluación y selección de la biblioteca de gestión de estado (DEC-MOV-002).
3. Evaluación y selección de la biblioteca de navegación (DEC-MOV-003).
4. Evaluación y selección del cliente HTTP (DEC-MOV-004).
5. Decisión sobre la estrategia de configuración por entorno en Flutter (DEC-MOV-013).
6. Decisión sobre las plataformas objetivo y versiones mínimas (DEC-MOV-015).
7. Decisión sobre la estructura definitiva de directorios (DEC-MOV-014).
8. Registro de todas las decisiones aprobadas en `memoria.md`.
9. Actualización de `spec.md` con las decisiones incorporadas.

### Dependencias

- Fase 1 completada y aprobada.

### Entregables esperados

- Decisiones DEC-MOV-002, DEC-MOV-003, DEC-MOV-004, DEC-MOV-013, DEC-MOV-014, DEC-MOV-015 resueltas y aprobadas.
- `spec.md` actualizado con las decisiones incorporadas.
- `memoria.md` actualizado con el historial de decisiones.

### Criterios de salida

- Las decisiones críticas de arquitectura están confirmadas y registradas.
- No existen contradicciones entre los documentos actualizados.
- La aprobación está documentada en `memoria.md`.

### Decisiones que bloquean el avance a la Fase 3

- DEC-MOV-001: Versión exacta de Flutter y Dart.

---

## Fase 3 — Preparación del entorno Flutter

**Objetivo:** Preparar el entorno de desarrollo Flutter reproducible y configurado para el proyecto BusTrack Móvil.

**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Fase 2 y resolución de DEC-MOV-001, DEC-MOV-007, DEC-MOV-015.

### Actividades previstas

1. Confirmar la versión de Flutter y Dart a utilizar (DEC-MOV-001).
2. Crear el proyecto Flutter con la plantilla adecuada para la plataforma(s) objetivo.
3. Configurar el archivo `pubspec.yaml` con las dependencias aprobadas en la Fase 2.
4. Configurar la estructura de directorios aprobada (DEC-MOV-014).
5. Configurar el mecanismo de separación de entornos (DEC-MOV-013).
6. Configurar `.gitignore` para excluir archivos locales y sensibles.
7. Verificar que el proyecto compila y ejecuta correctamente en el entorno de desarrollo.
8. Documentar el proceso de configuración del entorno para nuevos colaboradores.

### Dependencias

- Fase 2 completada y aprobada.
- DEC-MOV-001: Versión de Flutter y Dart.
- DEC-MOV-007: Versiones exactas de dependencias aprobadas.
- DEC-MOV-015: Plataformas objetivo y versiones mínimas.

### Entregables esperados

- Proyecto Flutter configurado y ejecutable en el entorno de desarrollo.
- `pubspec.yaml` con las dependencias aprobadas.
- Estructura de directorios establecida.
- Documentación del entorno de desarrollo.

### Criterios de salida

- El proyecto Flutter compila sin errores en el entorno de desarrollo.
- La estructura de directorios refleja la arquitectura en capas aprobada.
- El entorno de configuración por entorno funciona correctamente.
- `.gitignore` excluye los archivos locales y sensibles correctamente.

### Bloqueos para el avance a la Fase 4

- DEC-MOV-006: Contratos funcionales de la API (necesarios para diseñar repositorios).

---

## Fase 4 — Definición de contratos con el backend

**Objetivo:** Establecer los contratos de la API REST que la aplicación móvil consumirá, en coordinación con el equipo del backend.

**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Fase 1 y depende de la disponibilidad del equipo del backend.

> **Nota:** Esta fase puede desarrollarse en paralelo con la Fase 3, pero sus entregables son necesarios antes de iniciar la Fase 5.

### Actividades previstas

1. Identificar las entidades y operaciones que la app móvil necesita consumir (en coordinación con el backend).
2. Documentar los endpoints de la API que serán consumidos por la app móvil (URLs, métodos HTTP, parámetros, estructuras de respuesta).
3. Definir los modelos de datos JSON que la app móvil recibirá del backend.
4. Documentar los errores que cada endpoint puede retornar.
5. Acordar el mecanismo de autenticación del cliente (DEC-MOV-010, alineado con el backend).
6. Revisar y aprobar los contratos con el equipo del backend.
7. Registrar los contratos aprobados como referencia en este repositorio.

### Dependencias

- Fase 1 completada.
- Disponibilidad del equipo del backend (repositorio `BusTrack_Back`).
- Especificaciones funcionales del sistema (fuera del alcance de la fase actual).

### Entregables esperados

- Documentación de contratos de API aprobados (DEC-MOV-006 resuelta).
- Definición del mecanismo de autenticación del cliente (DEC-MOV-010 resuelta).

### Criterios de salida

- DEC-MOV-006 marcada como confirmada en `memoria.md`.
- DEC-MOV-010 marcada como confirmada en `memoria.md`.
- Los contratos están documentados y aprobados por ambos equipos (backend y móvil).

---

## Fase 5 — Implementación de la estructura base

**Objetivo:** Implementar la arquitectura base de la aplicación Flutter con las capas, la comunicación HTTP, el manejo de errores y los mecanismos base de la aplicación.

**Estado:** 🔴 BLOQUEADA — Depende de Fases 3 y 4, y de la resolución de DEC-MOV-002, DEC-MOV-003, DEC-MOV-004, DEC-MOV-005.

### Actividades previstas

1. Implementar la estructura de capas (Presentación, Aplicación, Datos) en el código.
2. Configurar el gestor de estado seleccionado (DEC-MOV-002).
3. Configurar la navegación base con la biblioteca seleccionada (DEC-MOV-003).
4. Configurar el cliente HTTP base con la biblioteca seleccionada (DEC-MOV-004).
5. Implementar el manejo centralizado de errores de red y de API.
6. Implementar los estados genéricos de carga, éxito, error y vacío.
7. Configurar el almacenamiento local base si aplica (DEC-MOV-005).
8. Implementar el mecanismo de autenticación en el cliente (DEC-MOV-010).
9. Verificar los criterios de aceptación AC-MOV-ARCH-01 al AC-MOV-ARCH-14.

### Dependencias

- Fase 3 completada (entorno preparado).
- Fase 4 completada (contratos de API definidos).
- DEC-MOV-002: Biblioteca de gestión de estado.
- DEC-MOV-003: Biblioteca de navegación.
- DEC-MOV-004: Cliente HTTP.
- DEC-MOV-005: Estrategia de almacenamiento local.

### Entregables esperados

- Estructura base del proyecto Flutter implementada.
- Cliente HTTP configurado y funcional contra el backend.
- Manejo de errores y estados implementado.
- Criterios de aceptación AC-MOV-ARCH-01 al AC-MOV-ARCH-14 verificados.

### Criterios de salida

- Todos los criterios de aceptación de la arquitectura base pasan.
- La aplicación compila y se ejecuta en Android e iOS en el entorno de desarrollo.
- La comunicación con el backend funciona correctamente.

---

## Fase 6 — Integración con la API

**Objetivo:** Implementar los repositorios y la capa de datos que conectan la aplicación con los endpoints reales del backend.

**Estado:** 🔴 BLOQUEADA — Depende de la Fase 5 y de la disponibilidad del backend.

### Actividades previstas

1. Implementar los repositorios definidos en los contratos de la Fase 4.
2. Implementar las fuentes de datos remotas (API calls).
3. Implementar el parsing y serialización de los modelos de datos JSON.
4. Probar la integración con el backend en el entorno de desarrollo.
5. Gestionar la paginación si aplica (alineado con la política del backend).
6. Verificar el correcto manejo de todos los códigos de error HTTP esperados.

### Dependencias

- Fase 5 completada (arquitectura base implementada).
- Backend disponible en el entorno de desarrollo.

### Entregables esperados

- Repositorios e integración con la API implementados y probados.
- Modelos de datos correctamente serializados/deserializados.

### Criterios de salida

- Los repositorios implementados funcionan correctamente contra el backend real.
- El manejo de errores HTTP funciona para todos los escenarios documentados.

---

## Fase 7 — Pruebas

**Objetivo:** Establecer la infraestructura de pruebas y crear las pruebas de la arquitectura base y de la integración con la API.

**Estado:** 🔴 BLOQUEADA — Depende de la Fase 5 y de la resolución de DEC-MOV-011 y DEC-MOV-012.

### Actividades previstas

1. Seleccionar las herramientas de prueba (DEC-MOV-012).
2. Crear pruebas unitarias para la lógica de la capa de aplicación y datos.
3. Crear pruebas de widgets para los componentes de interfaz críticos.
4. Crear pruebas de integración para los flujos principales.
5. Verificar que las pruebas se ejecutan correctamente en el entorno local.
6. Documentar la estrategia de pruebas adoptada.

### Dependencias

- Fase 5 completada.
- DEC-MOV-011: Umbral mínimo de cobertura.
- DEC-MOV-012: Herramientas de prueba.

### Entregables esperados

- Suite de pruebas unitarias, de widgets y de integración de la arquitectura base.
- Documentación de la estrategia de pruebas adoptada.

### Criterios de salida

- Las pruebas unitarias pasan sin conexión de red.
- El umbral de cobertura definido en DEC-MOV-011 se cumple.
- Las pruebas de integración validan los criterios de aceptación de la arquitectura.

---

## Fase 8 — Automatización de comprobaciones (CI/CD)

**Objetivo:** Configurar el pipeline de integración continua para la ejecución automática de pruebas y validación de la calidad del código.

**Estado:** 🔴 BLOQUEADA — Depende de la Fase 7.

### Actividades previstas

1. Seleccionar la herramienta de CI/CD para la app móvil (alineada con el resto del sistema).
2. Crear el pipeline de integración continua.
3. Configurar la ejecución automática de pruebas en cada commit o pull request.
4. Configurar el análisis estático de código Dart (`dart analyze`, `flutter analyze`).
5. Documentar el pipeline y su configuración.

### Dependencias

- Fase 7 completada.
- Repositorio configurado con protección de ramas y `.gitignore` apropiado.

### Entregables esperados

- Pipeline de CI configurado y funcionando.
- Ejecución automática de pruebas y análisis estático verificada.

### Criterios de salida

- El pipeline ejecuta las pruebas automáticamente y falla si alguna prueba no pasa.
- El análisis estático de código no reporta errores críticos.

---

## Fase 9 — Preparación de la entrega

**Objetivo:** Preparar la aplicación para su distribución en las plataformas objetivo (App Store, Google Play u otras).

**Estado:** 🔴 BLOQUEADA — Depende de la Fase 8 y de la resolución de DEC-MOV-009.

### Actividades previstas

1. Seleccionar la estrategia de publicación y distribución (DEC-MOV-009).
2. Configurar la firma de la aplicación para Android e iOS.
3. Configurar el pipeline de entrega continua (CD) para generar artefactos distribuibles.
4. Preparar los metadatos de las tiendas de aplicaciones (nombre, descripción, capturas, etc.) si aplica.
5. Realizar una prueba de la distribución en el entorno de staging.
6. Documentar el proceso de distribución.

### Dependencias

- Fase 8 completada.
- DEC-MOV-009: Estrategia de publicación y distribución.
- Cuentas de desarrollador en las tiendas de aplicaciones si aplica.

### Entregables esperados

- Artefacto distribuible (APK/AAB para Android, IPA para iOS) generado correctamente.
- Pipeline de CD configurado.
- Documentación del proceso de distribución.

### Criterios de salida

- La aplicación se distribuye correctamente en el entorno de staging.
- El pipeline de CD genera artefactos firmados sin errores.
- Los secretos de firma no están en el repositorio.

---

## Resumen de dependencias entre fases

```
Fase 1 (Validación documental)
  └── Fase 2 (Aprobación arquitectura móvil)
        └── Fase 3 (Preparación entorno Flutter)
              └── Fase 5 (Implementación estructura base)
        
  Fase 4 (Contratos con backend) ──────────────────► Fase 5
  [puede iniciarse tras Fase 1, en paralelo con Fase 3]

              Fase 5 ──── Fase 6 (Integración con API)
                    └──── Fase 7 (Pruebas)
                               └── Fase 8 (CI/CD)
                                       └── Fase 9 (Preparación entrega)
```

---

## Bloqueos identificados

| Bloqueo | Fases afectadas | Dependencia |
|---------|----------------|-------------|
| DEC-MOV-001: Versión de Flutter/Dart sin confirmar | Fase 3 | Decisión técnica pendiente |
| DEC-MOV-002: Gestión de estado sin seleccionar | Fase 5 | Decisión de arquitectura pendiente |
| DEC-MOV-003: Navegación sin seleccionar | Fase 5 | Decisión de arquitectura pendiente |
| DEC-MOV-004: Cliente HTTP sin seleccionar | Fase 5 | Decisión de arquitectura pendiente |
| DEC-MOV-006: Contratos de API sin definir | Fase 5, 6 | Coordinación con el backend |
| DEC-MOV-009: Estrategia de distribución sin confirmar | Fase 9 | Decisión de negocio pendiente |
| DEC-MOV-011/012: Pruebas sin definir | Fase 7 | Decisiones técnicas pendientes |
| Backend disponible en entorno de desarrollo | Fase 6 | Dependencia del equipo del backend |

---

*Este plan no tiene fechas asignadas. Las duraciones y el calendario deben acordarse cuando cada fase sea aprobada para iniciarse. No se han ejecutado actividades de ninguna fase.*
