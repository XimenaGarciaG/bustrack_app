# spec.md — Especificación de Arquitectura Base de la Aplicación Móvil de BusTrack

**Versión:** 1.0.0  
**Estado:** Borrador — Pendiente de revisión y aprobación  
**Última actualización:** 2026-10-28  
**Referencia normativa:** [`constitution.md`](./constitution.md)

---

## 1. Propósito

Este documento especifica la arquitectura base de la **aplicación móvil de BusTrack**, desarrollada con Flutter y Dart. Define la estructura, los principios y las reglas técnicas que deben guiar la construcción del cliente móvil antes de incorporar especificaciones funcionales específicas.

Este documento establece la **base arquitectónica** sobre la que se construirán las funcionalidades futuras. No define pantallas específicas, widgets, modelos de dominio particulares ni endpoints de la API.

---

## 2. Alcance y exclusiones

### Dentro del alcance de esta especificación

- Propósito y rol de la aplicación móvil en el sistema BusTrack.
- Interacción con la API REST del backend.
- Organización en capas de la aplicación (Presentación / Aplicación / Datos).
- Componentes compartidos y de infraestructura móvil.
- Principios de navegación.
- Estrategia general de gestión de estado.
- Comunicación HTTP y procesamiento de JSON.
- Manejo de errores y estados de carga.
- Configuración por entorno.
- Seguridad y protección de datos en el cliente móvil.
- Estrategia de pruebas.
- Requisitos no funcionales.
- Decisiones pendientes que afectan a la arquitectura.
- Criterios de aceptación verificables de la arquitectura base.

### Fuera del alcance de esta especificación

Los siguientes temas se especificarán en documentos funcionales futuros y **no deben incorporarse a esta especificación**:

| Tema excluido | Razón |
|---------------|-------|
| Registro, autenticación y recuperación de contraseña | Especificación funcional futura |
| Consulta y búsqueda de rutas, paradas, destinos y horarios | Especificación funcional futura |
| Cálculo de tarifas | Especificación funcional futura |
| Gestión de calificaciones y comentarios | Especificación funcional futura |
| Recomendaciones mediante IA | Especificación funcional futura |
| Detección de paradas por acelerómetro | Especificación funcional futura |
| Operaciones administrativas específicas | Especificación funcional futura |
| Seguimiento GPS continuo | Fuera del alcance del sistema |
| Pantallas, widgets y diseño visual concreto | Especificación funcional futura |
| Modelos de dominio específicos | Dependen de los contratos de API (DEC-MOV-006) |
| Endpoints concretos de la API | Dependen de los contratos de API (DEC-MOV-006) |
| Biblioteca específica de gestión de estado | Decisión pendiente (DEC-MOV-002) |
| Biblioteca específica de navegación | Decisión pendiente (DEC-MOV-003) |
| Cliente HTTP concreto | Decisión pendiente (DEC-MOV-004) |
| Estrategia de almacenamiento local definitiva | Decisión pendiente (DEC-MOV-005) |

---

## 3. Contexto del sistema y rol de la aplicación móvil

La aplicación móvil de BusTrack es un **cliente de la API REST centralizada**. Su función es presentar al usuario final la información de transporte público que proporciona el backend, sin contener lógica de negocio propia ni acceso directo a los datos.

```
┌─────────────────────────────────────────────────────┐
│           Sistema BusTrack                          │
│                                                     │
│  ┌────────────────────┐   ┌─────────────────────┐  │
│  │  App Móvil         │   │  Plataforma Web      │  │
│  │  (Flutter + Dart)  │   │  (Angular + TS)      │  │
│  │  [Este repositorio]│   │  [Repo separado]     │  │
│  └────────┬───────────┘   └──────────┬────────────┘  │
│           │                          │              │
│           │      HTTPS / REST / JSON │              │
│           └──────────────┬───────────┘              │
│                          │                          │
│             ┌────────────▼──────────┐               │
│             │   Backend BusTrack    │               │
│             │  ASP.NET Core Web API │               │
│             │  [Repo separado]      │               │
│             └────────────┬──────────┘               │
│                          │                          │
│             ┌────────────▼──────────┐               │
│             │  Base de Datos NoSQL  │               │
│             │  (Azure — proveedor   │               │
│             │   pendiente)          │               │
│             └───────────────────────┘               │
└─────────────────────────────────────────────────────┘
```

