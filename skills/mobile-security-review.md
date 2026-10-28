# mobile-security-review.md — Skill: Revisión de Seguridad del Cliente Móvil

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`../constitution.md`](../constitution.md)

> **Aviso:** Este archivo describe un procedimiento de revisión reutilizable. No es un script ejecutable ni depende de ninguna plataforma específica. Cualquier agente o colaborador puede seguir este procedimiento manualmente.

---

## 1. Objetivo

Verificar que la aplicación móvil de BusTrack cumple con los principios de seguridad y privacidad definidos en `constitution.md` (sección 7) y `spec.md` (sección 11), y que no contiene ningún contenido que represente un riesgo de seguridad para el sistema o los usuarios.

---

## 2. Cuándo utilizarlo

- Al finalizar la generación de documentación de arquitectura.
- Antes de iniciar cualquier fase que involucre comunicación HTTP o almacenamiento local.
- Cuando se propone un mecanismo de autenticación o almacenamiento de tokens.
- Antes de cualquier commit de código con funcionalidades de red o autenticación.
- En cualquier revisión de pull request que modifique la capa de datos o de aplicación.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `constitution.md` sección 7 | Principios de seguridad de la app móvil | Sí |
| `spec.md` sección 11 | Principios de seguridad del cliente | Sí |
| `memoria.md` | Decisiones pendientes de seguridad | Sí |
| Artefacto a revisar | Documento, diseño o código bajo evaluación | Sí |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar la ausencia de acceso directo a la base de datos

1. Buscar en el código y documentos cualquier referencia a SDKs de bases de datos directas (MongoDB, Cosmos DB, SQLite para datos del servidor, etc.).
2. Verificar que la capa de datos solo contiene llamadas HTTP al backend, no a la base de datos.
3. Verificar que no hay cadenas de conexión a bases de datos en ningún archivo.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-01 y SEC-MOV-02 cumplidos.

### Paso 2: Verificar la seguridad de la comunicación

1. Verificar que el cliente HTTP está configurado para usar HTTPS exclusivamente.
2. Verificar que no hay URLs con protocolo `http://` (sin cifrado) en la configuración.
3. Verificar que no se ignoran certificados SSL (no hay bypass de validación TLS).
4. Verificar que los headers de autenticación se incluyen correctamente en las solicitudes.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-03 cumplido.

### Paso 3: Verificar la gestión de tokens de autenticación

1. Verificar que los tokens no se almacenan en `SharedPreferences` sin cifrado ni en texto plano en ficheros.
2. Verificar que se usan mecanismos seguros del sistema operativo (Keychain en iOS, Keystore/EncryptedSharedPreferences en Android, o equivalente con la biblioteca aprobada).
3. Verificar que los tokens se eliminan del almacenamiento al cerrar sesión.
4. Verificar que los tokens no se incluyen en logs ni en parámetros de URL.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-04 cumplido.

### Paso 4: Verificar la ausencia de secretos en el repositorio

1. Revisar todos los archivos del repositorio en busca de:
   - Claves de API.
   - Tokens de autenticación.
   - Contraseñas.
   - URLs de producción hardcodeadas.
   - Credenciales de base de datos.
2. Verificar que el `.gitignore` excluye archivos de configuración local que pudieran contener secretos.
3. Verificar que `pubspec.yaml` no contiene dependencias con tokens incluidos.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-05 cumplido.

### Paso 5: Verificar los registros de diagnóstico

1. Verificar que las sentencias de log no imprimen tokens de autenticación.
2. Verificar que las sentencias de log no imprimen datos personales del usuario (nombre, correo, teléfono, etc.).
3. Verificar que los errores registrados no incluyen detalles internos del sistema que podrían exponer la arquitectura.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-06 cumplido.

### Paso 6: Verificar los permisos del sistema operativo

1. Verificar en `AndroidManifest.xml` (Android) y `Info.plist` (iOS) que solo se declaran permisos justificados.
2. Verificar que no se solicitan permisos de GPS, cámara, micrófono, contactos u otros sin especificación funcional aprobada.
3. Verificar que los permisos declarados tienen una justificación documentada.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-07 cumplido.

### Paso 7: Verificar el principio de datos mínimos en el dispositivo

1. Verificar que los datos almacenados localmente son los estrictamente necesarios para la experiencia del usuario.
2. Verificar que los datos sensibles almacenados localmente tienen justificación documentada.
3. Verificar que los datos locales se eliminan correctamente al cerrar sesión.

**Resultado esperado:** Sin hallazgos. Criterio SEC-MOV-08 cumplido.

### Paso 8: Verificar la validación de respuestas del backend

1. Verificar que los datos recibidos del backend se parsean a modelos tipados antes de usarse.
2. Verificar que no se usan datos del backend sin validación previa (p. ej., mapas dinámicos sin tipo directamente en la interfaz).
3. Verificar que los errores del backend se capturan y se presentan al usuario sin exponer detalles técnicos.

**Resultado esperado:** Sin hallazgos. Criterios SEC-MOV-09 y SEC-MOV-10 cumplidos.

---

## 5. Criterios de aceptación

La revisión resulta en estado **CONFORME** cuando todos los pasos anteriores resultan sin hallazgos negativos.

La revisión resulta en estado **CONFORME CON OBSERVACIONES** cuando hay hallazgos menores que no representan un riesgo de seguridad inmediato pero deben corregirse.

La revisión resulta en estado **NO CONFORME** cuando:
- Se detecta acceso directo a la base de datos.
- Se detectan credenciales o tokens en el repositorio.
- La comunicación no usa HTTPS.
- Los tokens se almacenan en texto plano.

---

## 6. Tabla de verificación rápida

| ID | Criterio | Verificado | Hallazgo |
|----|----------|-----------|----------|
| SEC-MOV-01 | Sin acceso directo a BD | ☐ | |
| SEC-MOV-02 | Sin credenciales de BD | ☐ | |
| SEC-MOV-03 | HTTPS obligatorio | ☐ | |
| SEC-MOV-04 | Tokens almacenados de forma segura | ☐ | |
| SEC-MOV-05 | Sin secretos en repositorio | ☐ | |
| SEC-MOV-06 | Logs sin datos sensibles | ☐ | |
| SEC-MOV-07 | Permisos mínimos | ☐ | |
| SEC-MOV-08 | Datos mínimos en dispositivo | ☐ | |
| SEC-MOV-09 | Validación de respuestas | ☐ | |
| SEC-MOV-10 | Errores sin detalles técnicos | ☐ | |

---

## 7. Formato esperado del resultado

```markdown
# Resultado de Revisión de Seguridad — App Móvil BusTrack

**Fecha:** YYYY-MM-DD
**Artefacto revisado:** [descripción]
**Revisado por:** [agente o colaborador]

## Resumen

Estado general: CONFORME / CONFORME CON OBSERVACIONES / NO CONFORME

## Hallazgos por paso

[Resultado de cada paso con evidencia]

## Riesgos identificados

| ID | Descripción | Nivel | Mitigación propuesta |
|----|-------------|-------|---------------------|

## Próximos pasos

[Acciones requeridas antes de considerar la revisión superada]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
