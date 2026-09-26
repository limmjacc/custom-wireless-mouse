# Board-specific application overlays

Per-board Kconfig fragments and devicetree overlays for this application,
named `<board>.conf` / `<board>.overlay` (e.g. `cwm_nrf52810.conf`), picked
up automatically by the Zephyr build system for the matching `-b <board>`
target. Empty for now — add overlays here as debug/release configuration
diverges from `../prj.conf`.
