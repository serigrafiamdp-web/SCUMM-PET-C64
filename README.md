# SCUMM-PET-C64

Mini C64 SCUMM-style engine for PETSCII / character animation and SID music.

## Motor actual (resumen visual)

```text
                            +-----------------------+
                            |      MAIN ENGINE      |
                            | scenes / resources    |
                            +-----------+-----------+
                                        |
                +-----------------------+-----------------------+
                |                       |                       |
                v                       v                       v
        +---------------+       +---------------+       +---------------+
        | RESOURCE CORE |       |  VISUAL CORE  |       |  AUDIO CORE   |
        +---------------+       +---------------+       +---------------+
        | Descriptor V3 |       | LVLLVL data   |       | AUDIO SLOT A  |
        | Load-list ptr |       | Frames / V2E  |       | AUDIO SLOT B  |
        | Executor ptr  |       | VIC-II        |       | Fade / SID    |
        | Directory     |       | Color RAM     |       | handoff A->B  |
        +-------+-------+       +-------+-------+       +-------+-------+
                |                       |                       |
                +-----------------------+-----------------------+
                                        |
                                        v
                                 +-------------+
                                 | MASTER IRQ  |
                                 | raster $FA  |
                                 +------+------+ 
                                        |
                       +----------------+----------------+
                       |                |                |
                       v                v                v
                    SID PLAY         VISUAL          ENGINE
                                   ScrollStep        events
```

## Cadena objetivo del proyecto

```text
INTRO CARGA (4F LEMMINGS)
        -> CARGA 1 (ANIMACION 1 + 2 SIDs + PORTADA gfx A)
        -> ANIMACION 1
        -> PORTADA visible / ventana de carga
        -> CARGA 2 (ANIMACION 2 + SID siguiente + mismo engine de PORTADA con otro grafico)
        -> ANIMACION 2
        -> repetir cadena
```

## Estado estable actual

**BANK16F = PASS**

Snapshot exacto:

`releases/BANK16F/TEST_BANK16F_POSTINTRO_CPU_FILL_8D00_8FFF.zip`

SHA-256:

`e0e7374844aedae1f01941ab4acdd89130afcd0797a7db1616e211b6d303730b`

## Reglas del repositorio

- **`main` solo contiene estados PASS confirmados.**
- Los experimentos nuevos no reemplazan el MASTER hasta pasar el pipeline completo.
- `docs/SCUMM_HIBRIDO_MAPA_MILESTONES.txt` es el contrato vivo de arquitectura.
- `docs/SCUMM_HIBRIDO_LOG.txt` conserva el historial consolidado PASS / FAIL.

## Estructura del repositorio

- `engine/` — árbol materializado completo del MASTER BANK16F PASS.
- `docs/` — mapa de arquitectura y log vivo del proyecto.
- `releases/BANK16F/` — snapshot exacto del último PASS + checksum.
- `tools/lvllvl-normalizer/` — TOOL normalizadora web oficial del proyecto.
- `.github/workflows/` — verificación y materialización del MASTER.

## TOOL normalizadora web

Ruta oficial actual:

`tools/lvllvl-normalizer/index.html`

Versión congelada validada:

`tools/lvllvl-normalizer/versions/LVLLVL_SCUMM_WEB_TOOL_V0_40.html`

Perfil vigente:

`ANIMATION_16F_V2E`

## Próximo paso documentado

**BANK16G** — pendiente de validación.

Objetivo: comprobar si todo `$8D00-$9FFF` es RAM reutilizable post-INTRO sin agregar un `KrillLoad` extra.
