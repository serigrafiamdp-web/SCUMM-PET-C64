# TEST BORDER RUNTIME 01 — V0.53b

Base:
- milestone/ecm-single-scheduler-pass-13-oct-2026
- MILESTONE_ECM_SINGLE_SCHEDULER_PASS_13_OCT_2026.zip = PASS

Goal:
Integrate LVLLVL per-frame BORDER metadata into the runtime without changing header size or resource layout.

Contract:
- SCUMM framepack entry byte 7 = BORDER.
- Runtime 12-byte frame header byte 3 = BORDER.
- Runtime header bytes 4..7 = BG0..BG3.
- Fresh Frame 1 reads $4403 -> $D020.
- Later frames: scheduler helper already reads header byte 3; its 3 NOP reserve is replaced by STA $D020.

Compatibility:
- Legacy runtime containers had byte 3 = $00.
- Existing code already forced border black.
- Therefore HALITO / INTRO / PORTADA should remain visually unchanged.
- Only newly integrated resources with nonzero BORDER can visibly change border per frame.

Test package:
TEST_BORDER_RUNTIME_01_FLT_V053B_PER_FRAME_BORDER.zip
SHA256:
f0523beea602d414b4117fe85c3c2059373005cd0db3f9119f7560074d235866

Current sample:
- FLT 16F V0.53b
- BORDER = $00 on all 16 frames
- Expected visual result: no border color change yet, but metadata path is exercised.
- Status: PENDING PASS/FAIL
