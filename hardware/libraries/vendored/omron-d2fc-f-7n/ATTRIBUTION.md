---
name: omron-d2fc-f-7n-attribution
---

# Omron D2FC-F-7N(20M) micro switch — attribution

- **Symbol** (`omron-d2fc-f-7n.kicad_sym`): hand-drawn, generic SPDT
  snap-action switch graphic with pins labeled per Omron's own "Contact
  Form" diagram (COM, NO, NC).
- **Footprint** (`omron-d2fc-f-7n.pretty/switch-tht-omron-d2fc-f-7n.kicad_mod`):
  hand-drawn from Omron's own published mechanical drawing for the D2F
  family's "Pin Plunger, PCB terminals (Straight)" variant: **12.8 × 5.8mm
  body**, **3 through-hole pins at 5.08mm pitch**. Pad drill/diameter
  (1.0mm drill, 2.0mm pad) is a reasonable convention for this lead gauge,
  not a value printed in the datasheet itself — confirm against the
  physical part before final layout.

## Datasheet note — important limitation, stated plainly

`hardware/datasheets/omron-d2f-family-datasheet.pdf` is Omron's **general
D2F catalog datasheet** (downloaded directly from omronfs.omron.com), not
a part-specific sheet for D2FC-F-7N(20M). Omron sells the D2FC line
(the mouse-industry variant, distinguished from the general-purpose D2F
line by the extra "C") through a separate, semi-custom program, and its
own datasheet (hosted behind Mouser's document server) could not be
fetched directly during this pass.

The body dimensions used for this footprint (12.8 × 5.8mm, 5.08mm pin
pitch) are the general D2F family's published "Low Operating Force"
pin-plunger variant (0.74N / 75gf max operating force — matching
D2FC-F-7N(20M)'s known 75gf spec exactly) and are corroborated by every
distributor/community source checked (DigiKey's own D2FC-F-7N(20M)
listing, and the entire Kailh GM-series/Huano/TTC clone ecosystem, which
all share this identical body). This is a well-corroborated cross-check,
not a guess, but it is not the same as reading D2FC-F-7N(20M)'s own
datasheet page directly — worth knowing if a real part in hand ever
disagrees with this footprint.

## Part selection note

This part (or its Kailh GM-series/Huano/TTC clones, all sharing the
identical 12.8×5.8×6.5mm through-hole body) is the de-facto industry
standard for DIY/mouse-modding swap-in switches — confirmed via Omron's
own D2FC product page, DigiKey's stocked listing, and multiple
mod-market vendors (KPrepublic, Chosfox, Meckeys) selling directly
interchangeable parts in this same footprint. This replaces the
previous Panasonic EVQ-P7B01P selection, which was a fundamentally
different switch class (SMD metal-dome tactile, 3.5×2.9mm, fixed 2
terminals) — mechanically incompatible with the DIY mouse-switch
aftermarket the board is meant to accept, not just a smaller version of
the same idea. A 2-pin switch (e.g., Kailh GM 2.0) populates the COM and
NO pads only, leaving the NC pad as an unconnected through-hole — no
separate footprint is needed for the 2-pin vs. 3-pin case.

## Sourcing note (2026-09-27)

DigiKey.ca (SKU 39-D2FC-F-7N(20M)-ND,
<https://www.digikey.ca/en/products/detail/omron-electronics-inc-emc-div/D2FC-F-7N-20M/20484121>)
lists this part as **manufacturer-discontinued** — its own listing
states it will no longer be stocked once depleted, with 4,658 units
remaining at the time of this check. That's enough for a small-batch
build, not a long-term production source. No same-footprint active
replacement was found at DigiKey or Mouser during this pass; if this
stock runs out before a future build, the mod-market ecosystem
described above (Kailh GM-series, Huano, TTC — all sharing this
identical body) is the fallback channel. See
[open-items.md](../../../../docs/hardware/open-items.md) item 13.

## 3D model

`3dmodels/switch-tht-omron-d2fc-f-7n.step` is a community-uploaded
model of the real part from GrabCAD
(<https://grabcad.com/library/omron-d2fc-f-7n-1>), downloaded manually
(GrabCAD requires an account for file download, which blocks automated
fetching) and placed here unmodified. That upload includes two
variants — straight-lead and a bent/formed-lead version; the
**straight-lead** variant was used here, matching this footprint's
straight-through-hole pin arrangement.

**Orientation note (2026-09-27):** this file's own STEP data places the
switch body's long axis (with its 3 pins) along a different local axis
than the footprint expects, and its own origin sits at one corner of
the body rather than the center. The footprint's `(model ...)` block
applies a 90° rotation about Z plus a matching `(-6.4, 2.9, 0)` offset
to correct both — confirmed by rendering all instances (at the time,
SW2, SW3, SW4, SW5, at different board rotations) with `kicad-cli pcb
render` and checking each sits flat and centered on its 3 THT pads.
(SW4 was later removed and SW5 later swapped to a different, lower-
profile part — this footprint is now only used by SW2 and SW3.)
