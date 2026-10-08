# SCUMM-PET-C64

Mini C64 SCUMM-style engine for PETSCII/character animation and SID music.

## Current stable MASTER

**BANK16F = PASS**

Exact snapshot:

`releases/BANK16F/TEST_BANK16F_POSTINTRO_CPU_FILL_8D00_8FFF.zip`

SHA-256:

`e0e7374844aedae1f01941ab4acdd89130afcd0797a7db1616e211b6d303730b`

## Repository layout

- `engine/` — complete materialized BANK16F working tree, including `main.ras`, assets, disk files, LEMMINGS source frames and archived unused resources.
- `docs/SCUMM_HIBRIDO_MAPA_MILESTONES.txt` — live architecture contract.
- `docs/SCUMM_HIBRIDO_LOG.txt` — consolidated PASS/FAIL history and decisions.
- `releases/BANK16F/` — exact reproducible PASS snapshot + checksum.
- `.github/workflows/materialize-bank16f.yml` — verifies the snapshot and materializes `engine/`.

## Versioning rule

**`main` only contains confirmed PASS states.**

Experimental tests should not replace the MASTER until they have passed the full runtime pipeline.

Current next test documented in `docs/`: **BANK16G**, still pending validation.
