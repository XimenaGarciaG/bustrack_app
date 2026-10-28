# memoria.md — Registro de Contexto y Decisiones Técnicas

**Versión:** 1.0.0  
**Estado:** Activo  
**Ámbito:** Aplicación móvil de BusTrack (`bustrack_app` — Flutter)  
**Última actualización:** 2026-10-28

> Este documento registra el contexto, las decisiones técnicas y su estado dentro del proyecto de la aplicación móvil de BusTrack. Es la fuente de verdad sobre qué está confirmado, qué está pendiente y qué está fuera del alcance actual.

---

## 1. Descripción del proyecto

**BusTrack** es un sistema multiplataforma de consulta y planificación de transporte público. Permite a los usuarios consultar información sobre empresas y asociaciones de transporte, medios de transporte, rutas, paradas, destinos, horarios de corridas, tarifas y calificaciones.

El sistema está compuesto por:

| Componente | Tecnología | Estado |
|------------|------------|--------|
| **Aplicación móvil** | Flutter + Dart | **Este repositorio** |
| Plataforma web | Angular + TypeScript | Repositorio separado |
| Backend centralizado | ASP.NET Core Web API + C# | Repositorio separado (`BusTrack_Back`) |
| Base de datos | NoSQL en Azure | Proveedor pendiente de selección |

La aplicación móvil es un **cliente de la API REST central**. No accede directamente a la base de datos. No almacena credenciales de acceso a la base de datos. Los datos de transporte se obtienen dinámicamente desde el backend.

---

## 2. Arquitectura confirmada

| Aspecto | Decisión confirmada |
|---------|---------------------|
| Framework móvil | Flutter |
| Lenguaje | Dart |
| Patrón de comunicación | API REST mediante HTTPS y JSON |
| Backend consumido | ASP.NET Core Web API |
| Organización interna | Capas con separación de responsabilidades |
| Acceso a datos | Solo a través de la API; sin acceso directo a la base de datos |
| Datos de transporte | Obtenidos dinámicamente desde el backend |
| Metodología | Spec-Driven Development (SDD) |

**Capas propuestas (pendientes de aprobación de estructura definitiva):**

| Capa | Responsabilidad | Estado |
|------|----------------|--------|
| Presentación | Widgets, pantallas, navegación, manejo de eventos de usuario | Propuesto |
| Aplicación | Lógica de aplicación, gestión de estado, coordinación entre capas | Propuesto |
| Datos | Acceso a la API REST, modelos de datos, transformación JSON | Propuesto |

> La estructura de capas es una propuesta arquitectónica. No está implementada. Debe validarse durante la fase de diseño de la arquitectura.

---

## 3. Stack tecnológico

| Componente | Tecnología | Versión | Estado |
|------------|------------|---------|--------|
| Framework móvil | Flutter | Por confirmar | Confirmado (versión pendiente) |
| Lenguaje | Dart | Acorde a la versión de Flutter | Confirmado |
| Comunicación | HTTPS + JSON | N/A | Confirmado |
| Gestión de estado | Por confirmar | — | **Pendiente** |
| Navegación | Por confirmar | — | **Pendiente** |
| Cliente HTTP | Por confirmar | — | **Pendiente** |
| Almacenamiento local | Por confirmar | — | **Pendiente** |
| Autenticación (mecanismo) | Por confirmar (alineado con backend) | — | **Pendiente** |
| CI/CD | Por confirmar | — | **Pendiente** |
| Distribución | Por confirmar | — | **Pendiente** |

---

## 4. Decisiones pendientes

Las siguientes decisiones no pueden convertirse en requisitos definitivos sin aprobación explícita. No deben asumirse valores concretos para estas decisiones.

