---
name: diodes-dmg2305uxq-attribution
---

# Diodes Inc. DMG2305UXQ P-channel MOSFET — attribution

- **Footprint** (`diodes-dmg2305uxq.pretty/sot-23-dmg2305uxq.kicad_mod`): copied from
  KiCad's own official library (`Package_TO_SOT_SMD.pretty/SOT-23.kicad_mod`),
  then re-saved in the current file format with `kicad-cli fp upgrade`
  (geometry unchanged).
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **3D model** (`3dmodels/sot-23-dmg2305uxq.step`): copied from KiCad's own
  official 3D model pack (`Package_TO_SOT_SMD.3dshapes/SOT-23.step`), same
  license as the footprint above.
- **Symbol** (`diodes-dmg2305uxq.kicad_sym`): hand-drawn, reusing the body
  graphic from KiCad's own generic `Device:Q_PMOS` symbol (same license as
  above), with pin numbers set to numeric (`1`/`2`/`3`) matching this
  footprint's numeric pad numbers, per the real SOT-23 pinout confirmed
  from the datasheet (page 1, package top view): pin 1 = Gate, pin 2 =
  Source, pin 3 = Drain (the lone pin on the side opposite the
  Gate/Source pair) — an identical convention to the previously-specified
  DMP2035U, which this part replaces (see "Part history" below).

## Part selection and verification

Datasheet: `hardware/datasheets/diodes-dmg2305uxq-datasheet.pdf` (Diodes
Inc., document DS38238 Rev. 3, September 2018), downloaded directly from
diodes.com and read in full before selection.

Selected for reverse-battery protection ahead of the TLV61220 boost
regulator (which needs only 0.7V to start up — a plain series diode's
0.3-0.7V drop would eat most of that margin on an aging single cell).
Key verified specs from the datasheet's Electrical Characteristics table:

- V_GS(th): min -0.5V, **typ (not stated directly, but consistent with
  Fig. 7's ~-0.8V room-temperature reading)**, **max -0.9V** (page 2) —
  a tighter (lower-magnitude) worst-case threshold than the part this
  replaces.
- R_DS(on): 40/52 mΩ typ/max at V_GS = -4.5V, I_D = -4.2A (page 2) —
  enormous headroom over this design's actual load (tens of mA).
- Continuous drain current: -4.2A at 25°C (page 2).
- Package: SOT-23, AEC-Q101 automotive-qualified, Active/stocked part
  (Diodes Inc., ordering codes DMG2305UXQ-7 / DMG2305UXQ-13).

**Corner-case note, carried over and improved**: at the worst-case
manufacturing corner (V_GS(th) = -0.9V max) and a fully discharged
single AA cell (~0.9V, per TI application report SLVA315 on this exact
single-cell class of problem), the gate overdrive could still be
marginal — this is an inherent limitation of a simple single-MOSFET
"ideal diode" at single-cell voltages, not specific to this part. What
changed versus the previous part is that -0.9V max is measurably better
than DMP2035U's -1.0V max, narrowing (not widening) this corner case.
TI's note describes a more elaborate circuit (deriving gate drive from
a boost converter's own internal auxiliary rail once it starts up) that
avoids the issue entirely, but that trick requires a boost IC with an
exposed low-threshold auxiliary supply pin, which the TLV61220 used in
this design does not have.

## Part history — replaces DMP2035U (2026-09-27)

This design previously specified Diodes Inc. **DMP2035U-7**
(V_GS(th) max -1.0V), which remains a valid, Active part but was out of
stock at both DigiKey.ca and Mouser with a ~40-week manufacturer lead
time at the time of this project's full sourcing audit. DMG2305UXQ-7
was identified as a genuine improvement rather than a compromise:

- **Better spec, not just an in-stock swap**: V_GS(th) max -0.9V vs.
  DMP2035U's -1.0V — this narrows the exact low-battery corner case
  described above, rather than widening it (an alternative that was
  considered and rejected, AO3401A, has V_GS(th) max -1.3V — worse).
- **Identical pinout**: SOT-23-3, Gate-Source-Drain in the same
  physical arrangement, so no footprint or schematic rewiring was
  needed — this was a pure component substitution.
- **Confirmed in stock** at DigiKey.ca (17 units at the time of check —
  thin, but more than sufficient for hobbyist/small-batch quantities;
  re-check before a larger production run) under SKU
  31-DMG2305UXQ-7CT-ND.
- **AEC-Q101 automotive-qualified** — not a requirement for this
  design, but not a downside either.

The library folder, symbol, footprint, and datasheet were all renamed
from `diodes-dmp2035u`/`DMP2035U` to `diodes-dmg2305uxq`/`DMG2305UXQ`
to match; `hardware/sym-lib-table` and `hardware/fp-lib-table` were
updated accordingly. ERC was re-run clean (0 violations) after the swap.

## Polarity / circuit topology note

Wired as a high-side "ideal diode": Source toward the battery/connector
side, Drain toward the protected downstream circuit, Gate tied to GND.
On correct polarity the body diode conducts momentarily until the
channel turns on (near-zero R_DS(on) drop); on reversed polarity the
source node goes negative relative to the grounded gate, keeping the
channel off and blocking current.
