# TEST ECM RUNTIME 08B — Resource02-only ECM bit6 guard

Base:
- TEST_ECM_RUNTIME_03_FLT16_NO_SPRITE_SLOW_CADENCE.zip

Correction vs TEST 08:
- TEST 08 forced ECM globally in the master IRQ and therefore corrupted HALITO1.
- TEST 08B gates the guard by current resource ID.

Guard:
```asm
LDA $3714
CMP #$02
BNE skip_ecm
LDA $D011
ORA #$40
STA $D011
skip_ecm:
JSR $4078
JMP $2CE3
```

Expected:
- Resource01 / HALITO1 remains non-ECM.
- PORTADA A unchanged.
- Resource02 / FLT reasserts ECM bit 6 every IRQ.
- D021-D024 deliberately untouched.
- Sprite OFF and slow cadence remain as in TEST 03.

ZIP:
- TEST_ECM_RUNTIME_08B_FLT16_R2_ONLY_BIT6_GUARD.zip
- SHA256: 82a8a6ca5c78834a727775b698b21d2078d12afed20ad0286f74be5a955adc30
- Status: PENDIENTE PASS/FAIL
