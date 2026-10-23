# Spec Delta

## Purpose

Define el comportamiento necesario para registrar, consultar y administrar los espacios académicos disponibles para las reservas institucionales.

## ADDED Requirements

### Requirement: Registro de espacios académicos
The system SHALL allow authorized administrators to register an academic space with a name, type, capacity, and location.

#### Scenario: Registro exitoso de un espacio
- **WHEN** an authorized administrator submits valid data for a space with a name that is not already in use
- **THEN** the system SHALL create the space and make its information available for consultation

#### Scenario: Nombre de espacio duplicado
- **WHEN** an authorized administrator attempts to register a space using a name that already exists
- **THEN** the system SHALL reject the operation and report that the name must be unique

### Requirement: Consulta de espacios académicos
The system SHALL allow authorized users to consult the information and active status of registered academic spaces.

#### Scenario: Consulta de un espacio existente
- **WHEN** an authorized user requests a registered space
- **THEN** the system SHALL return the space information, including its name, type, capacity, location, and status

#### Scenario: Consulta de un espacio inexistente
- **WHEN** an authorized user requests a space identifier that does not exist
- **THEN** the system SHALL report that the requested space was not found

### Requirement: Modificación de espacios académicos
The system SHALL allow authorized administrators to update the information of a registered space while preserving its identity.

#### Scenario: Actualización de información
- **WHEN** an authorized administrator submits valid updated information for an existing space
- **THEN** the system SHALL save the changes and return the updated information

#### Scenario: Actualización con nombre duplicado
- **WHEN** an authorized administrator attempts to rename a space using a name already assigned to another space
- **THEN** the system SHALL reject the change and report the uniqueness conflict

### Requirement: Activación y desactivación de espacios
The system SHALL allow authorized administrators to activate or deactivate a registered space without physically deleting it.

#### Scenario: Desactivación de un espacio
- **WHEN** an authorized administrator deactivates an active space
- **THEN** the system SHALL preserve the space record and change its status to inactive

#### Scenario: Reactivación de un espacio
- **WHEN** an authorized administrator activates an inactive space
- **THEN** the system SHALL change its status to active