**Características del contexto:**

- La aplicación móvil **no tiene acceso directo** a la base de datos.
- La aplicación móvil **no almacena credenciales** de la base de datos.
- Los datos de transporte se **obtienen dinámicamente** desde el backend; no se codifican catálogos estáticos.
- La aplicación móvil y la plataforma web consumen la misma API REST (ver SUP-MOV-001 en `memoria.md`).
- No existe comunicación directa entre la aplicación móvil y la plataforma web; toda comunicación pasa por el backend.
- La aplicación móvil es un consumidor de la API, no un administrador del sistema.

---

## 4. Arquitectura general: cliente REST en capas

La aplicación móvil se organiza en tres capas con responsabilidades claramente delimitadas. Esta estructura es una propuesta arquitectónica pendiente de aprobación (ver HIST-MOV-005 en `memoria.md`).

### Vista general de capas

```
┌──────────────────────────────────────────────┐
│           Capa de Presentación               │
│   Widgets · Pantallas · Navegación           │
│   Manejo de eventos de usuario               │
└──────────────────────┬───────────────────────┘
                       │ (consume estado / dispara eventos)
┌──────────────────────▼───────────────────────┐
│           Capa de Aplicación                 │
│   Gestión de estado · Lógica de aplicación  │
│   Coordinación · Transformación de datos    │
└──────────────────────┬───────────────────────┘
                       │ (solicita y recibe datos)
┌──────────────────────▼───────────────────────┐
│           Capa de Datos                      │
│   Repositorios · Fuentes de datos (API)      │
│   Modelos de datos · Parseo JSON             │
└──────────────────────┬───────────────────────┘
                       │ (solicitudes HTTP)
                ┌──────▼──────┐
                │ API REST    │
                │  (Backend)  │
                └─────────────┘
```

### Flujo de una solicitud (ilustrativo)

```
Usuario interactúa con la UI
  │
  ▼
[Widget / Pantalla] — Delega el evento a la capa de aplicación
  │
  ▼
[Gestor de estado / Lógica de aplicación] — Solicita datos al repositorio
  │
  ▼
[Repositorio] — Invoca la fuente de datos correspondiente
  │
  ▼
[Fuente de datos (API)] — Realiza la solicitud HTTP al backend
  │
  ▼
[Backend BusTrack] — Responde con JSON
  │
  ▼
[Modelo de datos] — Parsea la respuesta JSON
  │
  ▼
[Gestor de estado] — Actualiza el estado con los datos obtenidos
  │
  ▼
[Widget / Pantalla] — Se reconstruye con el nuevo estado
```

> **Nota:** Este flujo es ilustrativo. Los componentes concretos (gestor de estado, cliente HTTP, etc.) dependen de decisiones pendientes (DEC-MOV-002, DEC-MOV-003, DEC-MOV-004).

---

## 5. Descripción de las capas

### 5.1 Capa de Presentación

**Responsabilidades:**
- Renderizar la interfaz de usuario mediante widgets de Flutter.
- Recibir los eventos del usuario (taps, entradas de texto, gestos).
- Suscribirse al estado expuesto por la capa de aplicación y reconstruirse cuando cambia.
- Delegar toda la lógica al nivel de aplicación o de datos.
- Gestionar la navegación entre pantallas siguiendo los principios definidos.

**Lo que NO hace:**
- No contiene lógica de negocio ni reglas de dominio.
- No realiza llamadas directas a la API REST.
- No accede directamente a servicios de datos.
- No transforma ni parsea modelos de datos.

