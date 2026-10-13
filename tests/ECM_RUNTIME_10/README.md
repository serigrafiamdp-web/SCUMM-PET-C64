# TEST ECM RUNTIME 10 — FLT numerada — SID B PLAY OFF

Base:
- TEST_ECM_RUNTIME_09_FLT_NUMBERED_RESOURCE_ONLY.zip

Hipótesis:
La corrupción visual coincide con momentos donde SID B agrega/cambia una voz.

Cambio único diagnóstico:
- disk_files/sid_b_stage.bin
- offset 3 / runtime $1003
- $A2 -> $60
- La entrada PLAY de SID B se convierte en RTS inmediato.

Se conserva:
- INIT SID B
- IRQ/raster
- scheduler
- Resource02 visual
- ECM
- charset
- BG0-BG3
- decoder
- timing visual
- page table
- loop F16->F1
- HALITO1 + SID A

Interpretación:
- Visual estable => la carga/interferencia de SID B PLAY es causal.
- Misma corrupción => SID B no es la causa principal.

ZIP:
TEST_ECM_RUNTIME_10_FLT_NUMBERED_SIDB_PLAY_OFF.zip
SHA256:
710d85886d093954afd91c281a319d9737a30938e96020cc0cf0c21b452c0056
