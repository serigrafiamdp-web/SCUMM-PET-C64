# TEST ECM RUNTIME 05 — FLT16 — TWO LOOPS + HOLD

Base:
- TEST_ECM_RUNTIME_04_FLT16_ONE_LOOP_HOLD.zip = PASS

Cambio único:
- Resource02 scheduler loop count: 1 -> 2
- HOLD inmediato tras exactamente dos loops completos
- Sprite Resource02: OFF
- Cadence: lenta permanente [24,24,24,28] x4
- Payload, decoder, ECM, charset, BG, SID y layout: sin cambios

Objetivo:
Confirmar estabilidad de dos loops completos.
Si PASS, siguiente: 3 loops + HOLD.

Artifact:
- TEST_ECM_RUNTIME_05_FLT16_TWO_LOOPS_HOLD.zip
- SHA256: a2f19374c5381150996e62b139115f9e61f7b6df5180309099e5143a083cfb94
- Estado: PENDIENTE PASS/FAIL
