# MASTER 13 OCT 2026 — ECM + BORDER + ANIMATED CHARS V0.56 — PASS

Estado estable confirmado en runtime.

## Snapshot exacto del motor

`MASTER_SCUMM_PET_13_OCT_2026_ECM_BORDER_ANIMATED_CHARS_V056_PASS.zip`

SHA-256:

`6c37bd12ab8f626daf06f042ea49f5cd63a1662348205c3c18b4be2c8f1462d7`

El archivo exacto está preservado en la Library raíz:

`/MASTER_SCUMM_PET_13_OCT_2026_ECM_BORDER_ANIMATED_CHARS_V056_PASS.zip`

Este MASTER es byte por byte el TEST runtime confirmado PASS, renombrado sin modificar su contenido.

## Avances promovidos

### Motor / runtime
- ECM de Resource02 validado con charset físico de 512 B / 64 glyphs.
- Screen codes ECM preservan 8 bits: bits 0-5 = glyph físico, bits 6-7 = selector BG0-BG3.
- Animación continua validada dentro de una sola sesión del scheduler.
- BORDER por frame validado: framepack byte 7 -> runtime header byte 3 -> $D020.
- Animated Chars procedurales validados sobre el charset activo.
- Cada Animated Char conserva tick/counter independiente.
- Tabla ACH1 final validada con 4 entradas:
  - $0068 -> glyph $0D -> RIGHT -> tick 6
  - $0058 -> glyph $0B -> LEFT  -> tick 6
  - $0028 -> glyph $05 -> LEFT  -> tick 6
  - $0030 -> glyph $06 -> RIGHT -> tick 6
- No se mueven caracteres no marcados.
- INTRO / HALITO / PORTADA / SID / BORDER sin regresiones reportadas.

### Contrato ECM aprendido
- LVLLVL puede editar en Text Art con índice lógico 0..255.
- Al exportar ECM, LVLLVL reorganiza/compacta los tiles al charset físico de 64 glyphs.
- `charset.bin` exportado es la verdad física del recurso.
- `animatedCharsTable.asm` ya está generado después de ese remapeo.
- `charOffset` de Animated Chars se usa DIRECTAMENTE como offset físico en el charset exportado.
- NO aplicar `& $3F` al `charOffset` de Animated Chars.
- `screenCode & $3F` se usa únicamente al resolver una celda ECM de pantalla.
- No deduplicar Animated Chars por bitmap.

### Tool oficial
- Tool promovida: **V0.56 ECM PHYSICAL ANIM OFFSETS PASS**.
- Ruta oficial:
  `tools/lvllvl-normalizer/index.html`
- Snapshot congelado:
  `tools/lvllvl-normalizer/versions/LVLLVL_SCUMM_WEB_TOOL_V0_56_ECM_PHYSICAL_ANIM_OFFSETS_PASS.html`
- Conserva BORDER por frame + export ACH1 + validación de offsets físicos ECM.

## Pendiente
- Animated Char tipo 5 FRAMES / `animatedCharsData` todavía no está promovido.
- No modificar ese contrato hasta validarlo con un test aislado PASS.

## Punto de retorno previo
- `milestone/animated-chars-v056-runtime-pass-13-oct-2026`
