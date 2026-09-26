# Hardware design documentation

**Status:** schematic complete and ERC-verified in the KiCad project at
[`hardware/`](../../hardware/) — not yet laid out (no PCB copper), not built,
not tested. This section documents the electrical design decisions, bill of
materials, net list, and the schematic itself.

## Project goal

Design a from-scratch PCB that fits the mechanical envelope of the Bambu
Lab-style "Wireless Mouse Components Kit-002" (MH002), replacing every
component with parts that are:

- In active production (not obsolete, not NRND)
- Verifiably in stock at a named distributor, checked live rather than assumed
- Fully publicly documented (no NDA required to get a working schematic)
- As cheap and simple as the above three constraints allow

The original kit's board uses two chips that fail every one of those tests:
the optical sensor's own distributor listing has lapsed, and the
wireless/MCU chip has no public datasheet anywhere, at any price, under any
license. Rather than keep fighting that, this project designs a new board
around parts that don't have that problem.

## Documents in this section

- [Architecture and design rationale](architecture.md) — wireless link
  choice, power rail strategy, antenna, debug interface, DPI control
- [Sensor selection](sensor-selection.md) — evaluation history across three
  candidate sensors, and the fallback path if sourcing falls through
- [Bill of materials](bom.md) — full BOM across major components and support
  passives, independently re-audited with corrections
- [Pin assignment / net list](pinout.md) — complete per-pin net mapping for
  every IC, matching the schematic exactly
- [Schematic](schematic.md) — how the schematic is organized, its
  conventions, and its ERC verification result
- [KiCad build guidance](kicad-build-guide.md) — suggested build order and
  library sourcing for entering this design into KiCad
- [Open items / verification checklist](open-items.md) — what's still
  unconfirmed before this design is buildable
- [Sources](sources.md) — references consulted during the design

## Scope note

This section covers hardware only. Firmware is covered separately in
[`docs/firmware/`](../firmware/).
