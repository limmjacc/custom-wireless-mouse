---
name: ttc-kailh-mouse-encoder-attribution
---

# TTC/Kailh-style mouse scroll wheel encoder — attribution

- **Symbol** (`ttc-kailh-mouse-encoder.kicad_sym`, part `MOUSE_ENCODER`):
  hand-drawn generic 2-phase quadrature incremental encoder (pins A, B,
  COM). No integrated pushbutton — these parts don't have one; middle-click
  is a separate discrete switch (see below).
- **Footprint**
  (`ttc-kailh-mouse-encoder.pretty/encoder-tht-placeholder-mouse-wheel.kicad_mod`):
  **an explicit placeholder, not a verified footprint.**

## Why this is a placeholder — read before layout

Unlike every other part in this project, **no manufacturer datasheet or
mechanical drawing with pad pitch/drill dimensions is publicly available**
for this class of part. TTC and Kailh sell these mouse-specific scroll
wheel encoders (marketed as "TTC Gold/Silver encoder," "Kailh 7/8/9/10/11mm
mouse encoder") only through mod-shop retail channels (ausmodshop,
meckeys, kprepublic, ttcswitches.com), not through standard distributors
with engineering documentation (no DigiKey/Mouser/LCSC listing, no
downloadable mechanical drawing was found from TTC or Kailh directly).

What's confirmed, from the manufacturer/reseller pages themselves:
- 2-phase quadrature output (A/B), 3 total pins (A, B, COM) — no
  integrated switch.
- Shaft diameter ≈ **1.74mm** (a D-shaft), sized for standard mouse
  scroll-wheel hubs — the reason this part was chosen over the
  previous Bourns PEC11R (which has a 6mm shaft, ~3.5x too large for a
  typical mouse wheel).
- Sold in multiple body heights (5/7/8/9/10/11/12mm) to match different
  wheel diameters — the specific height needed depends on the actual
  wheel part chosen, which is a mechanical/enclosure decision outside
  this pass's scope.

What's **not** confirmed, and must be measured against the physical
part before finalizing a PCB layout:
- Exact pin pitch and pin diameter (this footprint guesses 2.54mm pitch,
  0.9mm drill — a placeholder, not a sourced value).
- Body diameter/mounting footprint on the PCB.
- Which physical pin is A vs. B vs. COM (varies by vendor/model; usually
  needs to be confirmed by testing the physical part with a multimeter
  or oscilloscope).

This mirrors how L1's inductor footprint is already flagged in
[`docs/hardware/open-items.md`](../../../../docs/hardware/open-items.md)
as a placeholder pending a real part in hand — same situation, same
honesty about the limitation, for the same reason (no public datasheet
exists to source from).

## Middle-click switch

Per the mechanical design intent, the wheel+encoder assembly sits in a
carriage that moves down as a unit when pressed, actuating a separate
discrete momentary switch mounted on the PCB beneath it. This project
reuses the same Omron D2FC-F-7N(20M) switch selected for the L/R/FN
buttons (see
[`../omron-d2fc-f-7n/ATTRIBUTION.md`](../omron-d2fc-f-7n/ATTRIBUTION.md))
for consistency, though its clearance under a real wheel carriage should
be revisited once the mechanical/enclosure design exists.

## 3D model — a real one exists for one body height, not retrievable by automated fetch

A community-uploaded STEP model for a "TTC 5mm" mouse scroll wheel
encoder exists on GrabCAD (dimensions given as 11.68 × 5.00 × 12.78mm,
consistent with this part class's ~5mm body-height variant), mirrored
on a paid CAD-drawing site. Neither is retrievable by automated fetch —
GrabCAD requires an account for file download, and the mirror site's
actual download action is behind client-side JavaScript this pass
couldn't drive. This also only covers the 5mm body-height variant;
this design hasn't picked a specific body height yet (that depends on
the actual wheel part, an open mechanical decision — see
[open-items.md](../../../../docs/hardware/open-items.md)), so even a
successfully-downloaded model would need to be swapped for the right
height once that's chosen. A human with a free GrabCAD account can
check the current state of that model here:
<https://grabcad.com/library/mouse-encoder-ttc-5mm-1>.
