# Mechanical

This PCB is designed to fit the mechanical envelope of the Bambu Lab-style
"Wireless Mouse Components Kit-002" (MH002) — see
[docs/hardware/README.md](../docs/hardware/README.md#project-goal). No
mechanical design files (shell, button caps, wheel housing) are original to
this project; the kit's existing mechanical parts are reused.

## Open questions against the physical kit

- **USB dongle storage slot.** If the kit's shell has a slot for storing a
  small USB receiver, that slot goes unused under this board's BLE-only
  architecture (no dongle). Not yet confirmed against the physical parts —
  see [docs/hardware/open-items.md](../docs/hardware/open-items.md).
- **Encoder mechanical fit.** ENC1's footprint and shaft/detent geometry need
  confirming against the kit's actual wheel assembly — this requires the
  physical parts in hand, not further research.

Add measurements, photos, or a 3D scan of the kit's shell/battery
compartment here as they're captured, to inform the PCB outline in
[`hardware/`](../hardware/).
