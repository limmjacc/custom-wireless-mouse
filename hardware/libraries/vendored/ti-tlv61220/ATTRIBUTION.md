---
name: ti-tlv61220-attribution
---

# TLV61220DBVT symbol and footprint — attribution

- **Symbol** (`ti-tlv61220.kicad_sym`): hand-drawn for this project directly
  from the pin-function table in Texas Instruments' public TLV61220
  datasheet (SLVSB53A), section 7 ("Pin Configuration and Functions") —
  `https://www.ti.com/lit/ds/symlink/tlv61220.pdf`. A datasheet's pinout
  (which pin number does what) is factual information, not copyrightable
  expression, so this is an original symbol rather than a copy of anyone
  else's library file. Pin 1=SW, 2=GND, 3=EN, 4=FB, 5=VOUT, 6=VBAT — TI's own
  pin name for the supply input is "VBAT", not "VIN".
- **Footprint** (`ti-tlv61220.pretty/sot-23-6.kicad_mod`) and **3D model**
  (`3dmodels/sot-23-6.step`): copied from KiCad's own bundled official
  library (`Package_TO_SOT_SMD.pretty` / `.3dshapes`), which matches TI's
  DBV package (JEDEC MO-178 Variant AB, standard SOT-23-6) exactly.
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — see
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md)
    for the full text (identical license, not duplicated per-directory).
