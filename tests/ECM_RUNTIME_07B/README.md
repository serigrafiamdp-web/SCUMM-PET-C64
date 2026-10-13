# TEST ECM RUNTIME 07B — 3 + 1 LOOPS — NO CODE SHIFT

Base:
- TEST_ECM_RUNTIME_03_FLT16_NO_SPRITE_SLOW_CADENCE.zip

Reason:
- Previous TEST 07 was not a clean isolation because the modified block grew by 3 bytes and shifted following code.

Sequence:
- scheduler call #1: 3 loops
- return
- scheduler call #2: 1 loop
- HOLD

Address preservation:
- Second loop count changes only $03 -> $01.
- Following SEI (1 byte) + LDX #$0F (2 bytes) is replaced by JMP HOLD (3 bytes).
- Therefore all subsequent code addresses remain unchanged.

Unchanged:
- Resource02 sprite OFF
- slow cadence
- ECM payload
- charset
- BG
- SID
- decoder
- physical layout

ZIP:
- TEST_ECM_RUNTIME_07B_FLT16_3PLUS1_NO_SHIFT.zip
- SHA256: 94d34b4d958935c238590862a93449c460efcc3f99e88ab5ae3146c689e8df6d
- Status: PENDING PASS/FAIL
