# TEST BORDER RUNTIME 02 — V0.54

Base:
- TEST_BORDER_RUNTIME_01_FLT_V053B_PER_FRAME_BORDER.zip
- runtime BORDER mapping already present: frame header byte 3 -> VIC-II $D020

Input:
- FLT_16_FRAMES_SCUMM_ANIMATION_V2E (2).zip
- Tool V0.54 BORDER EDITOR TEST
- ECM, 16 frames

Per-frame border:
- F01 $0B
- F02 $04
- F03 $0B
- F04 $04
- F05 $0B
- F06 $04
- F07 $0B
- F08 $04
- F09 $0B
- F10 $04
- F11 $0B
- F12 $04
- F13 $0B
- F14 $04
- F15 $0B
- F16 $04

Runtime test package:
- TEST_BORDER_RUNTIME_02_FLT_V054_BORDER_0B_04.zip
- SHA256: d7281494052cf9c7a0a9f1df1cb665a88ab60b55d5b3fb8be9446bfceca10c8f
- Status: PENDING PASS/FAIL

Isolation:
- main.ras unchanged vs BORDER RUNTIME 01
- scheduler_helper_reloc.bin unchanged vs BORDER RUNTIME 01
- only Resource02 payload/page table regenerated from V0.54 export

Expected:
- HALITO1 / INTRO / PORTADA unchanged
- FLT border alternates dark gray ($0B) / purple ($04) frame by frame
