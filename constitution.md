# Constitución de la Aplicación Móvil de BusTrack

**Versión:** 1.0.0  
**Estado:** Vigente  
**Ámbito:** Aplicación móvil de BusTrack (`bustrack_app`)  
**Última actualización:** 2026-10-28

---

## 1. Propósito y alcance de esta constitución

Esta constitución establece los principios normativos, restricciones obligatorias y reglas de coherencia que rigen el diseño, la documentación y la futura implementación de la **aplicación móvil de BusTrack**.

Es el documento de referencia de mayor jerarquía dentro de este repositorio. Cualquier documento, especificación, plan, tarea o contribución de código debe ser coherente con las reglas aquí establecidas. En caso de contradicción entre esta constitución y otro documento, prevalece esta constitución.

**Relación con la constitución general del sistema:** La presente constitución está alineada con y subordinada a los principios generales del sistema BusTrack. En caso de conflicto con una norma del sistema superior, este conflicto debe registrarse en `memoria.md` para su resolución.

**Alcance:**
- Aplica a todo el contenido del repositorio `bustrack_app`.
- Aplica a cualquier agente de IA, colaborador humano o herramienta automatizada que trabaje sobre este repositorio.
- No aplica a los repositorios del backend (`BusTrack_Back`) ni de la plataforma web (Angular), aunque sí define cómo la aplicación móvil interactuará con el backend.
- No autoriza modificaciones al backend ni a la plataforma web.

---

## 2. Principios obligatorios de Spec-Driven Development (SDD)

El desarrollo de la aplicación móvil sigue la metodología **Spec-Driven Development**. Estos principios son obligatorios y no negociables:

1. **La especificación precede a la implementación.** Ninguna funcionalidad puede codificarse sin una especificación aprobada previa que la describa.
2. **La documentación es la fuente de verdad.** El código debe derivarse de los documentos SDD, no al revés.
3. **Los cambios de especificación requieren aprobación.** Ninguna decisión arquitectónica o funcional puede modificarse unilateralmente. Los cambios deben proponerse, discutirse y registrarse en `memoria.md`.
4. **La trazabilidad es obligatoria.** Toda tarea en `task.md` debe referirse a una especificación en `spec.md` o a una fase en `plan.md`.
5. **Las decisiones pendientes no deben inventarse.** Si una decisión aún no está confirmada, debe registrarse como pendiente y no asumir un valor arbitrario.
6. **Las etapas son secuenciales.** No se puede comenzar la implementación de una fase sin haber completado la documentación de las fases anteriores y sin la aprobación correspondiente.

---

## 3. Reglas de coherencia entre documentos

Los documentos del repositorio forman una jerarquía normativa:

| Nivel | Documento | Función |
|-------|-----------|---------|
| 1 | `constitution.md` | Norma suprema; define principios y restricciones |
| 2 | `AGENTS.md` | Instrucciones operativas para agentes y colaboradores |
| 3 | `memoria.md` | Registro de decisiones, estado y contexto del proyecto |
| 4 | `spec.md` | Especificación técnica de la arquitectura base |
| 5 | `plan.md` | Plan de implementación por fases |
| 6 | `task.md` | Desglose de tareas trazables |
| 7 | `subagents/` | Definición de roles y restricciones de subagentes |
| 8 | `skills/` | Procedimientos reutilizables de revisión |

**Reglas:**
- Los documentos de nivel inferior no pueden contradecir a los de nivel superior.
- Si se detecta una contradicción, debe registrarse en `memoria.md` como conflicto pendiente de resolución antes de continuar.
- Ningún documento puede eliminarse sin aprobación explícita.
- Las actualizaciones deben reflejarse en todos los documentos afectados.

---

## 4. Stack tecnológico: decisiones confirmadas e inamovibles

Las siguientes decisiones tecnológicas están confirmadas y no pueden modificarse sin aprobación explícita y documentada:

| Aspecto | Decisión |
|---------|----------|
| Framework móvil | Flutter |
| Lenguaje | Dart |
| Comunicación con backend | API REST mediante HTTPS y JSON |
| Backend consumido | ASP.NET Core Web API |
| Metodología | Spec-Driven Development (SDD) |
| Gestión de versiones | GitHub |
| Documentación | Markdown |

**Restricciones obligatorias:**
- **Prohibido** adoptar un framework móvil diferente a Flutter sin aprobación explícita.
- **Prohibido** que la aplicación acceda directamente a la base de datos en ningún escenario.
- **Prohibido** que la aplicación almacene credenciales de acceso a la base de datos.
- **Prohibido** seleccionar como definitivas las decisiones pendientes sin aprobación.

---

## 5. Separación de responsabilidades (arquitectura en capas)

