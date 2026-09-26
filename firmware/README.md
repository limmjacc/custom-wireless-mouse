# Firmware

nRF Connect SDK (Zephyr) application for the custom wireless mouse, targeting
U1 (Nordic nRF52810). This repository folder is itself a **west workspace
application repository** ("T2 star topology" in Nordic's terms) — it is not
a full Zephyr/NCS checkout. The SDK itself (`zephyr/`, `nrf/`, toolchain,
etc.) is fetched by `west` into sibling directories that are **not** part of
this git repository.

No firmware logic exists yet — see [`docs/firmware/`](../docs/firmware/) for
current scope and open items. This is scaffolding for that work.

## First-time setup

From an empty directory (outside this repository, or in a parent directory
that does not track it), following
[Nordic's application development guide](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/zephyr/develop/application/index.html):

```sh
west init -l --local /path/to/custom-wireless-mouse/firmware
west update
```

This pulls the pinned nRF Connect SDK revision (from `west.yml`) into
siblings of `firmware/` at that location, and installs Python dependencies
separately per the SDK's own instructions.

## Building

```sh
west build -b cwm_nrf52810 firmware/app
```

`cwm_nrf52810` is this project's own custom board definition (see
[`boards/harding/cwm_nrf52810/`](boards/harding/cwm_nrf52810/)) — there is no
off-the-shelf devkit that matches this PCB.

## Layout

```
firmware/
├── west.yml                          West manifest (this repo is the manifest/app repo)
├── CMakeLists.txt, Kconfig            Zephyr module entry points for this repo
├── zephyr/module.yml                 Declares this repo as a Zephyr module (board_root, dts_root)
├── app/                              The actual application
│   ├── CMakeLists.txt, Kconfig, prj.conf, VERSION
│   ├── src/                          Application source
│   └── boards/                       Per-board Kconfig/devicetree overlays
├── boards/harding/cwm_nrf52810/      Custom board definition (no upstream board matches this PCB)
├── drivers/sensor/pmw3610/           Out-of-tree PMW3610 sensor driver (not yet implemented)
├── dts/bindings/sensor/              Out-of-tree devicetree bindings
└── include/app/                      Public headers shared across app/drivers
```

## Why nRF Connect SDK / Zephyr

The sensor pick (PMW3610) has existing mainline Zephyr driver precedent via
[ZMK](https://zmk.dev/) (itself Zephyr-based), and Nordic's own SDK for the
nRF52810 is Zephyr-based — see
[docs/hardware/sensor-selection.md](../docs/hardware/sensor-selection.md).
