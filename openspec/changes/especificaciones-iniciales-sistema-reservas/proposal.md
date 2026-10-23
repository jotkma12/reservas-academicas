# Proposal

## Why

La institución necesita centralizar la gestión de espacios académicos y usuarios, y aplicar reglas de autorización consistentes para reducir errores administrativos y accesos no permitidos. Definir estas capacidades antes de implementar la API permitirá establecer comportamientos verificables y mantener coherencia con el plan de ingeniería.

## What Changes

- Definir los requisitos para crear, consultar, modificar, activar y desactivar espacios académicos.
- Definir los requisitos para registrar y administrar usuarios, incluyendo unicidad del correo electrónico y control del estado de las cuentas.
- Definir los requisitos para los roles fijos del sistema y la autorización de operaciones según los permisos asignados.
- Establecer escenarios de aceptación verificables para cada requisito.
- Documentar las decisiones funcionales necesarias sin implementar código en este cambio.

## Capabilities

### New Capabilities

- `spaces`: gestión y consulta de espacios académicos, incluidos sus datos y estado.
- `users`: registro y administración de cuentas de usuario, con validaciones de identidad y estado.
- `permissions`: definición de roles fijos y control de acceso a las operaciones del sistema.

### Modified Capabilities

Ninguna. No existen especificaciones previas registradas para modificar.

## Impact

- Documentación OpenSpec: `proposal.md`, especificaciones de las tres capacidades y artefactos de planificación necesarios.
- API REST futura desarrollada con FastAPI y persistencia mediante SQLAlchemy y SQLite, según `PLAN_INGENIERIA.md`.
- Autenticación y autorización: las especificaciones de usuarios y permisos deberán ser coherentes con el uso previsto de JWT y control de acceso basado en roles.
- No se implementarán endpoints, modelos, migraciones ni pruebas de código en este cambio.
- `PLAN_INGENIERIA.md` permanecerá sin modificaciones.