| ID | Decisión | Impacto si se demora | Bloquea |
|----|----------|---------------------|---------|
| DEC-MOV-001 | Versión exacta de Flutter y Dart | No se puede definir la configuración del entorno | Fases 3, 4 del plan |
| DEC-MOV-002 | Biblioteca de gestión de estado (Provider, Riverpod, Bloc, GetX, u otro) | No se puede diseñar la capa de aplicación | Fases 4, 5 del plan |
| DEC-MOV-003 | Biblioteca de navegación (GoRouter, Navigator 2.0, AutoRoute, u otro) | No se puede diseñar la arquitectura de navegación | Fases 4, 5 del plan |
| DEC-MOV-004 | Cliente HTTP concreto (`http`, `dio`, u otro) | No se puede diseñar la capa de datos | Fase 5 del plan |
| DEC-MOV-005 | Estrategia definitiva de almacenamiento local | No se puede definir la persistencia local | Fase 5 del plan |
| DEC-MOV-006 | Contratos funcionales definitivos de la API (endpoints, modelos de respuesta) | No se pueden implementar los repositorios | Fase 6 del plan |
| DEC-MOV-007 | Versiones exactas de las dependencias de Flutter/Dart | No se puede preparar el entorno reproducible | Fase 3 del plan |
| DEC-MOV-008 | Funcionalidades específicas autorizadas para implementar | No se puede iniciar la implementación funcional | Fase 7 del plan |
| DEC-MOV-009 | Estrategia de publicación y distribución (App Store, Play Store, otros) | No se puede planificar la entrega | Fase 9 del plan |
| DEC-MOV-010 | Mecanismo de autenticación en el cliente (alineado con el backend) | No se puede diseñar el flujo de autenticación | Fases 5, 6 del plan |
| DEC-MOV-011 | Umbral mínimo de cobertura de pruebas | No se puede validar la calidad del código | Fase 7 del plan |
| DEC-MOV-012 | Herramientas específicas de prueba (flutter_test, integration_test, mockito, u otro) | No se puede iniciar la implementación de pruebas | Fase 7 del plan |
| DEC-MOV-013 | Estrategia de configuración por entorno en Flutter | No se puede separar la configuración de desarrollo/producción | Fase 3 del plan |
| DEC-MOV-014 | Estructura definitiva de directorios del proyecto Flutter | No se puede iniciar la implementación | Fase 4 del plan |
| DEC-MOV-015 | Plataformas objetivo (Android, iOS, versiones mínimas) | No se puede configurar el proyecto Flutter | Fase 3 del plan |

---

## 5. Restricciones de alcance

Las siguientes funcionalidades están **fuera del alcance de la fase actual** y solo podrán especificarse en fases futuras:

| Funcionalidad | Motivo de exclusión |
|---------------|---------------------|
| Registro, autenticación y recuperación de contraseña | Especificación funcional futura |
| Consulta y búsqueda de rutas, paradas, destinos y horarios | Especificación funcional futura |
| Cálculo y consulta de tarifas | Especificación funcional futura |
| Gestión de calificaciones y comentarios | Especificación funcional futura |
| Recomendaciones mediante inteligencia artificial | Especificación funcional futura |
| Detección de paradas mediante acelerómetro | Especificación funcional futura |
| Operaciones administrativas específicas | Especificación funcional futura |
| Integraciones con proveedores externos definitivos | Especificación funcional futura |
| Seguimiento GPS continuo de vehículos o usuarios | **Fuera del alcance del sistema**: el mapa es de consulta y orientación de rutas registradas, no de rastreo continuo |
| Implementación de pantallas, widgets, modelos, servicios, repositorios | No implementable hasta tener especificación aprobada |

---

## 6. Supuestos que necesitan validación

| ID | Supuesto | Impacto si es incorrecto | Próximo paso |
|----|----------|--------------------------|--------------| 
| SUP-MOV-001 | La aplicación móvil y la web consumen exactamente la misma API sin adaptadores intermedios (no se requiere BFF) | Se requeriría un BFF (Backend for Frontend) u otros adaptadores | Confirmar con el equipo del backend y del sistema |
| SUP-MOV-002 | El sistema no requiere comunicación en tiempo real (WebSockets, notificaciones push de alta frecuencia) en la fase inicial de la app móvil | Requeriría integrar servicios de tiempo real y cambios arquitectónicos | Confirmar alcance de la fase inicial |
| SUP-MOV-003 | La aplicación funcionará primariamente con conexión a internet; la funcionalidad offline es secundaria y requiere especificación aprobada | Requeriría estrategias de sincronización y almacenamiento local más complejas | Confirmar con los requisitos del proyecto |
| SUP-MOV-004 | Los contratos de la API (endpoints, modelos JSON) serán diseñados conjuntamente con el equipo del backend antes de la implementación móvil | Los modelos de datos y repositorios implementados podrían ser incompatibles | Iniciar definición de contratos una vez aprobada la arquitectura base |
| SUP-MOV-005 | La documentación SDD es revisada y aprobada por el profesor antes de iniciar la implementación | El trabajo de implementación podría invalidarse si la especificación cambia | Someter los documentos a revisión antes de avanzar |
| SUP-MOV-006 | Flutter es la versión estable actual en el momento de iniciar la implementación | Podría requerirse una migración si la versión tiene cambios de ruptura relevantes | Confirmar la versión en la fase de preparación del entorno (DEC-MOV-001) |

