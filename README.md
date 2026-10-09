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

**MASTER 09/10/2026 = PASS**

HALITO 1 AUTO/MIX + HALITO 2 fresh load comprimido.

Snapshot exacto:

`MASTER_SCUMM_PET_09_OCT_2026_HALITO1_AUTOMIX_HALITO2_FRESH_PASS.zip`

SHA-256:

`2a84c3298f8053934db8f4ece8e1afaf48fb85a49a2bdef0768d4b818a1a2ed2`

Estado validado:

- HALITO 1: F01 RLE, F02 CHANGES, F03-F13 BITMAP_DELTA, F14-F15 RLE, F16 CHANGES.
- COLOR: cadena optimizada y cerrada.
- Ahorro neto HALITO 1: 4999 B = 4.88 KiB (~40.5%).
- HALITO 2: Resource02 carga fresco desde disco y reconstruye F01 desde SCREEN RLE + COLOR RLE.
- SID2, timing, sprites y loop: PASS.

## Reglas del repositorio

- **`main` solo contiene estados PASS confirmados.**
- Los experimentos nuevos no reemplazan el MASTER hasta pasar el pipeline completo.
- `docs/SCUMM_HIBRIDO_MAPA_MILESTONES.txt` es el contrato vivo de arquitectura.
- `docs/SCUMM_HIBRIDO_LOG.txt` conserva el historial consolidado PASS / FAIL.

## Estructura del repositorio

- `engine/` — árbol materializado histórico; el MASTER vigente se registra en `releases/` y en la documentación viva.
- `docs/` — mapa de arquitectura y log vivo del proyecto.
- `releases/MASTER_09_OCT_2026/` — manifiesto del MASTER PASS vigente + checksum.
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

Integrar en la TOOL normalizadora el contrato aprendido con HALITO 1:

- optimización de COLOR sobre glyphs realmente vacíos;
- generación por Frame de RLE / BITMAP_DELTA / CHANGES;
- selección AUTO del payload más chico;
- export compatible con fresh load, respetando el codec real de Frame01.