**Candidatos de contenido (pendiente de diseño detallado):**
- Widgets de pantalla (Screen Widgets).
- Widgets de componente (Component Widgets) reutilizables.
- Widgets de estado de carga y error.
- Configuración de rutas de navegación.
- Temas y estilos de la aplicación.

### 5.2 Capa de Aplicación

**Responsabilidades:**
- Gestionar el estado de la aplicación y exponerlo a la capa de presentación.
- Coordinar las solicitudes entre la presentación y los repositorios de datos.
- Aplicar transformaciones y adaptaciones de los datos obtenidos antes de exponerlos.
- Gestionar el ciclo de vida de los estados de carga, error y éxito.
- Implementar la lógica de aplicación no perteneciente al dominio de negocio.

**Lo que NO hace:**
- No realiza llamadas directas a la API REST.
- No renderiza widgets ni gestiona la interfaz directamente.
- No implementa reglas de negocio del dominio (esas residen en el backend).

**Candidatos de contenido (pendiente de diseño detallado y de DEC-MOV-002):**
- Gestores de estado (la biblioteca concreta es una decisión pendiente).
- Controladores de aplicación.
- Modelos de estado de la interfaz (UI State Models).
- Servicios de aplicación.

### 5.3 Capa de Datos

**Responsabilidades:**
- Abstraer el origen de los datos (API REST, caché local, etc.) del resto de la aplicación.
- Implementar los repositorios que consumen la API REST del backend.
- Serializar las solicitudes y deserializar las respuestas JSON.
- Gestionar los errores de comunicación con la API.
- Implementar la caché local si se requiere (pendiente de decisión DEC-MOV-005).

**Lo que NO hace:**
- No contiene lógica de presentación ni de estado de la interfaz.
- No implementa reglas de negocio.
- No expone detalles de implementación HTTP a las capas superiores.

**Candidatos de contenido (pendiente de diseño detallado y de DEC-MOV-004, DEC-MOV-006):**
- Repositorios (interfaces e implementaciones).
- Fuentes de datos remotas (Remote Data Sources).
- Modelos de datos (clases Dart que representan las respuestas JSON de la API).
- Adaptadores de serialización/deserialización.
- Fuentes de datos locales (Local Data Sources), si aplica.

---

## 6. Componentes compartidos e infraestructura móvil

### 6.1 Gestión de configuración por entorno

La aplicación debe soportar múltiples entornos de ejecución:

| Entorno | Propósito |
|---------|-----------|
| Desarrollo | Trabajo local del desarrollador |
| Pruebas | Ejecución de pruebas automatizadas |
| Staging | Validación previa a producción |
| Producción | Uso final de la aplicación |

La estrategia concreta de configuración por entorno en Flutter está pendiente de decisión (DEC-MOV-013). Ningún valor de producción debe almacenarse en el código fuente ni en archivos versionados.

### 6.2 Manejo de errores y estados de carga

La aplicación debe gestionar de forma consistente los siguientes estados de cualquier operación asíncrona:

| Estado | Descripción |
|--------|-------------|
| **Cargando** | La operación está en progreso; se muestra un indicador al usuario |
| **Éxito** | La operación completó con datos válidos; se muestra el contenido |
| **Error** | La operación falló; se muestra un mensaje apropiado y una acción de recuperación |
| **Vacío** | La operación completó pero no hay datos que mostrar |

**Principios del manejo de errores:**
- Los errores de red deben distinguirse de los errores de negocio (respuestas de error del backend).
- Los mensajes de error mostrados al usuario deben ser comprensibles y accionables.
- Los errores no deben exponer detalles técnicos internos al usuario.
- Debe existir siempre una acción de recuperación (reintentar, volver atrás) cuando sea posible.
- Los errores deben registrarse de forma diagnóstica sin incluir datos personales del usuario.

