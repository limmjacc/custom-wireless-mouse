---
name: omron-b3u-1000p-attribution
---

# Omron B3U-1000P ultra-small SMD tactile switch — attribution

- **Footprint** (`omron-b3u-1000p.pretty/switch-smd-omron-b3u-1000p.kicad_mod`):
  copied unmodified (geometry, pad sizes/pitch) from KiCad's own official
  library, `Button_Switch_SMD.pretty/SW_SPST_B3U-1000P.kicad_mod` — this is
  an exact-match footprint for this specific part number, not a generic
  substitute.
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **3D model** (`3dmodels/switch-smd-omron-b3u-1000p.step`): copied from
  KiCad's own official 3D model pack
  (`Button_Switch_SMD.3dshapes/SW_SPST_B3U-1000P.step`), same license as
  the footprint above.
- **Symbol** (`omron-b3u-1000p.kicad_sym`): hand-drawn, reusing the body
  graphic from KiCad's own generic `Switch:SW_Push` symbol (same license
  as above) — electrically this part is nothing more than a 2-terminal
  SPST-NO momentary pushbutton, so the generic push-button glyph is
  accurate, not a simplification.

## Part selection and verification (2026-09-27)

Selected to replace SW5 (the scroll-wheel middle-click switch), which
previously used the same Omron D2FC-F-7N(20M) part as the L/R/FN
buttons (SW2-4). That part's 12.8×5.8×6.5mm THT body is far too tall to
fit *underneath* the scroll wheel assembly, which mounts on ENC1's
shaft directly above SW5's location — a real mechanical clearance
problem caught during layout, not a schematic-only concern.

Datasheet: `hardware/datasheets/omron-b3u-1000p-datasheet.pdf` (Omron
Corporation, Cat. No. A162-E1-07), downloaded directly from
omronfs.omron.com and read in full before selection.

Deep-audited against several other ultra-low-profile tactile switch
candidates before choosing this one:

| Candidate | Height | Package | Verdict |
|---|---|---|---|
| **Omron B3U-1000P** | **1.6mm** | 3.0×2.5mm SMD, 2-pin | **Selected** — real DigiKey.ca stock, exact KiCad library match |
| TE Connectivity FSM4JSMATR | 5.25mm | 6×10mm SMD | Rejected — barely shorter than the part being replaced |
| Panasonic EVQ-PUC02K | not specified, side-actuated | 6.4×3.5mm | Rejected — side-actuated (button press direction is horizontal, not vertical); wrong actuation geometry for a top-mounted wheel plunger |

Key verified specs from the datasheet (page 1, "Ratings/Characteristics"
and "Operating Characteristics" tables):

- Height: **1.6mm** (vs. D2FC-F-7N's 6.5mm — the entire reason for this
  swap).
- Contact form: SPST-NO, 2 terminals (no COM/NO/NC distinction like the
  D2FC — this is a simpler part electrically, not a like-for-like
  pinout swap).
- Operating force: 1.50 N ± 0.49 N (153 ± 50 gf) — comparable click
  feel to a standard mouse button, verified via the datasheet's
  "Operating force (OF)" spec.
- Rating: 1 to 50mA, 3 to 12VDC (resistive load) — comfortably covers a
  logic-level GPIO input pulled through a resistor, the same class of
  load as the D2FC switches it replaces.
- Mechanical life: 200,000 operations minimum.
- Degree of protection: IEC IP40 (dust-proof, no liquid rating).

## Sourcing (2026-09-27)

Manufacturer part number **B3U-1000P** (Aratas, formerly Omron
Electronic Components), confirmed via a live DigiKey.ca fetch:

- Distributor: DigiKey.ca
- SKU: [SW1020CT-ND](https://www.digikey.ca/en/products/detail/omron-electronics-inc-emc-div/B3U-1000P/1534338) (cut tape; also SW1020TR-ND tape & reel, SW1020DKR-ND Digi-Reel)
- Status: Active
- Stock at time of check: 129,510 units
- Price: $1.83 CAD (qty 1), $1.45 CAD (qty 25)

## Pinout note

No terminal numbers are printed on the physical switch itself (per the
datasheet's own note: "No terminal numbers are indicated on the
Switches") — it is a symmetric 2-pad SPST part, so either pad may be
wired to either side of the switched net. Pin "1"/"2" numbering here is
this footprint's own internal convention only, not a manufacturer
polarity requirement.

## What this swap does *not* include

Per the request that prompted this swap, SW5 was replaced as a
component (symbol, footprint, 3D model, and sourcing fields all
updated) but deliberately left **unwired** in the schematic — its old
3-pin connections don't map onto this part's 2-pin SPST-NO circuit, so
rewiring it to the correct nets (and updating the PCB footprint to
match, via KiCad's "Update PCB from Schematic" or "Update Footprints
from Library") is left to the project owner.
