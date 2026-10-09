# MASTER 09 OCT 2026 — PASS

Estado estable confirmado en runtime.

## Snapshot

`MASTER_SCUMM_PET_09_OCT_2026_HALITO1_AUTOMIX_HALITO2_FRESH_PASS.zip`

SHA-256:

`2a84c3298f8053934db8f4ece8e1afaf48fb85a49a2bdef0768d4b818a1a2ed2`

## Contratos validados

- HALITO 1 AUTO/MIX completo.
- SCREEN por Frame mezcla RLE / BITMAP_DELTA / CHANGES.
- COLOR optimizado con cadena cerrada.
- Ahorro físico neto HALITO 1: 4999 B = 4.88 KiB (~40.5%).
- Resource02 / HALITO 2 vuelve a cargar fresco desde disco.
- Fresh Frame01 debe decodificar según su codec; no asumir RAW/FULL4.
- HALITO 2 fresh SCREEN RLE + COLOR RLE = PASS.
- SID2, timing, sprites, scheduler y loop = PASS.

## Nota de archivo

El ZIP exacto está preservado también en la Library del proyecto con el
checksum anterior. Este directorio fija el estado MASTER en GitHub antes
de continuar con la integración en la TOOL normalizadora.