### 6.3 Logging y diagnóstico

- La aplicación debe emitir registros diagnósticos durante el desarrollo.
- Los registros de producción no deben incluir datos personales ni credenciales.
- Se debe contemplar la integración con un servicio de monitoreo de errores en producción (decisión pendiente, no parte de la arquitectura base).

---

## 7. Principios de navegación

La navegación de la aplicación debe seguir estos principios generales. La biblioteca y estrategia concreta de navegación están pendientes de decisión (DEC-MOV-003).

**Principios obligatorios:**
- La navegación debe ser declarativa o semi-declarativa, coherente con las mejores prácticas de Flutter.
- El historial de navegación debe ser predecible y gestionable (soporte para botón de retroceso en Android).
- Las rutas de la aplicación deben estar centralizadas en un único lugar, no dispersas en los widgets.
- La navegación no debe acoplarse directamente a los repositorios o fuentes de datos.
- Las rutas deben poder representarse como URLs (deep links) para facilitar la navegación desde notificaciones o enlaces externos, si aplica en el futuro.

**Tipos de navegación contemplados (ilustrativo, no definitivo):**
- Navegación entre pantallas principales (stack de navegación).
- Navegación en pestañas (bottom navigation bar o similar).
- Navegación modal (diálogos, bottom sheets).
- Flujos de incorporación (onboarding) si aplica.

---

## 8. Estrategia general de gestión de estado

La gestión de estado es una decisión arquitectónica crítica pendiente de selección (DEC-MOV-002). Esta sección define los principios que debe cumplir cualquier solución adoptada, independientemente de la biblioteca específica elegida.

**Principios obligatorios para la solución de gestión de estado:**

1. **Separación:** El estado de la aplicación debe estar separado de los widgets que lo consumen.
2. **Reactividad:** Los widgets deben reconstruirse automáticamente cuando el estado relevante cambia.
3. **Testabilidad:** El estado debe poder probarse unitariamente sin necesidad de la interfaz gráfica.
4. **Predecibilidad:** Los cambios de estado deben ser trazables y predecibles.
5. **Granularidad:** Solo los widgets afectados por un cambio de estado deben reconstruirse.
6. **Sin lógica en widgets:** Los widgets de pantalla no deben contener lógica de negocio ni de aplicación.

**Candidatos a evaluar (ninguno es una decisión confirmada):**

| Candidato | Observación |
|-----------|-------------|
| Riverpod | Popular en la comunidad Flutter; diseñado por el autor de Provider |
| Bloc / Cubit | Arquitectura bien definida; buena separación de eventos y estados |
| Provider | Solución oficial de Google; ampliamente utilizada |
| GetX | Todo-en-uno (estado, navegación, DI); menor separación de responsabilidades |

> La evaluación y selección definitiva es responsabilidad del equipo, con documentación en `memoria.md` bajo DEC-MOV-002.

---

## 9. Comunicación HTTP y procesamiento de JSON

### Protocolo de comunicación

- La comunicación con el backend se realiza exclusivamente mediante **HTTPS**.
- El formato de intercambio es **JSON**.
- La aplicación no debe aceptar respuestas en otros formatos.
- Se debe validar que las respuestas recibidas tienen el formato esperado antes de procesarlas.

### Estructura de una solicitud (principio general)

```
Repositorio
  │
  ├── Construye la solicitud (URL, método, headers, body si aplica)
  ├── Incluye el token de autenticación en los headers (mecanismo pendiente DEC-MOV-010)
  │
  ▼
Cliente HTTP (biblioteca pendiente DEC-MOV-004)
  │
  ├── Realiza la solicitud HTTP al backend
  ├── Recibe la respuesta
  │
  ▼
Fuente de datos
  ├── Verifica el código de estado HTTP
  ├── Si es éxito: parsea el JSON al modelo de datos correspondiente
  └── Si es error: convierte el error HTTP en una excepción tipada de la aplicación
```

