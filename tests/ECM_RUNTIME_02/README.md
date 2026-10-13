# TEST ECM RUNTIME 02 — FLT16 — RESOURCE02 SPRITE OFF

Base:
- TEST_ECM_RUNTIME_01_FLT16_TOOL_V052.zip = PASS.
- SHA256 base: 157676dd252cb85ea140c270dd62ae67fc78a4ed08975828a955458f8f57dd65

Nuevo test:
- TEST_ECM_RUNTIME_02_FLT16_NO_RESOURCE02_SPRITE.zip
- SHA256: 17c2c1cc4718a37c8b79bb41c4a80c8dfae35f8c6938fa449aa8f64505dc51e9
- Estado: PENDIENTE PASS/FAIL

Cambio aislado:
- SOLO Resource02:
  - se desactiva JSR $A300 (SHOW/INIT sprite);
  - no se activan $A6F0/$A6F1 (movimiento).
- La llamada $A300 de PORTADA A permanece intacta.
- Se conservan exactamente:
  - 3 loops iniciales,
  - 3 loops intermedios,
  - transición a cadence rápida,
  - ECM,
  - SID2,
  - dispatcher,
  - codecs,
  - layout,
  - loop F16->F1.

Objetivo:
Confirmar si el bug que aparece al entrar el sprite desaparece al mantener
Resource02 completamente sin Sprite Engine visible/móvil.
