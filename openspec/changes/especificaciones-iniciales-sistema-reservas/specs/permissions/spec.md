# Spec Delta

## Purpose

Define los roles institucionales y las reglas de autorización que determinan qué operaciones puede realizar cada usuario en el sistema de reservas académicas.

## ADDED Requirements

### Requirement: Roles institucionales definidos
The system SHALL support the fixed roles Solicitante, Gestor de espacios, and Administrador.

#### Scenario: Consulta de los roles disponibles
- **WHEN** an authorized administrator requests the available system roles
- **THEN** the system SHALL return the defined roles Solicitante, Gestor de espacios, and Administrador

#### Scenario: Asignación de un rol no reconocido
- **WHEN** an administrator attempts to assign a role that is not defined by the system
- **THEN** the system SHALL reject the assignment and report that the role is invalid

### Requirement: Asignación y modificación de roles
The system SHALL allow only authorized administrators to assign or change a user's role.

#### Scenario: Asignación autorizada de un rol
- **WHEN** an authorized administrator assigns a defined role to an existing user
- **THEN** the system SHALL associate the selected role with that user

#### Scenario: Intento no autorizado de cambiar un rol
- **WHEN** a user without administrative permission attempts to assign or change a role
- **THEN** the system SHALL reject the operation without changing the user's role

### Requirement: Autorización de operaciones administrativas
The system SHALL restrict the creation, modification, activation, and deactivation of academic spaces and user accounts to users with the Administrador role.

#### Scenario: Administrador ejecuta una operación administrativa
- **WHEN** a user with the Administrador role requests an operation permitted for administrators
- **THEN** the system SHALL authorize the operation if its input and other applicable business rules are valid

#### Scenario: Solicitante intenta una operación administrativa
- **WHEN** a user with the Solicitante role attempts to create or modify an academic space or administer another user's account
- **THEN** the system SHALL deny the operation

#### Scenario: Gestor de espacios intenta una operación administrativa restringida
- **WHEN** a user with the Gestor de espacios role attempts to administer user accounts or change role assignments
- **THEN** the system SHALL deny the operation

### Requirement: Autorización de las operaciones del gestor de espacios
The system SHALL allow the Gestor de espacios role to perform the reservation-management operations assigned to that role by the system's access rules.

#### Scenario: Gestor realiza una operación permitida
- **WHEN** a user with the Gestor de espacios role requests a reservation-management operation permitted for that role
- **THEN** the system SHALL authorize the operation if all applicable business rules are satisfied

#### Scenario: Gestor intenta una operación ajena a su rol
- **WHEN** a user with the Gestor de espacios role requests an operation not permitted for that role
- **THEN** the system SHALL deny the operation

### Requirement: Acceso limitado del solicitante
The system SHALL restrict the Solicitante role to permitted consultation and personal reservation operations.

#### Scenario: Solicitante consulta información permitida
- **WHEN** a user with the Solicitante role requests academic-space information or reservation availability that is permitted for consultation
- **THEN** the system SHALL provide the requested information subject to the applicable access rules

#### Scenario: Solicitante intenta administrar espacios o usuarios
- **WHEN** a user with the Solicitante role attempts an operation reserved for administrators or gestores de espacios
- **THEN** the system SHALL deny the operation

### Requirement: Denegación predeterminada
The system SHALL deny protected operations when the requesting user's identity or permissions cannot be established.

#### Scenario: Solicitud sin identidad autenticada
- **WHEN** a request attempts to access a protected operation without valid authentication
- **THEN** the system SHALL deny access

#### Scenario: Permiso no definido
- **WHEN** an authenticated user requests an operation for which the user's role has no permission
- **THEN** the system SHALL deny the operation without performing the requested action
