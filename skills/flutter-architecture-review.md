# flutter-architecture-review.md — Skill: Revisión de Arquitectura Flutter

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`../constitution.md`](../constitution.md)

> **Aviso:** Este archivo describe un procedimiento de revisión reutilizable. No es un script ejecutable ni depende de ninguna plataforma específica. Cualquier agente o colaborador puede seguir este procedimiento manualmente.

---

## 1. Objetivo

Verificar que la arquitectura Flutter de la aplicación móvil de BusTrack cumple con los principios de separación de responsabilidades, seguridad, comunicación con el backend y requisitos no funcionales definidos en `spec.md` y `constitution.md`.

---

## 2. Cuándo utilizarlo

- Al finalizar la generación o actualización de documentos de arquitectura.
- Antes de iniciar la Fase 2 (Aprobación de arquitectura) del plan.
- Cuando se propone una nueva capa, componente o patrón de diseño.
- Cuando se detecta una posible desviación de la arquitectura propuesta.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `constitution.md` | Principios normativos de la app móvil | Sí |
| `spec.md` | Especificación de arquitectura base Flutter | Sí |
| `memoria.md` | Decisiones confirmadas y pendientes | Sí |
| Propuesta o código a revisar | El artefacto bajo evaluación | Sí |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar la separación de capas

1. Confirmar que existe una separación clara entre Presentación, Aplicación y Datos.
2. Verificar que los widgets (Presentación) no contienen:
   - Llamadas directas a repositorios o fuentes de datos.
   - Llamadas directas al cliente HTTP.
   - Lógica de negocio o de dominio.
3. Verificar que los gestores de estado (Aplicación) no contienen:
   - Lógica de renderizado de la interfaz.
   - Llamadas directas al cliente HTTP (solo a repositorios).
4. Verificar que los repositorios (Datos) no contienen:
   - Lógica de presentación o de estado de la interfaz.
   - Dependencias directas de widgets.

**Resultado esperado:** Cada capa tiene responsabilidades claramente delimitadas según `spec.md` sección 5.

### Paso 2: Verificar la comunicación con el backend

1. Confirmar que toda comunicación con el backend pasa por el cliente HTTP de la capa de datos.
2. Confirmar que el protocolo es HTTPS (no HTTP).
3. Confirmar que el formato de intercambio es JSON.
4. Verificar que las respuestas JSON se parsean a modelos de datos tipados.
5. Verificar que todos los códigos de error HTTP documentados en `spec.md` sección 9 tienen manejo explícito.

**Resultado esperado:** La comunicación con el backend cumple los principios de `spec.md` sección 9.

### Paso 3: Verificar la gestión de errores y estados de carga

1. Confirmar que existen los cuatro estados: Cargando, Éxito, Error, Vacío.
2. Confirmar que los mensajes de error al usuario no exponen detalles técnicos internos.
3. Confirmar que siempre hay una acción de recuperación disponible (reintentar, volver).
4. Verificar que los errores de red se distinguen de los errores de negocio del backend.

**Resultado esperado:** El manejo de errores es consistente con `spec.md` sección 6.2.

### Paso 4: Verificar la configuración por entorno

1. Confirmar que la URL base de la API es configurable por entorno.
2. Confirmar que no hay URLs de producción hardcodeadas en el código.
3. Confirmar que los archivos de configuración local están en `.gitignore`.
4. Verificar que el mecanismo de configuración por entorno es coherente con DEC-MOV-013.

**Resultado esperado:** La configuración cumple los principios de `spec.md` sección 10.

### Paso 5: Verificar la navegación

1. Confirmar que las rutas de la aplicación están centralizadas en un único lugar.
2. Confirmar que la navegación no está acoplada a repositorios ni fuentes de datos.
3. Verificar que la biblioteca de navegación es coherente con DEC-MOV-003.

**Resultado esperado:** La navegación sigue los principios de `spec.md` sección 7.

### Paso 6: Verificar la gestión de estado

1. Confirmar que el estado de la aplicación está separado de los widgets.
2. Confirmar que el gestor de estado es testeable sin la interfaz gráfica.
3. Verificar que la biblioteca de gestión de estado es coherente con DEC-MOV-002.

**Resultado esperado:** La gestión de estado sigue los principios de `spec.md` sección 8.

### Paso 7: Verificar la ausencia de contenido prohibido

- [ ] No hay credenciales de base de datos en ningún archivo.
- [ ] No hay URLs de producción hardcodeadas.
- [ ] No hay llamadas directas a la base de datos desde la app.
- [ ] No hay funcionalidades fuera del alcance (GPS continuo, autenticación sin especificar, etc.).

---

## 5. Criterios de aceptación

La revisión resulta en estado **SIN OBSERVACIONES** cuando:

- Todos los pasos anteriores se verifican sin hallazgos negativos.
- Los criterios de aceptación AC-MOV-ARCH-01 al AC-MOV-ARCH-14 pueden considerarse cumplibles con la arquitectura propuesta.
- No se detectan funcionalidades fuera del alcance actual.

---

## 6. Formato esperado del resultado

```markdown
# Resultado de Revisión de Arquitectura Flutter

**Fecha:** YYYY-MM-DD
**Documentos revisados:** [lista]
**Revisado por:** [agente o colaborador]

## Resumen

Estado general: SIN OBSERVACIONES / CON OBSERVACIONES / CON ERRORES CRÍTICOS

## Hallazgos por paso

### Paso 1: Separación de capas
[resultado]

### Paso 2: Comunicación con el backend
[resultado]

### Paso 3: Gestión de errores y estados de carga
[resultado]

### Paso 4: Configuración por entorno
[resultado]

### Paso 5: Navegación
[resultado]

### Paso 6: Gestión de estado
[resultado]

### Paso 7: Ausencia de contenido prohibido
[resultado]

## Observaciones y recomendaciones

[Lista de observaciones con referencia al documento y sección afectados]

## Próximos pasos recomendados

[Acciones antes de considerar la revisión superada]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
