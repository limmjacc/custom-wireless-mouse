# Firmware documentation

**Status:** scaffolding only. No firmware logic has been written — see
[`firmware/`](../../firmware/) for the current source layout.

## Scope

Firmware for U1 (Nordic nRF52810), built on the nRF Connect SDK (Zephyr).
Responsibilities, once implemented:

- BLE HID mouse profile (see
  [docs/hardware/architecture.md](../hardware/architecture.md#wireless-architecture-ble-not-proprietary-24ghz)
  for why BLE HID rather than a proprietary 2.4GHz link)
- PMW3610 sensor driver and motion reporting (see
  [`firmware/drivers/sensor/pmw3610/`](../../firmware/drivers/sensor/pmw3610/))
- Button (left/right/function) and rotary-encoder scroll-wheel input
- DPI stepping behavior on the function button — a firmware-only decision by
  design, see
  [docs/hardware/architecture.md](../hardware/architecture.md#dpi-control)
- Power management for single-AA-cell operation

See [programming.md](programming.md) for how U1 gets flashed and debugged —
J1's SWD pinout, toolchain integration (`west flash` runners), and a cost
comparison of debug probe options.

## Open items

- GPIO pin assignment for all sensor/button/encoder signals is not yet fixed
  (hardware layout decision) — see
  [docs/hardware/open-items.md](../hardware/open-items.md), item 5. The
  board definition at
  [`firmware/boards/harding/cwm_nrf52810/`](../../firmware/boards/harding/cwm_nrf52810/)
  cannot gain real SPI/GPIO devicetree nodes until that's resolved.
- PMW3610 driver: to be adapted from ZMK's existing driver rather than
  written from scratch — see
  [`firmware/drivers/sensor/pmw3610/README.md`](../../firmware/drivers/sensor/pmw3610/README.md).
