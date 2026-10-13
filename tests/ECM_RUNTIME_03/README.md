# TEST ECM RUNTIME 03 — FLT16 — NO SPRITE + SLOW CADENCE

Base:
- TEST_ECM_RUNTIME_02_FLT16_NO_RESOURCE02_SPRITE.zip

Single isolation change:
- source of the cadence-copy loop changes from $2F60 (FAST) to $2F50 (SLOW).
- instruction count and copy-loop structure remain unchanged.
- Resource02 therefore stays at [24,24,24,28] x4 permanently.

Unchanged:
- Resource02 sprite remains disabled.
- ECM state.
- frame data/codecs.
- charset.
- BG0-BG3.
- SID2.
- dispatcher.
- loop.
- physical layout.

Expected interpretation:
- PASS: cyclic corruption disappears => fast cadence was the trigger.
- FAIL: cyclic corruption remains => investigate D011/ECM state writes next.

ZIP:
- TEST_ECM_RUNTIME_03_FLT16_NO_SPRITE_SLOW_CADENCE.zip
- SHA256: 85cf2917c3fcd4b599c19566090a871dc27956c5d463ee483154c0d4879d2034
