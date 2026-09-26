---
name: bourns-pec11r-attribution
---

# PEC11R rotary encoder footprint — attribution

- **Footprint**
  (`bourns-pec11r.pretty/rotary-encoder-switched-pec11r.kicad_mod`): copied
  from DigiKey's official KiCad library
  (`digikey-footprints.pretty/Rotary_Encoder_Switched_PEC11R.kicad_mod`),
  then upgraded from its original legacy (KiCad 5-era) file format to the
  current format with `kicad-cli fp upgrade` — no geometry was changed, only
  the file syntax.
  - Upstream source: <https://github.com/Digi-Key/digikey-kicad-library>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md)
    (DigiKey's library uses the identical license text as KiCad's own).
- No 3D model is included. A community repository
  (`github.com/ubiqueIoT/rotary-encoder-PEC11R`) has one, but carries no
  license file of its own, and its README attributes the model to Adafruit
  without linking a specific licensed source — not used here for that
  reason.

## Fit note

This footprint is drawn for Bourns PEC11R‑4xxxF‑S0024 (24 pulses/rev). This
project's ENC1 is PEC11R‑**4220F‑S0012** (12 pulses/rev) — mechanically and
electrically identical footprint (the PPR digit only changes the internal
encoder disc, not the pinout or panel-mount geometry), so the same footprint
applies unmodified. Confirm this against Bourns' own PEC11R datasheet
dimensional drawing before layout if in doubt — see
`hardware/datasheets/bourns-pec11r-datasheet.pdf`.

Pad numbering in this footprint: `A`, `B`, `C` = encoder quadrature phase A,
phase B, and common; `1`, `2` = integrated pushbutton switch terminals; `3`
(appears twice, both the same pad number) = the two mechanical mounting
tabs. This project's schematic ties the mounting tabs to GND for shielding —
see [docs/hardware/pinout.md](../../../../docs/hardware/pinout.md).
