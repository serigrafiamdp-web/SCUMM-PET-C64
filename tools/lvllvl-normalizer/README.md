# LVLLVL → SCUMM Normalizer

Web tool used by **SCUMM-PET-C64** to inspect LVLLVL C64 NEW exports and normalize them into the engine resource contract.

## Official current tool

`index.html`

Current version: **V0.40**

Engine profile: **ANIMATION_16F_V2E**

The tool runs locally in the browser. It imports an LVLLVL SOURCE.zip, reconstructs frames and Color RAM, validates the resource, applies the selected color policy, and can export a SCUMM resource package.

## Version archive

Frozen known versions are stored in:

`versions/`

Current frozen baseline:

`versions/LVLLVL_SCUMM_WEB_TOOL_V0_40.html`

When a newer tool is validated:

1. preserve the old known-good version in `versions/`;
2. replace `index.html` with the new validated version;
3. update the architecture map and project log;
4. do not call a tool version official until its export has passed the engine runtime tests.

## V0.40 contract

- Resource type: ANIMATION_16F
- Engine profile: ANIMATION_16F_V2E
- Maximum frames: 16
- Charset: 2048 bytes
- Screen delta base: visible Frame N-1
- Runtime copies front -> back before map delta
- BITMAP_DELTA fast path: bitmap byte $00 skips 8 cells
- Presentation order: screen swap -> Color RAM
- Optional HALITO color normalization: $02 -> $0C
- $01 white is preserved
- Whole-frame deduplication: OFF

The current tool still contains the historical 18,688-byte framepack budget used by the validated V2E layout. If the universal animation bank is promoted later, this budget must only be changed after the new memory contract is confirmed PASS.
