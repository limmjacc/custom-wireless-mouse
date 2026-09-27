# KiCad build guidance

The schematic (`hardware/custom-wireless-mouse.kicad_sch`) is done — see
[schematic.md](schematic.md) for how it's organized and
[open-items.md](open-items.md) for what's still open before layout. This
records the order it was actually built in and the reasoning per part, for
anyone extending or re-deriving it.

1. **U1 (nRF52810) and its support circuit first** — symbol and footprint
   vendored from KiCad's own official `MCU_Nordic` / `Package_DFN_QFN`
   libraries (see [`hardware/libraries/vendored/nordic-nrf52810-qcxx/`](../../hardware/libraries/vendored/nordic-nrf52810-qcxx/)),
   rather than relying on KiCad's global library at build time — the goal is
   a project that opens identically on any KiCad 10 install, not one that
   depends on whichever library version happens to be bundled locally.
2. **U2 (PMW3610) and its charge-pump network** — the vendored symbol and
   footprint at
   [`hardware/libraries/vendored/pmw3610dm-sudu/`](../../hardware/libraries/vendored/pmw3610dm-sudu/)
   (sourced from `github.com/siderakb/pmw3610-pcb`, CERN-OHL-P licensed)
   rather than a new 16-pin DIP symbol drawn from the datasheet. The
   charge-pump values (C12/C13/C14) were confirmed by reading that project's
   actual `.kicad_sch` file directly and cross-checking against PixArt's own
   datasheet Figure 6 — see [bom.md](bom.md) for what that changed.
3. **U3 (boost regulator) and passives** — no ready-made symbol existed for
   this exact part anywhere checked, so it was hand-drawn directly from TI's
   published pinout table (a datasheet's pin function list is factual
   information, not copyrightable expression, so this is an original symbol
   rather than a copy of anyone's library). Footprint is KiCad's own
   bundled SOT-23-6, vendored in alongside it.
4. **Switches, encoder, SWD header** — same pattern throughout: a real
   footprint from KiCad's or DigiKey's official libraries where one existed
   (encoder, both switch families, the header), with a symbol either copied
   from KiCad's generic library equivalent (tactile switch, header) or
   hand-drawn where the part's pin arrangement is specific enough to need it
   (the DPDT slide switch, the encoder). Every vendor directory's
   `ATTRIBUTION.md` says which case applies and why that specific part was
   picked over its closest sibling.
5. **Battery input and protection (J2, F1, Q1)** — a JST B2B-XH-A header
   (J2) accepts a pre-crimped harness from an external battery pack, in
   series with a Littelfuse 0603L010 PPTC resettable fuse (F1, short-circuit
   protection) and a Diodes Inc. DMP2035U P-channel MOSFET (Q1, wired as a
   high-side ideal diode for reverse-polarity protection) ahead of SW1 and
   U3. Symbols, footprints, and 3D models for all three are vendored from
   KiCad's own official libraries; see each part's `ATTRIBUTION.md` under
   [`hardware/libraries/vendored/`](../../hardware/libraries/vendored/).

See [`hardware/README.md`](../../hardware/README.md) for the project's
overall library policy and folder layout.
