# PMW3610 sensor driver (planned)

No driver source lives here yet. This directory is a placeholder for an
out-of-tree Zephyr `sensor` (or `input`) subsystem driver for the PixArt
PMW3610DM-SUDU, communicating over the SPI-like 3-wire bus described in
[docs/hardware/pinout.md](../../../../docs/hardware/pinout.md).

Prior art worth starting from rather than writing register-level access code
from scratch:

- [ZMK](https://zmk.dev/)'s own PMW3610 input driver — the PMW3610 pick was
  made in part because of this existing, working driver (see
  [docs/hardware/sensor-selection.md](../../../../docs/hardware/sensor-selection.md)).
  ZMK is itself Zephyr-based, so its driver structure (devicetree binding,
  SPI transfer sequencing, motion-interrupt handling) should port with
  modest changes.
- The register map and timing requirements in PixArt's public PMW3610
  datasheet.

## When implementing

- Add a devicetree binding under
  [`firmware/dts/bindings/sensor/`](../../../dts/bindings/sensor/) describing
  the `spi-cs`, `irq-gpios` (MOTION), and `reset-gpios` (NRESET) properties.
- Wire this directory into the build via `drivers/CMakeLists.txt` and
  `drivers/Kconfig` (currently empty, with the wiring instructions inline).
- Reference the driver from a devicetree node in
  `firmware/boards/harding/cwm_nrf52810/cwm_nrf52810.dts`, once that board's
  SPI/GPIO pin assignment is finalized (see
  [docs/hardware/open-items.md](../../../../docs/hardware/open-items.md), item 5).
