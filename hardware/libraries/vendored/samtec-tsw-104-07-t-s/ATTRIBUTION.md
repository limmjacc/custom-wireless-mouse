---
name: samtec-tsw-104-07-t-s-attribution
---

# SWD header (Samtec TSW-104-07-T-S) symbol/footprint — attribution

- **Symbol** (`samtec-tsw-104-07-t-s.kicad_sym`, part `SWD_HEADER`): copied
  from KiCad's own bundled `Connector_Generic.kicad_sym`, symbol
  `Conn_01x04` — a generic 4-pin single-row connector. Only the pin *names*
  were changed, from generic `Pin_1..4` to this design's actual SWD signal
  names (pin 1 = nRESET, pin 2 = SWDCLK, pin 3 = SWDIO, pin 4 = GND — see
  [docs/hardware/pinout.md](../../../../docs/hardware/pinout.md)); pin
  numbers, the symbol drawing, and electrical types are unmodified.
- **Footprint**
  (`samtec-tsw-104-07-t-s.pretty/pinheader-1x04-p2.54mm-vertical.kicad_mod`)
  and **3D model** (`3dmodels/pinheader-1x04-p2.54mm-vertical.step`): copied
  from KiCad's own bundled `Connector_PinHeader_2.54mm.pretty` /
  `.3dshapes` libraries — a generic 1×4, 2.54mm-pitch, vertical THT header,
  which is exactly Samtec's TSW-104-07-T-S mechanical footprint (a standard
  0.025" square-post header on 0.1" pitch).
  - Upstream source: <https://gitlab.com/kicad/libraries/kicad-symbols> /
    <https://gitlab.com/kicad/libraries/kicad-footprints>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).

## Pin assignment note

This design assigns pin 1 = nRESET, pin 2 = SWDCLK, pin 3 = SWDIO, pin 4 =
GND. This is a plain, unkeyed 4-pin 0.1" header — there is no external
standard pinout for a connector like this (unlike, say, ARM's shrouded
10-pin Cortex Debug connector or a Tag-Connect footprint), so this order is
purely this project's own choice. Wire to a probe using these pin labels
directly rather than assuming a conventional SWDIO-first ordering.