### Convenciones de JSON esperadas del backend

Coherente con la especificación del backend (`spec.md` del repositorio `BusTrack_Back`):
- Las propiedades de los objetos JSON usan **camelCase**.
- Las fechas están en formato **ISO 8601**.
- Los errores del backend siguen una estructura uniforme (pendiente de definición definitiva — DEC-MOV-006 y el DEC-010 del backend).

### Manejo de errores HTTP

| Código de estado | Comportamiento esperado en la app |
|-----------------|-----------------------------------|
| 200, 201, 204 | Éxito; procesar respuesta |
| 400 | Error de solicitud del cliente; mostrar mensaje de validación |
| 401 | No autenticado; redirigir al flujo de autenticación |
| 403 | Sin permiso; mostrar mensaje de acceso denegado |
| 404 | Recurso no encontrado; mostrar estado vacío o mensaje |
| 422 | Validación de negocio fallida; mostrar los errores específicos |
| 5xx | Error del servidor; mostrar mensaje genérico de error y opción de reintento |
| Sin conexión | Error de red; mostrar mensaje de sin conexión y opción de reintento |

### Cliente HTTP

La biblioteca de cliente HTTP concreta está pendiente de selección (DEC-MOV-004). Cualquier solución adoptada debe:
- Permitir configurar una URL base.
- Soportar la inyección de headers de autenticación.
- Exponer los errores de forma tipada (errores de red, errores HTTP).
- Ser intercambiable sin afectar a las capas superiores (a través de abstracciones).

---

## 10. Configuración por entorno

### Valores de configuración necesarios

La aplicación requiere, como mínimo, los siguientes valores configurables por entorno:

| Parámetro | Descripción | Sensibilidad |
|-----------|-------------|--------------|
| URL base de la API | Dirección del backend a consumir | Alta (no versionar la de producción) |
| Timeout de solicitudes HTTP | Tiempo máximo de espera en solicitudes | Baja |
| Nivel de logging | Verbosidad de los registros de diagnóstico | Baja |

> Esta lista es ilustrativa. Los parámetros concretos se definirán en la fase de diseño del entorno.

### Restricciones

- Ningún valor de la URL de producción ni ningún secreto debe hardcodearse en el código fuente.
- Los archivos de configuración local de desarrollo deben excluirse del repositorio mediante `.gitignore`.
- La estrategia técnica concreta en Flutter está pendiente de decisión (DEC-MOV-013).

---

## 11. Seguridad y protección de datos

### Principios de seguridad del cliente móvil

1. **Sin credenciales de base de datos:** La aplicación jamás debe contener ni gestionar credenciales de acceso directo a la base de datos. Toda comunicación pasa por el backend.
2. **Gestión segura de tokens:** Los tokens de autenticación deben almacenarse usando mecanismos seguros del sistema operativo (p. ej., Keychain en iOS, Keystore en Android), no en almacenamiento en texto plano. La implementación concreta depende de DEC-MOV-005 y DEC-MOV-010.
3. **HTTPS obligatorio:** Toda comunicación con el backend debe realizarse mediante HTTPS; no se aceptan conexiones no cifradas.
4. **Validación de respuestas:** Los datos recibidos del backend deben validarse antes de ser presentados al usuario.
5. **Sin datos sensibles en logs:** Los registros de diagnóstico no deben incluir credenciales, tokens, ni datos personales del usuario.
6. **Datos mínimos en el dispositivo:** Solo se almacenan localmente los datos estrictamente necesarios para la experiencia del usuario.

### Mecanismo de autenticación

El mecanismo de autenticación en el cliente está **pendiente de selección** (DEC-MOV-010), y debe estar alineado con la decisión de autenticación del backend (DEC-002 del repositorio `BusTrack_Back`).

