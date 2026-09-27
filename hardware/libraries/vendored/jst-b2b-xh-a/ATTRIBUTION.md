---
name: jst-b2b-xh-a-attribution
---

# JST B2B-XH-A battery connector — attribution

- **Footprint**
  (`jst-b2b-xh-a.pretty/battery-conn-jst-b2b-xh-a.kicad_mod`): copied from
  KiCad's own official library
  (`Connector_JST.pretty/JST_XH_B2B-XH-A_1x02_P2.50mm_Vertical.kicad_mod`),
  then re-saved in the current file format with `kicad-cli fp upgrade`
  (geometry unchanged). Confirmed present in the local KiCad 10.0.6
  install at `/Applications/KiCad/KiCad.app`.
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **3D model** (`3dmodels/battery-conn-jst-b2b-xh-a.step`): copied from
  KiCad's own official 3D model pack
  (`Connector_JST.3dshapes/JST_XH_B2B-XH-A_1x02_P2.50mm_Vertical.step`),
  same license as the footprint above.
- **Symbol** (`jst-b2b-xh-a.kicad_sym`): copied from KiCad's own official
  `Connector.kicad_sym` library (`Conn_01x02_Pin`), with the reference
  prefix, value, footprint link and datasheet link edited to point at
  this project's own vendored files. Pin geometry and numbering are
  otherwise unchanged. Same license as the footprint above.

## Part selection note

B2B-XH-A is JST's own generic 2-position, 2.50mm-pitch, top-entry,
through-hole pin header — the standard board-side half of the widely used
JST XH battery-connector pair (mates with an XHP-2 wire housing crimped
onto the battery leads). Confirmed as an active, stocked part at DigiKey
(part 455-B2B-XH-A-ND). This is the same connector family used on most
hobbyist LiPo/coin-cell battery packs, so commercial pre-crimped battery
leads are readily available without custom crimping.

## Polarity note

JST's own part numbering for B2B-XH-A carries no inherent polarity — pin
1 and pin 2 are just sequential pad numbers, and physical polarity is
determined entirely by which wire is crimped into which cavity of the
mating XHP-2 housing. This project's symbol labels pin 1 "+" and pin 2
"-" as a project convention (matching the polarity already used for B1's
schematic nets), not as a manufacturer-defined fact. Verify against the
actual battery pack's pre-crimped harness before wiring, since some
commercial packs reverse this convention.

## Datasheet

`hardware/datasheets/jst-xh-connector-series.pdf` — JST's own public XH
series datasheet (`eXH.pdf`), covering B2B-XH-A.
