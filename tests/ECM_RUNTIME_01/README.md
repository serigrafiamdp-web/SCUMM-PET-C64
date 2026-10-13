# TEST ECM RUNTIME 01 — FLT 16F

Base funcional autoritativa:
- TEST_FRESH_DISPATCHER_01_HEADER_RLE_DYNAMIC_POINTER(1).zip
- SHA256: 9cc232337fdda2311a87b0b7fcfb063ee95e7a693703d258395fb4f7848c0777
- Estado: PASS

Test derivado:
- TEST_ECM_RUNTIME_01_FLT16_TOOL_V052.zip
- SHA256: 157676dd252cb85ea140c270dd62ae67fc78a4ed08975828a955458f8f57dd65
- Estado: PENDIENTE PASS/FAIL

Origen visual:
- FLT_16_FRAMES_SCUMM_ANIMATION_V2E.zip
- Tool V0.52 ECM TEST
- Perfil: ANIMATION_16F_ECM_V1
- 16 frames
- charset ECM: 512 B / 64 glyphs
- screen code bits 0-5 = glyph, bits 6-7 = selector BG0-BG3

Cambios aislados:
- Resource02 reempacado dentro de las cuatro cargas A/B/C/D existentes.
- Sin KrillLoad adicional.
- Charset ECM staged en $9E00-$9FFF y copiado a $3800-$39FF al handoff.
- D011 activa ECM sólo al mostrar Resource02.
- Tabla dinámica F2-F16+loop en $3490-$349F.
- Loop FLT F16->F1 en $6F00.
- SID/timing/sprites/dispatcher/codecs sin rediseño.

Layout:
F1  $4400
F2  $4800
F3  $4A00
F4  $4C00
F5  $4E00
F6  $4F00
F7  $5200
F8  $5400
F9  $5700
F10 $5A00
F11 $5D00
F12 $6000
F13 $6300
F14 $6600
F15 $6900
F16 $6C00
LOOP $6F00
ECM CHARSET $9E00-$9FFF
