# TEST ECM RUNTIME 08 — FLT16 ECM BIT6 GUARD

Base:
- TEST_ECM_RUNTIME_03_FLT16_NO_SPRITE_SLOW_CADENCE.zip
- Resource02 sprite OFF
- Slow cadence permanent
- Continuous loop

Single change:
- Existing IRQ call at $2CE0 is redirected from JSR $4078 to JSR $2D20.
- New trampoline at free gap $2D20:
  - LDA $D011
  - ORA #$40
  - STA $D011
  - JSR $4078
  - JMP $2CE3
- No original code is shifted.
- $D021-$D024 deliberately untouched.

Purpose:
Determine whether the cyclic FLT corruption is caused by VIC-II ECM bit 6 being temporarily cleared.

Artifact:
- TEST_ECM_RUNTIME_08_FLT16_ECM_BIT6_GUARD.zip
- SHA256: eca36a2fc165665bcd769623f1882dce7759b26126aa656c03132ae5099ad751
- Status: PENDING PASS/FAIL