**Principios que aplican independientemente del mecanismo:**
- Los tokens no se exponen en logs ni en parámetros de URL.
- Los tokens se invalidan y eliminan del almacenamiento local al cerrar sesión.
- El flujo de refresco de tokens (si aplica) debe ser transparente para el usuario.

### Plataformas y permisos

- La aplicación solo debe solicitar los permisos del sistema operativo estrictamente necesarios para las funcionalidades activas.
- No se solicitarán permisos de GPS continuo, cámara, micrófono u otros sin especificación funcional aprobada.

---

## 12. Estrategia de pruebas

### Tipos de prueba contemplados

| Tipo | Propósito | Alcance |
|------|-----------|---------|
| Pruebas unitarias | Verificar la lógica de la capa de aplicación y de datos de forma aislada | Capa de Aplicación, Capa de Datos |
| Pruebas de widgets | Verificar el comportamiento de componentes de la interfaz de forma aislada | Capa de Presentación |
| Pruebas de integración | Verificar flujos completos del usuario en la aplicación | Todas las capas |

### Principios generales

- Las pruebas unitarias no deben depender de la red ni del backend real.
- Las dependencias externas (repositorios, clientes HTTP) deben poder sustituirse por dobles de prueba (mocks, stubs).
- Las pruebas de widgets deben probar el comportamiento (interacción), no solo la apariencia.
- Las pruebas de integración pueden ejecutarse contra un backend de prueba o un servidor simulado.

### Herramientas

- **Pendiente de selección** (DEC-MOV-012). El ecosistema Flutter provee `flutter_test` e `integration_test` como herramientas estándar; bibliotecas de simulación como `mockito` o `mocktail` son candidatas habituales.

### Umbral de cobertura

- **Pendiente de definición** (DEC-MOV-011).

### Integración con CI/CD

- Las pruebas automatizadas deben ejecutarse como parte del pipeline de integración continua.
- Ningún artefacto distribuible debe generarse si las pruebas fallan.

---

## 13. Requisitos no funcionales

| ID | Requisito | Descripción | Estado |
|----|-----------|-------------|--------|
| RNF-MOV-01 | Rendimiento de la interfaz | La aplicación debe mantener una tasa de fotogramas fluida (60 o 120 fps según el dispositivo) en las pantallas principales | Principio arquitectónico |
| RNF-MOV-02 | Tiempo de respuesta percibido | Las operaciones asíncronas deben mostrar indicadores de carga en menos de 300 ms desde que se inician | Principio arquitectónico |
| RNF-MOV-03 | Compatibilidad de plataforma | La aplicación debe funcionar correctamente en Android e iOS (versiones mínimas por definir — DEC-MOV-015) | Pendiente DEC-MOV-015 |
| RNF-MOV-04 | Seguridad de datos en reposo | Los datos sensibles almacenados localmente deben estar cifrados o protegidos por el sistema operativo | Principio de seguridad |
| RNF-MOV-05 | Recuperación ante errores de red | La aplicación debe gestionar las pérdidas de conexión sin bloquearse ni perder el estado del usuario | Principio arquitectónico |
| RNF-MOV-06 | Accesibilidad | Los elementos interactivos deben tener etiquetas semánticas para lectores de pantalla | Buena práctica |
| RNF-MOV-07 | Mantenibilidad | La arquitectura debe permitir incorporar nuevas funcionalidades sin refactorizaciones masivas | Principio arquitectónico |
| RNF-MOV-08 | Testabilidad | Las capas de aplicación y datos deben poder probarse sin dependencia de la interfaz gráfica ni del backend real | Principio arquitectónico |
| RNF-MOV-09 | Tamaño de la aplicación | El tamaño del artefacto distribuible debe minimizarse eliminando dependencias innecesarias | Pendiente de evaluación |
| RNF-MOV-10 | Privacidad | La aplicación no debe recopilar datos del usuario más allá de lo estrictamente necesario para su funcionamiento | Principio de seguridad |

---

## 14. Decisiones pendientes

