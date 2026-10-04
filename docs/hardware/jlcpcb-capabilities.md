# JLCPCB manufacturing capabilities vs. this design

This board is intended to be fabricated (and possibly assembled) at
JLCPCB. This document records JLCPCB's published capability limits as of
2026-10-04 (from [jlcpcb.com/capabilities/pcb-capabilities](https://jlcpcb.com/capabilities/pcb-capabilities),
[jlcpcb.com/capabilities/pcb-assembly-capabilities](https://jlcpcb.com/capabilities/pcb-assembly-capabilities),
and [jlcpcb.com/capabilities/pcb-stencil-manufacturing](https://jlcpcb.com/capabilities/pcb-stencil-manufacturing)),
and checks this design's actual PCB file against each relevant limit.
Flex PCB and Flexible Heater capabilities are also summarized for
completeness, but don't apply to this design (rigid 2-layer FR-4 board).

## PCB fabrication capabilities (rigid, FR-4)

| Parameter | JLCPCB capability | This design | OK? |
|---|---|---|---|
| Layer count | 1–32 layers | 2 layers | ✅ |
| Board thickness | 0.4–4.5mm (1.6mm standard) | 1.6mm | ✅ |
| Board size | min 3×3mm, max 670×600mm (2-layer) | 48.1 × 60.1mm | ✅ |
| Min. track width/spacing (1oz, 2-layer) | 0.10/0.10mm (4/4 mil) | 0.2mm / 0.15mm clearance rule | ✅ (2x margin) |
| Min. drill diameter | 0.15mm (2+ layer) | Smallest THT drill used: 0.75mm (U2) | ✅ |
| Min. PTH annular ring (2-layer, 1oz) | Recommended ≥0.25mm; **absolute minimum 0.18mm** | All component (THT) pads: 0.25–0.5mm ring | ✅ |
| Min. PTH annular ring — **vias** | Same 0.18mm absolute floor applies | All 50 vias: 0.8mm pad / 0.3mm drill → 0.25mm ring | ✅ (meets JLCPCB's *recommended* value, not just the floor) |
| Min. NPTH annular ring | ≥0.45mm | No NPTH holes in this design | ✅ (n/a) |
| Min. SMD pad | 0.25×0.25mm | Smallest SMD pad (0402 passives): 0.5×0.6mm | ✅ |
| SMD pad-to-pad clearance (different nets) | 0.15mm | Board clearance rule: 0.15mm (meets, no margin) | ✅ (exact minimum, not a violation) |
| Copper weight | 1–4.5oz (2-layer) | 1oz (default, not yet explicitly set per layer) | ✅ |
| Surface finish | HASL, ENIG, OSP | Not yet selected (ordering-time choice) | — |
| Solder mask colors | Green/Purple/Red/Yellow/Blue/White/Black | Not yet selected (ordering-time choice) | — |

## Resolved finding: via annular ring was undersized for JLCPCB

Originally, every via on the board (50 total, all `0.6mm` pad diameter
/ `0.3mm` drill) had an annular ring of **0.15mm** — `(0.6 - 0.3) / 2`.
JLCPCB's own capability page states the **absolute minimum** PTH
annular ring for a standard 2-layer, 1oz-copper board is **0.18mm**,
with 0.25mm or above recommended — so 0.15mm was below even their
stated hard floor for a 2-layer board.

I first tried fixing this by blanket-resizing all 50 vias to 0.7mm and
0.8mm pad diameter via a script: both attempts broke clearance
elsewhere (69 and 86 new DRC violations respectively), since the
routing had been done tight around the original 0.6mm via size, so I
reverted both attempts rather than force it through.

**Resolved 2026-10-04:** manually reworked the routing and resized all
50 vias to `0.8mm` pad / `0.3mm` drill (**0.25mm** ring — meets
JLCPCB's *recommended* value, not just the 0.18mm floor). `kicad-cli
pcb drc` confirms no new violations were introduced (still just the 1
pre-existing antenna-keepout error — see below — and 0 unconnected
items). The project's net-class via defaults and DRC rule floor
(`min_via_annular_width`) were also updated to `0.8mm`/`0.18mm` so any
via added later via the GUI inherits JLCPCB-compliant sizing by
default.

## PCB assembly (PCBA) capabilities

| Parameter | Economic tier | Standard tier | This design | OK? |
|---|---|---|---|---|
| Min. component package | 0402 | 0201 (01005 supported) | Smallest used: 0402 (C1, C6, C7) | ✅ (meets both tiers) |
| Min. IC pin spacing | 0.4mm | 0.35mm | U1 QFN: 0.5mm pitch | ✅ (meets both tiers) |
| Min. BGA spacing | 0.5mm | 0.3mm | No BGA on this board | ✅ (n/a) |
| Assembly type | SMT + THT mixed, single/double-sided | same | Mixed SMT + THT, single-sided placement | ✅ |
| Board size (single PCB) | 10×10mm – 470×500mm | 70×70mm – 460×500mm | 48.1 × 60.1mm | ✅ (Economic tier only — below Standard tier's 70×70mm minimum) |

**Note:** at 48.1 × 60.1mm, this board is **too small for JLCPCB's
Standard PCBA tier** (which requires at least 70×70mm per board) but
fits the Economic tier (10×10mm minimum) — or it could be panelized to
meet Standard's minimum if Standard-tier assembly (e.g. for its tighter
0201/BGA support) is ever needed. Since this design doesn't use
anything below 0402 or any BGA, Economic-tier assembly capability is
sufficient either way.

## Stencil capabilities

Framework and non-framework stainless steel (304 HTA) stencils,
laser-cut, minimum aperture >0.08mm, standard thicknesses 0.10/0.12/
0.15/0.18/0.20mm at no extra cost. Nothing on this board requires a
nonstandard aperture or thickness — standard stencil ordering applies.

## Flex PCB / Flexible Heater capabilities

Not applicable — this is a rigid 2-layer FR-4 board, not a flex or
flex-rigid design, and doesn't include a flexible heater element.
Recorded here only because the capabilities page groups them together:
flex PCBs support 1–2(+) layers, 0.07–0.12mm polyimide/copper
construction, 8×12mm–234×490mm sizes; flexible heaters support
polyimide-laminated resistive layers, -70°C to 200°C (or -40 to 300°C
with high-temp PI film), 10×10mm–1200×490mm sizes.

## Everything else checked and found compliant

- Board outline, cutouts, and the "plus"-shaped board (narrow 16mm neck
  between the two switch wings) are all well above JLCPCB's 3×3mm
  absolute minimum board size in every dimension.
- All THT component holes (ENC1, J1, J2, SW2, SW3, U2) have drill/pad
  combinations giving 0.25–0.5mm annular ring — comfortably above
  JLCPCB's component-hole minimum.
- All 50 vias now meet JLCPCB's *recommended* annular ring (0.25mm),
  not just their absolute minimum — see the resolved finding above.
- Track widths used (0.2mm, 0.3mm) and the board's clearance rule
  (0.15mm) are at or above JLCPCB's 1oz/2-layer minimums, with no
  track/spacing combination anywhere near their 0.10/0.10mm floor.
- No component package below 0402 and no BGA — this board doesn't need
  JLCPCB's Standard PCBA tier for component-level reasons, only
  (optionally) for the board-size minimum noted above.
