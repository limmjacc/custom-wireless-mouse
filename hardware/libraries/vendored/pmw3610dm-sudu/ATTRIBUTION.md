---
name: pmw3610dm-sudu-attribution
---

# PMW3610DM-SUDU symbol and footprint — attribution

The KiCad symbol (`PMW3610DM-SUDU.kicad_sym`) and footprint
(`PMW3610DM-SUDU.pretty/PMW3610DM-SUDU_16Pin.kicad_mod`) in this directory
were extracted from [siderakb/pmw3610-pcb](https://github.com/siderakb/pmw3610-pcb),
an open-hardware PMW3610 breakout board by **siderakb**, and adapted for
standalone use in this project (isolated to the single PMW3610DM-SUDU part;
the footprint reference on the symbol was repointed at this library's own
name so it resolves without the rest of that project's files).

- Upstream repository: <https://github.com/siderakb/pmw3610-pcb>
- License: CERN Open Hardware Licence v2 — Permissive (CERN-OHL-P v2), reproduced
  in full in `LICENSE-CERN-OHL-P-v2.txt` in this directory.
- Files vendored: `pmw3610_pcb.kicad_sym` (symbol only) and
  `pmw3610_pcb.pretty/PMW3610DM-SUDU 16Pin.kicad_mod`.

No modification was made to the underlying geometry, pin mapping, or pad
definitions — only the file names and the internal footprint cross-reference
were changed to fit this project's library layout.

## 3D model — none found anywhere

No 3D STEP/WRL model for PMW3610DM-SUDU could be found through any
channel checked: not in the open-hardware reference repository itself
(no `3dshapes`/`.step` files exist in that project), not on PixArt's own
datasheet or site, not on JLCPCB's EasyEDA library, and not on any
general CAD-model search. This is consistent with the part's
already-documented non-standard sourcing channel (absent from DigiKey/
Mouser/LCSC) — it simply isn't the kind of part major CAD-library
sites carry. A 3D-accurate render of this board's U2 position isn't
achievable without either measuring the physical part and modeling it
by hand, or asking PixArt directly.
