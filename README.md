# custom-wireless-mouse

Custom BLE wireless mouse: from-scratch PCB (KiCad) and firmware (nRF
Connect SDK / Zephyr) built to fit the mechanical envelope of the Bambu
Lab-style "Wireless Mouse Components Kit-002" (MH002), replacing its two
undocumented/discontinued ICs with fully public, sourceable parts.

See [docs/hardware/README.md](docs/hardware/README.md) for the full design
rationale, bill of materials, and net list, and
[docs/firmware/README.md](docs/firmware/README.md) for firmware scope.

## Layout

```
.
├── hardware/     KiCad 10 project — schematic, PCB layout, libraries
├── firmware/     nRF Connect SDK (Zephyr) application
├── docs/         Design documentation (hardware and firmware)
└── mechanical/   Notes on the reused kit mechanical parts
```

## Status

Schematic complete and ERC-verified (see [docs/hardware/schematic.md](docs/hardware/schematic.md)).
PCB layout not yet started, not built, not tested. No firmware logic has
been written. See each section's open-items document for what's left.

## Credits

Every vendored KiCad library part under `hardware/libraries/vendored/`
carries its own `ATTRIBUTION.md` with full sourcing detail. The two with
licenses other than KiCad's own (CC-BY-SA 4.0, used simply because most
parts were extracted from KiCad's or DigiKey's official libraries):

- The PMW3610DM-SUDU sensor's symbol and footprint, at
  [`hardware/libraries/vendored/pmw3610dm-sudu/`](hardware/libraries/vendored/pmw3610dm-sudu/),
  are from [**siderakb/pmw3610-pcb**](https://github.com/siderakb/pmw3610-pcb),
  an open-hardware PMW3610 breakout board by **siderakb**, licensed under the
  CERN Open Hardware Licence v2 — Permissive (CERN-OHL-P v2).
- The PEC11R rotary encoder footprint and the JS202011SCQN slide switch
  footprint, at
  [`hardware/libraries/vendored/bourns-pec11r/`](hardware/libraries/vendored/bourns-pec11r/)
  and
  [`hardware/libraries/vendored/ck-js202011scqn/`](hardware/libraries/vendored/ck-js202011scqn/),
  are from [**Digi-Key's official KiCad library**](https://github.com/Digi-Key/digikey-kicad-library)
  (CC-BY-SA 4.0).
