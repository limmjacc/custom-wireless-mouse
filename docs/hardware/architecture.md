# Architecture and design rationale

## Wireless architecture: BLE, not proprietary 2.4GHz

The original kit uses a proprietary 2.4GHz link to a paired USB dongle.
Replicating that exactly would mean designing and firmware-ing two boards
(mouse + dongle) and inventing a wire protocol from scratch.

**Decision:** use Bluetooth Low Energy (BLE) HID instead. A BLE mouse pairs
directly with any host that already has Bluetooth, which is effectively all
modern PCs, laptops, and phones. This removes the dongle board entirely —
not a simplification of it, an elimination of it. If a host lacks Bluetooth,
a generic off-the-shelf BLE dongle works, no custom pairing protocol
required.

Tradeoff acknowledged: if the mechanical kit expects a small USB receiver to
live somewhere (e.g., stored in the mouse body), that storage slot goes
unused. This is an open question against the physical kit parts — see
[open items](open-items.md).

## Single shared power rail

Both major ICs need a similar, narrow low-voltage window:

- nRF52810: 1.7V–3.6V
- PMW3610DM-SUDU: VDD 1.7–2.1V (1.8V typical), VDDIO 1.7–3.3V (1.8V typical)

A single boost-regulated rail at approximately **1.8V** sits inside both
windows, so one regulator feeds the entire board. No second regulator, no
level-shifting LDO between domains — that complexity only exists in the
general-purpose breakout-board reference design (which has to support hosts
at either 1.8V or 3.3V logic). This board only has one internal logic level,
so it doesn't need that flexibility.

Both ICs' minimum operating voltage sits at or below 1.8V, and both tolerate
1.8V comfortably under their respective maximums (nRF52810 up to 3.6V,
PMW3610 up to 2.1V). Setting the boost output to ~1.8V threads both windows
with a single regulator — deliberately chosen over running two rails, which
would need a second regulator or an LDO and buys nothing here since neither
chip needs a different voltage.

## No external 32.768kHz crystal

nRF52810's low-frequency clock (used for BLE connection timing) can run off
the internal RC oscillator instead of an external 32.768kHz crystal. This
trades slightly reduced timing accuracy for one fewer crystal and two fewer
load capacitors, and frees P0.00/P0.01 as ordinary GPIOs (used for two of the
wheel-encoder or button signals — see [pinout](pinout.md)). The 32MHz crystal
(Y1, for the radio itself) is not optional — BLE's frequency tolerance
requirements make an external crystal mandatory there regardless.

## Antenna

Specified as a PCB trace (inverted-F or meander pattern) rather than a
discrete chip antenna, since a trace costs nothing extra in fabrication.
Nordic publishes reference antenna layouts for the nRF52 series; exact trace
geometry should be pulled from that reference at layout time, not invented
from scratch.

## SWD debug header

J1 exposes SWDCLK, SWDIO, RESET, and (implicitly) power/ground for
programming and debugging U1. This is the same category of interface that
consumed significant effort to locate (unsuccessfully) on the original kit's
undocumented MCU — on this board, it's exposed on purpose from the start.

## DPI control

BTN_FN (SW4) is wired as a plain GPIO input with no fixed behavior baked into
hardware. Since this board's firmware is fully custom, DPI stepping, or any
other function assigned to this button, is entirely a firmware decision —
this was the original motivating problem for the whole project, and this
design makes it a non-issue by construction.
