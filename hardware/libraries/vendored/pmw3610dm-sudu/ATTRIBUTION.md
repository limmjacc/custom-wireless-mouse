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

## Where to actually buy this part

Confirmed live listing (2026-09-27): AliExpress item 1005007118767775,
"New and Original PMW3610DM-SUDU + LM18-LSI DIP" —
<https://de.aliexpress.com/item/1005007118767775.html> (same listing,
mirrored across AliExpress's regional storefronts). This bundles the
sensor with its matched LM18-LSI lens (LENS1 on the schematic), sold
together rather than separately. This part remains genuinely absent
from DigiKey, Mouser, and LCSC — that is a real characteristic of its
supply chain, not a gap in this project's sourcing effort. Re-check
price/stock on the live listing before ordering.

## 3D model — a real PMW3360 model, verified dimensionally against PMW3610

No 3D model exists for PMW3610DM-SUDU itself under any name — not in
the open-hardware reference repository, not from PixArt, not on
JLCPCB/EasyEDA, not on any general CAD-model search. Consistent with
this part's already-documented non-standard sourcing channel (absent
from DigiKey/Mouser/LCSC).

`3dmodels/pmw3610dm-sudu-16-pin-approx.step` is instead a community
GrabCAD model of PixArt's **PMW3360DM-T2QU**
(<https://grabcad.com/library/pmw3360dm-mouse-sensor-1>), a different
PixArt sensor. This is a deliberate substitution, not a mistake: both
parts' real datasheet package outline drawings were compared
dimension-by-dimension, and every external mechanical figure matches
exactly —

| Dimension | PMW3610DM-SUDU | PMW3360DM-T2QU |
|---|---|---|
| Body width | 9.10mm | 9.10mm |
| Body length | 16.20mm | 16.20mm |
| Width at shoulder | 10.90mm | 10.90mm |
| Depth | 10.10mm | 10.10mm |
| Pin count / pitch | 16 pins, 1.78mm | 16 pins, 1.78mm |
| Pin width | 0.50mm | 0.50mm |
| Package doc number | `LSR_INT_16A_Pkg_005` | `LED_INT_16A_Pkg_002` |

Both share the same `_16A` molded lead-frame DIP tooling family (per
PixArt's own package doc numbers) — this is PixArt reusing one
mechanical package across sensor generations, not a coincidence.

**The one real difference**: PMW3610 integrates a VCSEL laser (a
"VCSEL hole" in its datasheet drawing); PMW3360 integrates an IR LED
instead (a "LED Hole" in its own drawing) — different optical
technology, different internal die, paired with a different lens
(LM18-LSI vs. LM19-LSI). This affects the small feature right at the
optical aperture, not the overall body silhouette, pin layout, or
mounting footprint. Accurate for board-level 3D visualization and
enclosure/clearance checks; not a claim that the aperture/lens detail
is pixel-accurate to the real PMW3610 part.
