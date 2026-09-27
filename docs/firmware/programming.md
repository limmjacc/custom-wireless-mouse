# Programming and debugging U1

U1 (Nordic nRF52810) has no USB peripheral, so there is no DFU-over-USB
path — the only way to load firmware or debug the running application is
SWD, through J1 on the board and an external debug probe.

## J1 — SWD header pinout

J1 (Samtec TSW-104-07-T-S) is a plain, unkeyed 4-pin 0.1" header. There is
no external standard pinout for a connector like this — unlike ARM's
shrouded 10-pin Cortex Debug connector or a Tag-Connect footprint, nothing
about this part's mechanical design fixes which pin carries which signal.
The assignment below is this project's own choice, and is what's actually
drawn in the schematic and printed on the symbol/silkscreen:

| Pin | Signal |
|---|---|
| 1 | nRESET |
| 2 | SWDCLK |
| 3 | SWDIO |
| 4 | GND |

Wire a probe to these labels directly. There is no VTref/VTG sense pin on
this header, so whichever probe is used needs its target voltage set
manually (this board runs at the boosted **+VSYS** rail, ~1.89V-to-boost-set
on the low side but presented to U1 at the regulated system voltage —
confirm against [`docs/hardware/bom.md`](../hardware/bom.md) at the bench)
rather than relying on auto-detection.

## Toolchain integration

This project's firmware is built on nRF Connect SDK (Zephyr's `west`).
`west flash` supports several interchangeable runners — `nrfjprog`/`jlink`,
`pyocd`, and `openocd` — selected with `west flash -r <runner>`. This means
any CMSIS-DAP probe (which uses `pyocd` or `openocd`) or a J-Link (which
uses `jlink`/`nrfjprog`) plugs into the same build workflow without needing
a different SDK or toolchain per probe.

## Debug probe options

### ST-Link V3SET — already owned, untested against this board

An ST-Link V3SET (board silkscreen `MB1440B`) is available for this
project. SWD itself is a generic ARM protocol, so it can in principle
reach any Cortex-M target — but ST-Link V3's own firmware is documented to
perform a device-ID check and, in many reported cases, simply refuses to
attach to a non-ST target. This is a known, tracked issue (OpenOCD ticket
#275, "ST-Link v3 refuses to work with non-ST targets"), not a one-off
report. Community workarounds (specific older firmware revisions,
specific OpenOCD development builds) exist but are inconsistent and
unofficial.

Practical guidance: test it with **OpenOCD**, not ST's own
STM32CubeProgrammer/ST-Link Utility (which will almost certainly refuse a
non-ST device outright). The V3SET kit's MB1440 adapter board exposes an
STDC14 (14-pin, 1.27mm-pitch) connector, not a simple 4-pin header, so
reaching J1 needs jumper wires or a breakout from the individual
T_SWDIO/T_SWCLK/T_NRST/GND signals on that connector — a wiring task, not a
blocker on its own.

### Cheaper alternatives, if the ST-Link V3SET doesn't attach

Ranked cheapest to most reliable, all independently confirmed (not just
assumed) to work against nRF52-family targets specifically:

1. **ST-Link V2 clone (~$2, AliExpress/eBay) + OpenOCD.** Unlike V3,
   ST-Link V2 doesn't have the device-restriction firmware issue, and
   there's a specific documented walkthrough for flashing an nRF52 this
   way. Trade-off: unbranded clone hardware, OpenOCD-only (no official
   tooling).
2. **Blue Pill (STM32F103, ~$2-8) flashed with Black Magic Probe
   firmware.** Nordic's own DevZone blog has a post specifically titled
   "Flashing and debugging nRF51/52 with a cheap Black Magic Probe
   compatible SWD programmer" — this exact cheap-clone-to-nRF5x path is
   Nordic-documented. Black Magic Probe runs its own GDB server on-chip,
   so OpenOCD isn't needed in the middle.
3. **A plain Raspberry Pi Pico (~$4-5) flashed with the open-source
   `debugprobe` firmware.** Genuine, reliable hardware (not a clone),
   official Raspberry Pi Foundation firmware, confirmed working against
   nRF52 targets. Requires soldering/wiring your own SWD leads and
   flashing the firmware yourself.
4. **The official Raspberry Pi Debug Probe (~$12).** Same firmware/approach
   as above, pre-built and cased with a ready-made SWD cable — no DIY
   wiring or flashing required. Best cost-to-hassle ratio of the cheap
   options.
5. **Segger J-Link EDU Mini (~$20).** The only option with zero
   compatibility guesswork, since `nrfjprog` (nRF Connect SDK's native
   tool) is built around J-Link specifically. Licensed **non-commercial /
   educational use only.**

## Sources

- [OpenOCD ticket #275 — "ST-Link v3 refuses to work with non-ST targets"](https://sourceforge.net/p/openocd/tickets/275/)
- [STMicroelectronics Community — "Is the STLINK-V3SET locked to only ST MCUs?"](https://community.st.com/stm32-mcus-boards-and-hardware-tools-26/is-the-stlink-v3set-locked-to-only-st-mcus-28160)
- [STLINK-V3SET User Manual (UM2448)](https://www.st.com/resource/en/user_manual/um2448-stlinkv3set-debuggerprogrammer-for-stm8-and-stm32-stmicroelectronics.pdf)
- [pcbreflux — nRF52832 first steps with ST-Link V2 and OpenOCD](https://pcbreflux.blogspot.com/2016/09/nrf52832-first-steps-with-st-link-v2.html)
- [Industrial Monitor Direct — Programming nRF52810 with ST-LINK V2 via OpenOCD](https://industrialmonitordirect.com/blogs/knowledgebase/programming-nrf52810-with-st-link-v2-openocd-configuration)
- [Nordic DevZone Blog — Flashing and debugging nRF51/52 with a cheap Black Magic Probe compatible SWD programmer](https://devzone.nordicsemi.com/nordic/nordic-blog/b/blog/posts/flashing-and-debugging-nrf5152-with-a-cheap-blackm)
- [gojimmypi — Converting a Blue Pill STM32F103 to a Black Magic Probe](https://gojimmypi.github.io/BluePill-STM32F103-to-BlackMagic-Probe/)
- [jsan.ch — Programming an nRF52 with the Raspberry Pi Debug Probe](https://jsan.ch/posts/2023/09/programming-an-nrf52-with-the-raspberry-pi-debug-probe/)
- [Raspberry Pi — Debug Probe product page](https://www.raspberrypi.com/products/debug-probe/)
- [Pimoroni — PicoProbe PCB kit ($8)](https://shop.pimoroni.com/en-us/products/picoprobe-pcb-kit)
- [SEGGER — J-Link EDU Mini](https://www.segger.com/products/debug-probes/j-link/models/j-link-edu-mini/)
- [nRF Connect SDK docs — Programming an application (runner support: nrfjprog, jlink, pyocd, openocd)](https://nrfconnectdocs.nordicsemi.com/ncs/latest/nrf/app_dev/programming.html)
