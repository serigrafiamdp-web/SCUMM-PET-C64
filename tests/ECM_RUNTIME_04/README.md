# TEST ECM RUNTIME 04 — FLT16 — ONE LOOP + HOLD

Base:
- TEST_ECM_RUNTIME_03_FLT16_NO_SPRITE_SLOW_CADENCE.zip
- Resource02 sprite OFF.
- Slow cadence [24,24,24,28] x4 permanent.

Change isolated:
- First Resource02 scheduler block: loop count $03 -> $01.
- After exactly one completed loop, infinite HOLD.
- No second block, no later phase.
- HOLD replaces the former second scheduler call footprint with JMP + 8 NOPs, so subsequent code addresses do not move.

No changes:
- visual payloads
- codecs/decoder
- ECM state
- charset
- BG0-BG3
- SID2
- physical layout

Artifact:
- TEST_ECM_RUNTIME_04_FLT16_ONE_LOOP_HOLD.zip
- SHA256: bc1263479d54a90258a339f185e40a0701d9c8b087d833e97de9d010f071897a

Expected:
F1 -> ... -> F16 -> F1 boundary, then HOLD.