Ver `memoria.md` sección 4 para el listado completo de decisiones pendientes con sus identificadores.

Las decisiones que afectan directamente a esta especificación son:

- **DEC-MOV-001:** Versión exacta de Flutter y Dart.
- **DEC-MOV-002:** Biblioteca de gestión de estado.
- **DEC-MOV-003:** Biblioteca de navegación.
- **DEC-MOV-004:** Cliente HTTP concreto.
- **DEC-MOV-005:** Estrategia definitiva de almacenamiento local.
- **DEC-MOV-006:** Contratos funcionales definitivos de la API.
- **DEC-MOV-010:** Mecanismo de autenticación en el cliente.
- **DEC-MOV-013:** Estrategia de configuración por entorno en Flutter.
- **DEC-MOV-014:** Estructura definitiva de directorios del proyecto Flutter.
- **DEC-MOV-015:** Plataformas objetivo y versiones mínimas.

Ninguna de estas decisiones puede asumirse como resuelta sin aprobación explícita y registro en `memoria.md`.

---

## 15. Criterios de aceptación verificables de la arquitectura base

Los siguientes criterios deben poderse verificar durante y después de la fase de implementación de la arquitectura base. **No se afirma que estén cumplidos actualmente.**

| ID | Criterio | Cómo verificarlo |
|----|----------|-----------------| 
| AC-MOV-ARCH-01 | El proyecto Flutter está organizado en directorios que reflejan las capas (Presentación, Aplicación, Datos) o equivalente aprobado | Inspección de la estructura de directorios |
| AC-MOV-ARCH-02 | Los widgets no contienen llamadas directas a repositorios o fuentes de datos HTTP | Revisión de código |
| AC-MOV-ARCH-03 | Los repositorios no contienen lógica de presentación ni de estado de la interfaz | Revisión de código |
| AC-MOV-ARCH-04 | La comunicación con el backend se realiza exclusivamente mediante HTTPS | Inspección de la configuración del cliente HTTP |
| AC-MOV-ARCH-05 | Las respuestas de la API se parsean a modelos de datos tipados; no se usan mapas dinámicos sin tipo en la lógica de aplicación | Revisión de código |
| AC-MOV-ARCH-06 | Los estados de carga, éxito, error y vacío están gestionados de forma consistente | Revisión de código y pruebas de widgets |
| AC-MOV-ARCH-07 | Ningún archivo versionado contiene credenciales, tokens ni URLs de producción hardcodeadas | Revisión de `.gitignore` y del código fuente |
| AC-MOV-ARCH-08 | Los tokens de autenticación se almacenan usando mecanismos seguros del sistema operativo (no en SharedPreferences no cifradas ni en texto plano) | Revisión de código |
| AC-MOV-ARCH-09 | Las rutas de navegación están centralizadas y no dispersas en los widgets | Revisión de código |
| AC-MOV-ARCH-10 | Las pruebas unitarias de la capa de aplicación y datos pasan sin conexión de red ni backend real | Ejecución del conjunto de pruebas |
| AC-MOV-ARCH-11 | La aplicación compila y se ejecuta en el entorno de desarrollo para Android e iOS | Ejecución de `flutter run` o equivalente |
| AC-MOV-ARCH-12 | La configuración de entorno (URL base de la API) es diferente entre desarrollo y producción y se inyecta sin hardcodear | Inspección de la configuración del entorno |
| AC-MOV-ARCH-13 | Los errores de red se capturan y presentan al usuario sin exponer detalles técnicos internos | Prueba de integración simulando error de red |
| AC-MOV-ARCH-14 | El gestor de estado elegido permite probar la lógica de aplicación sin la interfaz gráfica | Pruebas unitarias del gestor de estado |

---

*Esta especificación debe revisarse y aprobarse antes de iniciar la implementación. Cualquier cambio debe seguir el proceso de control de cambios descrito en `constitution.md`.*
