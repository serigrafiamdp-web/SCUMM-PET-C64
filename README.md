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

**MASTER 13/10/2026 = PASS**

ECM + BORDER por frame + Animated Chars procedurales + Tool V0.56.

Snapshot exacto del motor:

`MASTER_SCUMM_PET_13_OCT_2026_ECM_BORDER_ANIMATED_CHARS_V056_PASS.zip`

SHA-256:

`6c37bd12ab8f626daf06f042ea49f5cd63a1662348205c3c18b4be2c8f1462d7`

Estado validado:

- Conserva los contratos anteriores HALITO1 AUTO/MIX + HALITO2 fresh load.
- Resource02 ECM: charset físico 512 B / 64 glyphs, screen codes de 8 bits.
- Animación continua dentro de una sola sesión del scheduler.
- BORDER por frame: framepack byte 7 -> runtime header byte 3 -> $D020.
- Animated Chars procedurales 0..4: PASS.
- Cada Animated Char conserva tick/counter independiente.
- LVLLVL remapea/compacta Text Art 0..255 al exportar ECM.
- `animatedCharsTable.asm charOffset` se usa como offset físico directo del charset exportado.
- NO aplicar `& $3F` a offsets de Animated Chars.
- TEST final de 4 Animated Chars: sólo se mueven los 4 caracteres seleccionados.
- INTRO / HALITO / PORTADA / SID / BORDER sin regresiones reportadas.

Release GitHub:

`releases/MASTER_13_OCT_2026_ECM_BORDER_ANIMATED_CHARS_V056/`

El ZIP exacto está preservado en Library raíz con el checksum anterior.

## Reglas del repositorio

- **`main` solo contiene estados PASS confirmados.**
- Los experimentos nuevos no reemplazan el MASTER hasta pasar el pipeline completo.
- `docs/SCUMM_HIBRIDO_MAPA_MILESTONES.txt` es el contrato vivo de arquitectura.
- `docs/SCUMM_HIBRIDO_LOG.txt` conserva el historial consolidado PASS / FAIL.

## Estructura del repositorio

- `engine/` — árbol materializado histórico; el MASTER vigente se registra en `releases/` y en la documentación viva.
- `docs/` — mapa de arquitectura y log vivo del proyecto.
- `releases/MASTER_13_OCT_2026_ECM_BORDER_ANIMATED_CHARS_V056/` — manifiesto del MASTER PASS vigente + checksum.
- `tools/lvllvl-normalizer/` — TOOL normalizadora web oficial del proyecto.
- `.github/workflows/` — verificación y materialización del MASTER.

## TOOL normalizadora web

Ruta oficial actual:

`tools/lvllvl-normalizer/index.html`

Versión oficial promovida:

**V0.56 ECM PHYSICAL ANIM OFFSETS PASS**

Snapshot congelado:

`tools/lvllvl-normalizer/versions/LVLLVL_SCUMM_WEB_TOOL_V0_56_ECM_PHYSICAL_ANIM_OFFSETS_PASS.html`

Perfil vigente:

`ANIMATION_16F_ECM_V1 / ANIMATION_16F_V2E`

Contratos promovidos en la Tool:

- Fresh F1 autocontenida FULL/RLE.
- RLE / CHANGES / BITMAP_DELTA compatibles con el motor.
- BORDER editable por frame.
- ECM con 64 glyphs físicos y BG0-BG3.
- Animated Chars ACH1 con tick independiente por entrada.
- Offsets Animated Char físicos preservados directamente desde LVLLVL.
- Sin deduplicación por bitmap.

## Próximo paso documentado

- Validar Animated Char tipo 5 FRAMES / `animatedCharsData` en un test aislado.
- Mantener V0.56 y este MASTER sin cambios mientras se prueba esa extensión.
- Cualquier función nueva entra primero como TEST PASS/FAIL antes de promoverse.

