# Sensor devicetree bindings (planned)

Out-of-tree devicetree bindings go here — in particular, a
`harding,pmw3610` (or similar) binding for the driver placeholder at
[`firmware/drivers/sensor/pmw3610/`](../../../drivers/sensor/pmw3610/).
`dts_root: .` in [`firmware/zephyr/module.yml`](../../../zephyr/module.yml)
already points Zephyr's devicetree tooling at this folder.