La aplicación móvil se organizará en capas con responsabilidades claramente delimitadas:

| Capa | Responsabilidad |
|------|----------------|
| **Presentación** | Widgets, pantallas, navegación visual, manejo de eventos de usuario |
| **Aplicación** | Lógica de aplicación, gestión de estado, coordinación entre presentación y datos |
| **Datos** | Acceso a la API REST, modelos de datos, transformación JSON |

> **Nota:** Esta estructura de capas es una propuesta arquitectónica que deberá validarse durante la fase de diseño de la arquitectura. No afirma que esté implementada actualmente.

**Reglas obligatorias:**
- La capa de presentación no debe contener lógica de negocio ni llamadas directas a la API.
- La capa de datos no debe depender de widgets ni de la lógica de presentación.
- Las dependencias deben dirigirse desde la presentación hacia los datos, no al revés.
- No se permiten llamadas HTTP directas desde los widgets.
- Los modelos de datos son responsabilidad de la capa de datos; no deben mezclarse con el estado de la interfaz.

---

## 6. Principios de comunicación con el backend

**Decisiones confirmadas:**
- La comunicación se realiza exclusivamente mediante **HTTPS**.
- El formato de intercambio es **JSON**.
- La aplicación móvil consume la misma API REST que la plataforma web.
- Los datos de transporte se obtienen dinámicamente desde el backend; no se codifican catálogos estáticos en la aplicación.

**Reglas obligatorias:**
- Las credenciales de usuario no se almacenan en texto plano en el dispositivo.
- Los tokens de sesión deben gestionarse de forma segura.
- La aplicación no debe acceder directamente a la base de datos en ningún escenario.
- Los endpoints concretos y los contratos de API deben derivarse de especificaciones aprobadas, no inventarse.

**Pendientes de aprobación:**
- Cliente HTTP concreto (p. ej., `http`, `dio`, u otro).
- Estrategia de manejo de errores de red (reintentos, timeout, circuit breaker).
- Contratos funcionales definitivos de la API.

---

## 7. Principios de seguridad y privacidad

**Principios obligatorios:**
1. **Sin credenciales de base de datos:** La aplicación jamás debe contener ni gestionar credenciales de acceso directo a la base de datos.
2. **Sin secretos en el repositorio:** Ninguna clave de API, token, URL de producción ni secreto puede almacenarse en el código fuente o en archivos versionados.
3. **HTTPS obligatorio:** La comunicación con el backend debe realizarse exclusivamente mediante HTTPS.
4. **Gestión segura de tokens:** Los tokens de autenticación deben almacenarse usando mecanismos seguros del sistema operativo, no en texto plano.
5. **Validación de respuestas:** Los datos recibidos del backend deben validarse antes de ser usados en la interfaz.
6. **Sin datos sensibles en logs:** Los logs de depuración no deben incluir credenciales, tokens ni datos personales del usuario.
7. **Principio de mínimo almacenamiento local:** Solo debe persistirse localmente la información estrictamente necesaria para la experiencia de usuario, con justificación documentada.

**Pendientes de aprobación:**
- Mecanismo de autenticación concreto (alineado con el backend).
- Estrategia definitiva de almacenamiento local seguro.
- Política de manejo de datos personales del usuario en el dispositivo.

---

## 8. Gestión de configuración

**Reglas obligatorias:**
- Los valores de configuración sensibles (URLs de producción, claves de API) no deben hardcodearse en el código fuente.
- La configuración debe separarse por entorno: desarrollo, pruebas, producción.
- Los archivos de configuración local de desarrollo deben excluirse del repositorio mediante `.gitignore`.
- Los identificadores de recursos de producción no deben estar en el repositorio.

**Pendiente de aprobación:**
- Estrategia definitiva de configuración por entorno en Flutter (variables de entorno, archivos de configuración, `--dart-define`, u otro).

---

## 9. Calidad, pruebas y mantenibilidad

**Principios obligatorios:**
- El código debe ser legible, mantenible y coherente con las convenciones del ecosistema Dart/Flutter.
- Las funcionalidades deben acompañarse de pruebas automatizadas.
- Se contemplan, como mínimo: pruebas unitarias para la lógica de aplicación y datos, y pruebas de widgets para los componentes de presentación críticos.
- La cobertura de pruebas no debe reducirse con cada nueva contribución.
- El manejo de errores debe ser consistente y centralizado.

**Pendiente de aprobación:**
- Umbral mínimo de cobertura de pruebas.
- Herramientas y bibliotecas específicas de prueba.
- Estrategia de pruebas de integración con el backend.

---

## 10. Requisitos de mantenibilidad y accesibilidad

