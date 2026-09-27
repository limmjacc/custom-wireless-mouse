---
name: littelfuse-0603l010-attribution
---

# Littelfuse 0603L010 PPTC resettable fuse — attribution

- **Footprint**
  (`littelfuse-0603l010.pretty/fuse-0603-littelfuse-0603l010.kicad_mod`):
  copied from KiCad's own official library
  (`Fuse.pretty/Fuse_0603_1608Metric.kicad_mod`), then re-saved in the
  current file format with `kicad-cli fp upgrade` (geometry unchanged).
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **3D model** (`3dmodels/fuse-0603-littelfuse-0603l010.step`): copied from
  KiCad's own official 3D model pack (`Fuse.3dshapes/Fuse_0603_1608Metric.step`),
  same license as the footprint above.
- **Symbol** (`littelfuse-0603l010.kicad_sym`): copied from KiCad's own
  official `Device.kicad_sym` library (`Fuse`), same license as above,
  with only the reference/value/footprint/datasheet properties edited to
  point at this project's own vendored files.

## Part selection and verification

Datasheet: `hardware/datasheets/littelfuse-0603l-series-datasheet.pdf`
(Littelfuse, PolySwitch Resettable PPTC Datasheet, revised GD.01/02/23),
downloaded directly and read in full before selection.

Selected part: **0603L010** (I_hold = 0.10A, I_trip = 0.30A, V_max =
15Vdc, I_max = 40A), from the 0603L series' full electrical
characteristics table (datasheet page 1). Placed in series with the
battery's positive lead for short-circuit protection.

Sizing rationale, cross-referenced against this design's own audited
current draw: the system's worst-case measured/estimated peak is ~28mA
(sensor + radio burst, see prior battery-life analysis in
[docs/hardware/bom.md](../../../../docs/hardware/bom.md) discussion),
against which 100mA hold current gives roughly 3.5x margin (and even at
+40°C derating, the datasheet's temperature-rerating table (page 2)
still gives 80mA hold — comfortably above 28mA), so normal operation
should never approach a nuisance trip, while the 300mA trip threshold
opens well below a typical AA cell's short-circuit current (commonly on
the order of several hundred mA to a few amps).

The smaller 0603L004 (0.04A hold) was considered and rejected: its
40mA hold current gives less than 1.5x margin over the 28mA peak (real
risk of nuisance tripping under normal use), and its minimum
un-tripped resistance (4Ω per the datasheet) would impose a much larger
voltage drop than 0603L010's (0.9Ω min) at this design's currents.
