---
name: diodes-dmp2035u-attribution
---

# Diodes Inc. DMP2035U P-channel MOSFET — attribution

- **Footprint** (`diodes-dmp2035u.pretty/sot-23-dmp2035u.kicad_mod`): copied from
  KiCad's own official library (`Package_TO_SOT_SMD.pretty/SOT-23.kicad_mod`),
  then re-saved in the current file format with `kicad-cli fp upgrade`
  (geometry unchanged).
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **3D model** (`3dmodels/sot-23-dmp2035u.step`): copied from KiCad's own
  official 3D model pack (`Package_TO_SOT_SMD.3dshapes/SOT-23.step`), same
  license as the footprint above.
- **Symbol** (`diodes-dmp2035u.kicad_sym`): hand-drawn, reusing the body
  graphic from KiCad's own generic `Device:Q_PMOS` symbol (same license as
  above), with pin numbers changed from lettered (`G`/`S`/`D`) to numeric
  (`1`/`2`/`3`) so they match this footprint's numeric pad numbers, per the
  real DMP2035U SOT-23 pinout confirmed from its datasheet (page 1, package
  top view): pin 1 = Gate, pin 2 = Source, pin 3 = Drain (the lone pin on
  the side opposite the Gate/Source pair).

## Part selection and verification

Datasheet: `hardware/datasheets/diodes-dmp2035u-datasheet.pdf` (Diodes Inc.,
document DS31830 Rev. 11, June 2025), downloaded directly from
diodes.com and read in full before selection.

Selected for reverse-battery protection ahead of the TLV61220 boost
regulator (which needs only 0.7V to start up — a plain series diode's
0.3-0.7V drop would eat most of that margin on an aging AA cell). Key
verified specs from the datasheet's Electrical Characteristics table:

- V_GS(th): min -0.4V, **typ -0.7V**, max -1.0V (page 2).
- R_DS(on): 23/30/41 mΩ typ (35/45/62 mΩ max) at V_GS = -4.5V/-2.5V/-1.8V
  respectively, I_D = -2A to -4A (page 2) — R_DS(on) is not characterized
  below V_GS = -1.8V in the table, but Fig. 1 (page 3) shows the channel
  is already conducting several amps at V_GS = -1.5V, far beyond this
  design's actual load (tens of mA).
- Continuous drain current: -4.9A at 25°C (page 2) — enormous headroom
  over this design's actual current.
- Package: SOT-23, active/stocked part (Diodes Inc., ordering codes
  DMP2035U-7 / DMP2035U-13).

**Known limitation, stated plainly rather than glossed over**: at the
worst-case manufacturing corner (V_GS(th) = -1.0V max) and a fully
discharged single AA cell (~0.9V, per TI application report SLVA315 on
this exact single-cell class of problem), the gate overdrive could be as
little as 0 V, meaning this part is not guaranteed to fully saturate at
the extreme low end of battery discharge. This is an inherent limitation
of a simple single-MOSFET "ideal diode" at single-cell voltages — TI's
note describes a more elaborate circuit (deriving gate drive from a
boost converter's own internal auxiliary rail once it starts up) that
avoids this, but that trick requires a boost IC with an exposed
low-threshold auxiliary supply pin, which the TLV61220 used in this
design does not have. In practice this only affects the very last
sliver of battery capacity near end-of-life, at typical (non-worst-case)
device parameters and room temperature the part turns on comfortably
well above 0.9V (V_GS(th) typ -0.7V, see Fig. 7 in the datasheet).

## Polarity / circuit topology note

Wired as a high-side "ideal diode": Source toward the battery/connector
side, Drain toward the protected downstream circuit, Gate tied to GND.
On correct polarity the body diode conducts momentarily until the
channel turns on (near-zero R_DS(on) drop); on reversed polarity the
source node goes negative relative to the grounded gate, keeping the
channel off and blocking current.