---

## 7. Riesgos conocidos

| ID | Riesgo | Probabilidad | Impacto | Mitigación propuesta |
|----|--------|-------------|---------|---------------------|
| RIESGO-MOV-001 | La selección tardía de la biblioteca de gestión de estado afecta el diseño arquitectónico | Alta | Alto | Priorizar DEC-MOV-002 antes de iniciar la Fase 4 |
| RIESGO-MOV-002 | Los contratos de la API no están definidos antes de iniciar la implementación móvil | Alta | Alto | Coordinar con el equipo del backend; priorizar DEC-MOV-006 |
| RIESGO-MOV-003 | Inconsistencia entre los modelos de datos del cliente y los del backend | Media | Alto | Definir contratos compartidos antes de implementar repositorios |
| RIESGO-MOV-004 | Cambios de versión en Flutter con ruptura de APIs entre la especificación y la implementación | Media | Medio | Fijar versión en DEC-MOV-001; evaluar antes de implementar |
| RIESGO-MOV-005 | Las bibliotecas seleccionadas para gestión de estado o navegación quedan sin mantenimiento | Baja | Medio | Preferir bibliotecas con respaldo de la comunidad Flutter o de Google |
| RIESGO-MOV-006 | Exposición accidental de credenciales o URLs de producción en el repositorio | Baja | Alto | Configurar `.gitignore` y revisar seguridad antes de cualquier commit de código |
| RIESGO-MOV-007 | La aplicación asume una API que cambia durante el desarrollo del backend | Media | Alto | Establecer un proceso de control de cambios de contratos de API |
| RIESGO-MOV-008 | Fragmentación entre plataformas Android/iOS que requiera código específico no anticipado | Baja | Medio | Documentar las plataformas objetivo en DEC-MOV-015 antes de implementar |

---

## 8. Historial de decisiones

| ID | Decisión | Estado | Justificación | Próximo paso |
|----|----------|--------|---------------|--------------| 
| HIST-MOV-001 | Usar Flutter + Dart para la aplicación móvil | **Confirmado** | Stack acordado; ecosistema maduro, soporte oficial Google, multiplataforma (Android/iOS) | Definir versión exacta (DEC-MOV-001) |
| HIST-MOV-002 | API REST con JSON como protocolo de comunicación | **Confirmado** | Estándar ampliamente adoptado; compatible con el backend ASP.NET Core | Definir contratos con el backend (DEC-MOV-006) |
| HIST-MOV-003 | Sin acceso directo a la base de datos desde la app | **Confirmado** | Principio de seguridad fundamental; toda la lógica de negocio reside en el backend | Verificar que ningún agente ni código proponga acceso directo |
| HIST-MOV-004 | Los datos se obtienen dinámicamente desde el backend | **Confirmado** | No se codifican catálogos estáticos de transporte en la aplicación | Documentar en los contratos de API (DEC-MOV-006) |
| HIST-MOV-005 | Arquitectura en capas (Presentación / Aplicación / Datos) | **Propuesto** | Estructura limpia; permite separación de responsabilidades; pendiente de validación | Aprobar en la fase de diseño de arquitectura |
| HIST-MOV-006 | Metodología SDD | **Confirmado** | Metodología establecida por el proyecto académico | Completar documentación antes de iniciar implementación |
| HIST-MOV-007 | HTTPS obligatorio para comunicación con el backend | **Confirmado** | Principio de seguridad; coherente con la constitución del backend | Aplicar al configurar el cliente HTTP en la implementación |
| HIST-MOV-008 | Sin credenciales de base de datos en la app | **Confirmado** | Principio de seguridad fundamental | Verificar que ningún agente proponga almacenar credenciales de BD |

---

## 9. Conflictos y propuestas de cambio pendientes de resolución

*(Sin conflictos registrados en la versión inicial)*

| ID | Descripción del conflicto | Documentos afectados | Estado |
|----|--------------------------|---------------------|--------|
| — | No se han registrado conflictos en la versión inicial | — | — |

---

*Este documento debe actualizarse en cada sesión de trabajo que modifique decisiones, identifique nuevos riesgos o supuestos, o cambie el estado de cualquier decisión pendiente.*
