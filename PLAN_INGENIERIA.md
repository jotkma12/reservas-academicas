# PLAN DE INGENIERÍA DE SOFTWARE

## Sistema de Gestión de Reservas Académicas

**Versión:** 1.0  
**Metodología:** Spec-Driven Development (SDD)  
**Herramienta de especificación:** OpenSpec

## 1. Análisis del problema

### 1.1 Problemática

La institución universitaria gestiona las reservas de espacios académicos mediante correos electrónicos y hojas de cálculo. Este procedimiento puede generar solicitudes duplicadas, conflictos de horarios, dificultades para consultar la disponibilidad y falta de trazabilidad en las aprobaciones.

### 1.2 Necesidades de la institución

- Centralizar las solicitudes de reserva.
- Administrar laboratorios, auditorios y salas de cómputo.
- Consultar la disponibilidad de los espacios.
- Evitar reservas simultáneas para un mismo espacio.
- Gestionar solicitudes pendientes, aprobadas, rechazadas y canceladas.
- Mantener un historial de las reservas.
- Controlar los permisos según el rol del usuario.
- Limitar las reservas a cuatro horas consecutivas como regla de negocio.

### 1.3 Actores involucrados

- **Solicitante:** consulta espacios y crea o cancela sus solicitudes según las reglas establecidas.
- **Administrador:** administra espacios, usuarios y parámetros del sistema.
- **Responsable de aprobación:** aprueba o rechaza solicitudes.
- **Sistema:** valida disponibilidad, horarios, permisos y restricciones.

Los permisos definitivos se detallarán en las especificaciones.

### 1.4 Alcance

La primera versión incluirá la administración de espacios y usuarios, autenticación, roles y permisos, solicitudes de reserva, validación de disponibilidad, prevención de conflictos, aprobación o rechazo, cancelación e historial.

No se incluirán inicialmente aplicaciones móviles nativas, integración con calendarios externos ni notificaciones por SMS.

## 2. Propuesta de solución

Se propone una aplicación web centralizada que permita gestionar las reservas desde una interfaz única y almacenar la información en una base de datos relacional.

### 2.1 Funcionalidades prioritarias

1. Autenticación y administración de usuarios.
2. Gestión de espacios académicos.
3. Consulta de disponibilidad.
4. Creación de solicitudes de reserva.
5. Validación de conflictos y duración.
6. Aprobación y rechazo de solicitudes.
7. Cancelación e historial.
8. Pruebas y documentación.

### 2.2 Organización modular

- Usuarios y autenticación.
- Espacios académicos.
- Reservas y disponibilidad.
- Aprobaciones y estados.
- Historial y auditoría.
- Pruebas y documentación.

### 2.3 Desarrollo progresivo

Se implementará una funcionalidad a la vez. Antes de programar cada funcionalidad se definirán y revisarán sus especificaciones en OpenSpec. Después se implementará, se probará y se registrará el cambio mediante Git.

## 3. Decisiones de arquitectura y tecnología

### 3.1 Arquitectura seleccionada

Se utilizará una arquitectura monolítica modular. Los módulos estarán organizados dentro de una única aplicación para reducir la complejidad inicial y facilitar las pruebas y el mantenimiento.

### 3.2 Stack tecnológico

- Lenguaje: Python.
- Framework web: Django.
- Base de datos: SQLite para el prototipo académico.
- Pruebas: pytest y pytest-django.
- Control de versiones: Git y GitHub.
- Gestión de especificaciones: OpenSpec.
- Asistencia de programación: agente de IA integrado en el entorno de desarrollo.

### 3.3 Persistencia de datos

Se utilizará una base de datos relacional. Las entidades principales serán Usuario, Espacio, Reserva y, si se requiere, Registro de auditoría.

Se definirán claves primarias, relaciones, restricciones y validaciones para mantener la integridad de los datos. SQLite será suficiente para el prototipo; para un despliegue concurrente en producción se evaluará PostgreSQL.

### 3.4 Comparación de decisiones técnicas

**Decisión 1: arquitectura**

Seleccionada: monolito modular.  
Alternativa descartada inicialmente: microservicios, porque añaden complejidad de despliegue y comunicación que no es necesaria para el alcance académico.

**Decisión 2: framework**

Seleccionado: Django.  
Alternativa descartada: desarrollar todo con Python sin framework, porque requeriría implementar manualmente más componentes de autenticación, administración y persistencia.

**Decisión 3: base de datos**

Seleccionada: SQLite para el prototipo.  
Alternativa evaluada: PostgreSQL. Se reserva para una etapa de despliegue con mayor concurrencia, ya que ofrece mejores capacidades para una aplicación multiusuario en producción.

**Decisión 4: metodología de desarrollo**

Seleccionada: SDD con OpenSpec.  
Alternativa descartada: programar únicamente mediante instrucciones directas a una IA, porque dificultaría mantener requisitos verificables y gestionar cambios de manera trazable.

