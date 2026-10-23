# Spec Delta

## Purpose

Define el comportamiento para registrar y administrar las cuentas de usuario del sistema de reservas académicas, manteniendo la integridad de sus datos y la protección de sus credenciales.

## ADDED Requirements

### Requirement: Registro de usuarios
The system SHALL allow authorized administrators to register users with a name, unique email address, and credentials.

#### Scenario: Registro exitoso
- **WHEN** an authorized administrator submits valid user data with an email address that is not already registered
- **THEN** the system SHALL create the user account and make the account information available for authorized consultation

#### Scenario: Registro con correo duplicado
- **WHEN** an authorized administrator attempts to register a user with an email address already assigned to another account
- **THEN** the system SHALL reject the operation and report the email uniqueness conflict

#### Scenario: Registro con datos obligatorios inválidos
- **WHEN** an authorized administrator submits a registration request with missing or invalid required data
- **THEN** the system SHALL reject the request and identify the validation errors

### Requirement: Consulta de usuarios
The system SHALL allow authorized administrators to consult registered user information without exposing authentication secrets.

#### Scenario: Consulta de un usuario existente
- **WHEN** an authorized administrator requests an existing user account
- **THEN** the system SHALL return the user's identifier, name, email address, role, and account status without returning the password or password hash

#### Scenario: Consulta de un usuario inexistente
- **WHEN** an authorized administrator requests a user identifier that does not exist
- **THEN** the system SHALL report that the user was not found

### Requirement: Actualización de usuarios
The system SHALL allow authorized administrators to update permitted user information while preserving the user's identity.

#### Scenario: Actualización de datos
- **WHEN** an authorized administrator submits valid updated information for an existing user
- **THEN** the system SHALL save the changes and return the updated information without exposing authentication secrets

#### Scenario: Actualización con correo duplicado
- **WHEN** an authorized administrator attempts to assign an email address already used by another account
- **THEN** the system SHALL reject the change and report the email uniqueness conflict

### Requirement: Activación y desactivación de usuarios
The system SHALL allow authorized administrators to activate or deactivate user accounts without physically deleting their records.

#### Scenario: Desactivación de una cuenta
- **WHEN** an authorized administrator deactivates an active user account
- **THEN** the system SHALL preserve the user record and change the account status to inactive

#### Scenario: Reactivación de una cuenta
- **WHEN** an authorized administrator activates an inactive user account
- **THEN** the system SHALL change the account status to active

### Requirement: Protección de credenciales
The system SHALL ensure that user passwords are not stored or exposed in plaintext.

#### Scenario: Almacenamiento de credenciales
- **WHEN** a user account is created or its password is changed
- **THEN** the system SHALL store a protected password representation rather than the original plaintext password

#### Scenario: Consulta o exposición de credenciales
- **WHEN** user information is returned through an administrative operation
- **THEN** the system SHALL NOT include the plaintext password or its stored protected representation in the response
