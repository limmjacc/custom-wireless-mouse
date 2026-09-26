# cwm_nrf52810

Zephyr board definition for the custom wireless mouse PCB, built around U1
(Nordic nRF52810, 32-QFN 5x5mm package). Vendor namespace `harding`.

This board has no upstream Zephyr entry — it is fully custom and lives only
in this repository. It targets the SoC only (`SOC_NRF52810_QFAA`); it does
not assume the presence of a J-Link debug probe on the final product, only
during bring-up via the SWD header (J1, see
[docs/hardware/pinout.md](../../../../docs/hardware/pinout.md)).

Several devicetree nodes (SPI bus to the PMW3610 sensor, GPIO button/encoder
inputs) are intentionally left out of `cwm_nrf52810.dts` for now — the exact
P0.xx pin for each signal is an open layout decision, tracked in
[docs/hardware/open-items.md](../../../../docs/hardware/open-items.md), item 5.
Fill in `cwm_nrf52810-pinctrl.dtsi` and the corresponding nodes in
`cwm_nrf52810.dts` once those pins are fixed at layout time.