**Principios obligatorios:**
- La aplicación debe ser compatible con las versiones de Android e iOS que se definan en las especificaciones funcionales aprobadas.
- Los componentes de la interfaz deben seguir buenas prácticas de accesibilidad (etiquetas semánticas, contraste de color adecuado).
- Los textos de la interfaz no deben hardcodearse de forma que impidan la futura internacionalización, aunque la internacionalización misma no es un requisito de la fase actual.
- La arquitectura debe permitir la incorporación de nuevas funcionalidades sin refactorizaciones masivas.

---

## 11. Restricciones sobre almacenamiento local

**Reglas obligatorias:**
- No se debe conectar la aplicación directamente a ninguna base de datos (local o remota) sin pasar por el backend.
- Cualquier estrategia de almacenamiento local (caché, preferencias, almacenamiento offline) debe ser aprobada y documentada antes de implementarse.
- Los datos almacenados localmente deben poder eliminarse de forma controlada (por ejemplo, al cerrar sesión).

**Pendiente de aprobación:**
- Estrategia definitiva de almacenamiento local (preferencias, base de datos local, caché, u otro).
- Política de invalidación y expiración de caché.

---

## 12. Prohibición de implementar funcionalidades no especificadas

**Regla obligatoria:** Ninguna funcionalidad que no haya sido previamente especificada en un documento `spec.md` aprobado puede implementarse.

Funcionalidades fuera del alcance de la arquitectura base (reservadas para especificaciones futuras):
- Registro, autenticación y recuperación de contraseña.
- Consulta y búsqueda de rutas, paradas, destinos y horarios.
- Cálculo y consulta de tarifas.
- Gestión de calificaciones y comentarios.
- Recomendaciones mediante inteligencia artificial.
- Detección de paradas mediante acelerómetro.
- Operaciones administrativas específicas.
- Integraciones definitivas con proveedores externos.
- Seguimiento GPS continuo de vehículos o usuarios.

---

## 13. Control de cambios y aprobación de decisiones

**Proceso obligatorio para modificar la constitución o cualquier decisión confirmada:**

1. Identificar la decisión o regla que se desea modificar.
2. Documentar la propuesta de cambio en `memoria.md` con justificación.
3. Registrar el cambio como **Propuesto** hasta que reciba aprobación explícita.
4. Solo tras la aprobación, actualizar los documentos afectados.
5. Registrar la decisión aprobada en el historial de `memoria.md`.

**Prohibiciones:**
- No modificar decisiones confirmadas sin seguir este proceso.
- No asumir que una propuesta está aprobada por falta de respuesta.
- No introducir cambios técnicos que contradigan la constitución sin aprobación previa.

---

## 14. Criterios para considerar conforme una contribución

Una contribución (documento, código o configuración) se considera **conforme** cuando:

1. Es coherente con esta constitución y con todos los documentos de nivel superior.
2. No contradice ninguna decisión confirmada.
3. No implementa funcionalidades no especificadas.
4. No contiene secretos ni información sensible.
5. Está acompañada de la actualización correspondiente en `memoria.md` si modifica alguna decisión.
6. Las tareas que documenta están en el estado correcto (no marcadas como completadas sin evidencia).
7. Respeta las convenciones de nomenclatura, idioma y formato establecidas.

---

## 15. Regla de no ejecución durante la etapa documental

**En la etapa actual, esta constitución establece explícitamente:**

- No se debe programar ninguna funcionalidad.
- No se deben crear proyectos Flutter ni archivos de código Dart.
- No se deben instalar paquetes ni dependencias.
- No se deben ejecutar comandos de desarrollo.
- No se deben crear recursos en Azure ni servicios externos.
- No se debe publicar ni distribuir la aplicación.
- No se deben marcar tareas como completadas por el simple hecho de haberlas escrito.

El resultado de la etapa actual es exclusivamente **documentación SDD**.

---

## 16. Convenciones generales de documentación

**Idioma:**
- La documentación técnica se escribe en **español técnico**.
- El código fuente, nombres de clases, métodos, variables y comentarios de código se escribirán en **inglés**, siguiendo las convenciones de Dart y Flutter.

**Nomenclatura de archivos:**
- Los archivos Markdown en la raíz del repositorio usan nombres en minúsculas: `constitution.md`, `spec.md`, `plan.md`, `task.md`, `memoria.md`.
- Las excepciones son: `AGENTS.md` y `README.md` (en mayúsculas por convención universal).

**Identificadores:**
- Los identificadores de tareas y decisiones deben ser estables y únicos; no se reutilizan identificadores eliminados.

---

## Historial de la constitución

| Versión | Fecha | Descripción |
|---------|-------|-------------|
| 1.0.0 | 2026-10-28 | Versión inicial de la constitución de la aplicación móvil de BusTrack |
