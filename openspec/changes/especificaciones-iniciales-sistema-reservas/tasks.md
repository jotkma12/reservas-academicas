# Tasks

## 1. Revisión de las especificaciones

- [ ] 1.1 Revisar spaces/spec.md contra la propuesta y el plan de ingeniería; verificar que los requisitos cubran registro, consulta, actualización, unicidad y estados de los espacios.
- [ ] 1.2 Revisar users/spec.md contra la propuesta y el plan de ingeniería; verificar unicidad del correo, validación de datos, protección de credenciales y estados de las cuentas.
- [ ] 1.3 Revisar permissions/spec.md y contrastar los permisos de Solicitante, Gestor de espacios y Administrador con las responsabilidades descritas en el plan de ingeniería; verificar que las operaciones permitidas y denegadas queden explícitas.

## 2. Coherencia documental

- [ ] 2.1 Contrastar proposal.md, design.md y las tres especificaciones; verificar que no existan contradicciones de alcance, seguridad o responsabilidades.
- [ ] 2.2 Confirmar que los escenarios de cada requisito describan condiciones WHEN y resultados THEN comprobables; verificar que cada requisito tenga al menos un escenario.
- [ ] 2.3 Revisar los artefactos del cambio para confirmar que no se hayan agregado requisitos ajenos al alcance ni modificado PLAN_INGENIERIA.md; verificar el resultado mediante revisión de Git.

## 3. Validación OpenSpec

- [ ] 3.1 Ejecutar openspec validate especificaciones-iniciales-sistema-reservas --strict y corregir los errores o advertencias que impidan una validación satisfactoria.
- [ ] 3.2 Ejecutar openspec status --change especificaciones-iniciales-sistema-reservas y verificar que proposal, specs, design y tasks figuren como completos.
- [ ] 3.3 Revisar git diff --check y el diff de los artefactos; verificar que no existan errores de formato y que los cambios correspondan únicamente a la documentación prevista.

## Workflow follow-up

- Revisar y aprobar los artefactos antes de archivar el cambio.
- Archivar el cambio cuando se hayan satisfecho los criterios de revisión de la actividad.
- Verificar que las especificaciones archivadas se hayan incorporado correctamente al repositorio.
- Crear un cambio OpenSpec separado para la implementación funcional cuando corresponda.
