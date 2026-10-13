# MILESTONE — ECM SINGLE SCHEDULER PASS — 13 OCT 2026

Estado: **PASS**

Punto de retorno del proyecto para la integración de animaciones ECM.

## Artefacto exacto

`MILESTONE_ECM_SINGLE_SCHEDULER_PASS_13_OCT_2026.zip`

SHA256:

`6f34422f82a9091dbcfa9d764a89639c57017d373069bfedcf39ea5b1af8d799`

`main.ras` dentro del milestone:

`39f3d4a4a4826cba15baa99b2627a5bd35023fa32b3b182b86268d3bbbf58d87`

## Hallazgo validado

La corrupción visual no proviene de una frame ECM específica.

- F16 -> F1 funciona correctamente mientras la animación permanece dentro de una sola sesión del scheduler.
- La corrupción aparecía al dividir la misma animación en dos llamadas consecutivas a `$3740`.
- TEST 11 ejecutó la animación de forma continua en una sola llamada y atravesó limpio el punto donde antes aparecía la corrupción.

Contrato vigente:

> Una animación continua debe permanecer en una sola sesión del scheduler, salvo que exista un reset explícito de estado interno previamente validado.

## No considerar causa confirmada

- SID: sólo correlación temporal; no quedó demostrado como causa.
- ECM: funciona correctamente en ejecución continua.
- TEST 08 / 08B: diagnósticos inválidos porque activaban ECM fuera de la ventana visual correcta.

## Limpieza

Se eliminaron los TXT auxiliares de pruebas. Los únicos TXT de registro que se conservan dentro del milestone son:

- `SCUMM_HIBRIDO_LOG.txt`
- `SCUMM_HIBRIDO_MAPA_MILESTONES.txt`

## Cómo volver

Usar el ZIP cuyo SHA256 figura arriba. Esta rama debe tratarse como congelada y no como rama de experimentación.
