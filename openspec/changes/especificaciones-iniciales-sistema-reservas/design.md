# Design

## Context

El cambio introduce tres capacidades nuevas: spaces, users y permissions. No existen especificaciones previas registradas para estas capacidades, por lo que sus requisitos se definen en los archivos spec.md de este cambio.

La solución futura deberá mantener coherencia con PLAN_INGENIERIA.md y con la propuesta aprobada. La arquitectura prevista utiliza una API REST con FastAPI, persistencia mediante SQLAlchemy y SQLite, migraciones con Alembic, autenticación mediante JWT y autorización basada en roles.

Este documento establece las decisiones de diseño para orientar una implementación posterior. No incluye código funcional ni modifica la arquitectura documentada en el plan de ingeniería.

## Goals / Non-Goals

**Goals:**

- Definir límites claros entre la gestión de espacios, la administración de usuarios y la autorización.
- Mantener las decisiones técnicas coherentes con el plan de ingeniería.
- Establecer criterios de seguridad para las credenciales y el acceso a operaciones protegidas.
- Facilitar que los requisitos de las especificaciones puedan implementarse y verificarse posteriormente.

**Non-Goals:**

- Implementar endpoints, modelos, migraciones o pruebas automatizadas.
- Modificar PLAN_INGENIERIA.md.
- Incorporar nuevos frameworks, servicios externos o mecanismos de autenticación.
- Definir funcionalidades adicionales que no estén respaldadas por la propuesta o las especificaciones.

## Decisions

### 1. Separación por capacidades

Las responsabilidades se organizarán en tres áreas funcionales:

- **spaces:** administración y consulta de espacios académicos, incluidos sus datos y estado.
- **users:** registro y administración de cuentas, validación de datos y control del estado de las cuentas.
- **permissions:** definición de roles institucionales y aplicación de las reglas de autorización.

Esta separación permite mantener responsabilidades identificables y facilita la validación independiente de cada capacidad.

**Alternativa considerada:** concentrar las tres responsabilidades en un único módulo. Se descarta porque dificultaría mantener límites claros entre la administración de datos y el control de acceso.

### 2. Arquitectura de la API y persistencia

La implementación futura seguirá la arquitectura definida en PLAN_INGENIERIA.md: API REST con FastAPI, SQLAlchemy como herramienta de persistencia, SQLite como base de datos y Alembic para gestionar migraciones.

Las decisiones de estructura interna deberán respetar los límites funcionales establecidos en las especificaciones, sin introducir dependencias o patrones arquitectónicos adicionales sin justificación.

**Alternativa considerada:** cambiar el framework o la base de datos. Se descarta porque no es necesario para este cambio y se apartaría del plan de ingeniería existente.

### 3. Identidad y protección de usuarios

Las cuentas deberán mantener un identificador estable y una dirección de correo electrónico única. Las respuestas destinadas a consulta no deberán exponer contraseñas ni sus representaciones protegidas.

La implementación deberá utilizar almacenamiento seguro de contraseñas y evitar que las credenciales se registren o devuelvan en texto plano.

**Alternativa considerada:** almacenar o devolver las credenciales originales. Se descarta por los riesgos de seguridad y por los requisitos establecidos en users/spec.md.

### 4. Autenticación y autorización

La solución futura utilizará JWT para identificar las solicitudes autenticadas y un control de acceso basado en roles para decidir si una operación está permitida.

Los roles institucionales serán Solicitante, Gestor de espacios y Administrador. Las operaciones protegidas deberán denegarse cuando no exista una identidad válida o no se haya establecido el permiso correspondiente.

La autorización deberá aplicarse de manera consistente en las operaciones protegidas, sin depender únicamente de restricciones de la interfaz cliente.

**Alternativa considerada:** permitir operaciones según el rol declarado por el cliente sin validación del servidor. Se descarta porque no proporciona una frontera de seguridad confiable.

La asignación concreta de permisos deberá mantenerse alineada con permissions/spec.md y con las responsabilidades definidas en PLAN_INGENIERIA.md. No se introducirán permisos adicionales sin revisar las especificaciones correspondientes.

### 5. Validación de datos y estados

Las operaciones de creación y actualización deberán validar los datos requeridos y las restricciones de unicidad descritas en las especificaciones.

La desactivación de espacios y usuarios deberá conservar sus registros, en lugar de eliminarlos físicamente. Las consultas deberán reflejar correctamente el estado de cada registro.

**Alternativa considerada:** permitir registros duplicados o eliminar físicamente los registros al desactivarlos. Se descarta porque contradice los requisitos funcionales establecidos.

### 6. Desarrollo guiado por especificaciones

Las especificaciones serán el contrato de comportamiento para la implementación posterior. Cada requisito deberá contar con escenarios verificables y los cambios de código futuros deberán poder relacionarse con esos requisitos.

Antes de implementar, deberán revisarse las ambigüedades funcionales que afecten los permisos, las validaciones o los resultados observables del sistema.

**Alternativa considerada:** implementar directamente a partir de decisiones implícitas en el código. Se descarta porque reduce la trazabilidad y dificulta verificar el cumplimiento de los requisitos.

## Risks / Trade-offs

- **Ambigüedad en los permisos por operación** → Revisar permissions/spec.md y contrastarlo con PLAN_INGENIERIA.md antes de implementar operaciones protegidas.
- **Exposición accidental de credenciales** → Excluir contraseñas y sus representaciones protegidas de las respuestas y revisar los registros de aplicación.
- **Inconsistencia entre especificaciones y arquitectura** → Revisar los requisitos y el diseño antes de descomponer el trabajo en tareas de implementación.
- **Restricciones de SQLite bajo concurrencia** → Considerar sus límites operativos al implementar las operaciones que requieran consistencia; no asumir que la elección de base de datos elimina los conflictos concurrentes.
- **Desviación del alcance original** → Mantener el cambio limitado a la documentación de OpenSpec y conservar PLAN_INGENIERIA.md sin modificaciones.

## Migration Plan

Este cambio solo incorpora documentación OpenSpec, por lo que no requiere migraciones de base de datos, despliegues ni cambios en los datos existentes.

La secuencia documental será:

1. Revisar proposal.md y las tres especificaciones de capacidades.
2. Completar y revisar design.md.
3. Crear tasks.md con actividades verificables derivadas de los requisitos y del diseño.
4. Validar el cambio con OpenSpec y corregir los errores o advertencias pertinentes.
5. Revisar los artefactos antes de archivarlos.

No se implementará código funcional como parte de este cambio. La implementación quedará para un cambio posterior.