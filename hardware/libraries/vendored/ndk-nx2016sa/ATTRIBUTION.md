---
name: ndk-nx2016sa-attribution
---

# NX2016SA-32MHz symbol and footprint — attribution

- **Symbol** (`ndk-nx2016sa.kicad_sym`, part `NX2016SA-32MHZ`): copied from
  KiCad's own bundled `Device.kicad_sym` library, symbol `Crystal_GND24`
  (4-pin crystal, pins 2 and 4 tied to ground/case) — an exact electrical
  match for NDK's NX2016SA pinout (pins 1/3 = crystal, pins 2/4 = GND/case,
  per the datasheet). Only the Value/Footprint/Datasheet properties were
  changed; the drawing and pin definitions are unmodified.
- **Footprint**
  (`ndk-nx2016sa.pretty/crystal-smd-2016-4pin-2.0x1.6mm.kicad_mod`) and
  **3D model** (`3dmodels/crystal-smd-2016-4pin-2.0x1.6mm.step`): copied from
  KiCad's own bundled `Crystal.pretty` / `Crystal.3dshapes` libraries
  (`Crystal_SMD_2016-4Pin_2.0x1.6mm`), which matches NX2016SA's package
  (2.0 × 1.6 × 0.45mm, 4-pad SMD) exactly.
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-symbols> /
    <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).

## Part selection note

The original audited BOM specified a crystal at 16pF load capacitance
(DigiKey SKU 644-02994-32MCT-ND). During this pass's independent re-audit,
that load capacitance was found to exceed Nordic's own documented 12pF
maximum for the nRF52810's HFXO oscillator (Nordic's reference circuitry
specifies an 8pF crystal with 12pF load caps). **NX2016SA-32MHZ-STD-CZS-5**
(NDK, 8pF, ±10ppm, 2016 package) was substituted instead — same
manufacturer, same electrical role, but matching Nordic's own reference
design's load capacitance rather than exceeding its documented maximum. See
[docs/hardware/bom.md](../../../../docs/hardware/bom.md) for the full
substitution rationale.