## 4. Estrategia de desarrollo

### 4.1 Metodología

Se aplicará un proceso iterativo de Spec-Driven Development. Cada cambio funcional comenzará con requisitos y escenarios de aceptación, continuará con implementación y pruebas, y finalizará con revisión y registro en Git.

### 4.2 Etapas

1. Planificación y registro del plan de ingeniería.
2. Inicialización de OpenSpec.
3. Definición y revisión de las especificaciones.
4. Implementación de usuarios y espacios.
5. Implementación de solicitudes y disponibilidad.
6. Implementación de aprobaciones, cancelaciones e historial.
7. Incorporación de la regla de cuatro horas mediante OpenSpec.
8. Ejecución de pruebas, documentación y cierre.

### 4.3 Dependencias

La gestión de reservas depende de los usuarios y espacios. La aprobación depende de la existencia de una solicitud. El historial depende de los cambios de estado de las reservas. Las pruebas de aceptación dependen de que los requisitos estén definidos.

### 4.4 Criterios de finalización

Cada etapa se considerará terminada cuando la funcionalidad cumpla sus escenarios de aceptación, las pruebas correspondientes pasen, no existan errores conocidos que bloqueen su uso y los cambios estén registrados en Git.

## 5. Estrategia de calidad

### 5.1 Tipos de pruebas

- Pruebas unitarias de validaciones y reglas de negocio.
- Pruebas de integración con la base de datos.
- Pruebas de API o de vistas web.
- Pruebas de permisos y autenticación.
- Pruebas de conflictos entre reservas.
- Pruebas de regresión después de modificar requisitos.
- Pruebas de aceptación basadas en las especificaciones.

### 5.2 Riesgos y mitigaciones

**Riesgo 1: reservas simultáneas.**  
Mitigación: validar solapamientos en el servidor, controlar las transacciones y probar solicitudes concurrentes cuando corresponda.

**Riesgo 2: permisos incorrectos.**  
Mitigación: aplicar autorización en el servidor y probar accesos permitidos y denegados.

**Riesgo 3: requisitos ambiguos.**  
Mitigación: establecer escenarios de aceptación verificables antes de implementar.

**Riesgo 4: errores en código generado por IA.**  
Mitigación: revisar el código, ejecutar pruebas y verificar el comportamiento real.

**Riesgo 5: cambios que rompan funcionalidades existentes.**  
Mitigación: ejecutar pruebas de regresión y gestionar los cambios mediante OpenSpec.

**Riesgo 6: pérdida o inconsistencia de datos.**  
Mitigación: definir restricciones de integridad, validar las operaciones y conservar copias de seguridad cuando corresponda.

### 5.3 Verificación de requisitos

Cada requisito deberá relacionarse con uno o más escenarios de aceptación y pruebas. Los resultados se registrarán para comprobar qué requisitos están implementados y cuáles continúan pendientes.

## 6. Uso de SDD e inteligencia artificial

### 6.1 Uso de OpenSpec

OpenSpec será utilizado para mantener las especificaciones funcionales, documentar propuestas de cambio, descomponer el trabajo en tareas y registrar la evolución de los requisitos.

### 6.2 Transformación del plan en especificaciones

Las necesidades identificadas en este documento se convertirán en requisitos claros y escenarios de aceptación. Antes de programar se revisarán su consistencia, alcance y correspondencia con el plan de ingeniería.

### 6.3 Actividades delegadas a la IA

La IA podrá ayudar a proponer estructuras de código, modelos, validaciones, pruebas, documentación y correcciones. Sus resultados serán considerados propuestas sujetas a revisión.

### 6.4 Verificación del código

Se revisarán las diferencias de Git, la coherencia con las especificaciones, las validaciones del servidor, los permisos, los resultados de las pruebas y el comportamiento ante casos límite.

### 6.5 Responsabilidad del estudiante

El estudiante será responsable de justificar la arquitectura, aprobar las especificaciones, revisar el código generado, interpretar las pruebas, gestionar los cambios y explicar las decisiones técnicas durante la sustentación.

## 7. Trazabilidad

Se mantendrá una relación entre:

- Plan de ingeniería: decisiones y alcance.
- Especificaciones OpenSpec: requisitos y escenarios.
- Tareas de implementación: actividades derivadas de los requisitos.
- Código fuente: comportamiento implementado.
- Pruebas automatizadas: evidencia de cumplimiento.
- Historial Git: registro cronológico de las decisiones y modificaciones.

## 8. Criterios generales de aceptación

El sistema deberá permitir gestionar los espacios, administrar usuarios y permisos, registrar solicitudes, validar la disponibilidad, impedir solapamientos, tramitar solicitudes, cancelar reservas conforme a las reglas establecidas y consultar el historial.

Ninguna reserva podrá superar cuatro horas consecutivas. Esta regla se incorporará y verificará mediante un cambio formal de OpenSpec antes de modificar el código correspondiente.
