---
name: panasonic-evq-p7b01p-attribution
---

# EVQ-P7B01P tactile switch symbol/footprint — attribution

- **Symbol** (`panasonic-evq-p7b01p.kicad_sym`): copied from KiCad's own
  bundled `Switch.kicad_sym`, generic symbol `SW_SPST` (simple 2-pin
  switch) — an exact electrical match for a single-pole tactile switch.
  Only the Value/Footprint/Datasheet properties and internal symbol names
  were changed.
- **Footprint**
  (`panasonic-evq-p7b01p.pretty/sw-spst-evqp7-side-actuated.kicad_mod`) and
  **3D model** (`3dmodels/sw-spst-evqp7-side-actuated.step`): copied from
  KiCad's own bundled `Button_Switch_SMD.pretty` / `.3dshapes` libraries
  (`SW_SPST_EVQP7A`).
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-symbols> /
    <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).

## Fit note

KiCad ships footprints for the EVQ-P7**A** and EVQ-P7**C** actuator-height
variants of this family, not EVQ-P7**B** specifically. Panasonic's EVQ-P7
series shares one PCB land pattern across the A/B/C suffix (side-actuated,
3.5×2.9mm body, per the family datasheet at
`sw_lt_eng_3529s_side.pdf`) — the suffix letter changes actuator/nub
geometry, not the solder pads. `SW_SPST_EVQP7A` was used as the closest
available match; this has not been independently re-verified pad-by-pad
against Panasonic's EVQ-P7B01P-specific dimensional drawing before layout.
