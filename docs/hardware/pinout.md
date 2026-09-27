# Pin assignment / net list

This reflects the actual connections drawn in `hardware/custom-wireless-mouse.kicad_sch`. Net names match the schematic's labels exactly — searching the schematic for any name below will find it.

## U1 — nRF52810-QCAA-T (32-QFN)

| Pin(s) | Signal | Net / connection |
|---|---|---|
| 9, 25, 32 | VDD | Net **+VSYS** |
| 20, 29, 33 (EP) | VSS | Net **GND** |
| 1, 21, 22, 30 | DEC1, DEC2, DEC3, DEC4 | Each to its own 100nF cap (C1–C4) to GND — not a shared net |
| 23 | XC1 | Y1 pin 1, plus C6 (12pF) to GND |
| 24 | XC2 | Y1 pin 3, plus C7 (12pF) to GND |
| 19 | ANT | Net **ANT** — PCB trace antenna, single connection point by design (see [architecture.md](architecture.md#antenna)) |
| 17 | SWDCLK | J1 pin 2 |
| 18 | SWDIO | J1 pin 3 |
| 16 | P0.21 / RESET | J1 pin 1 (~RESET) |
| 31 | DCC | **Unconnected (no-connect flag)** — internal LDO only, no DC/DC inductor used (see [architecture.md](architecture.md#single-shared-power-rail)) |
| 4 | P0.04 | Net **SPI_SCLK** → U2 pin 3 (SCLK) |
| 5 | P0.05 | Net **SPI_SDIO** → U2 pin 2 (SDIO) |
| 6 | P0.06 | Net **SPI_NCS** → U2 pin 5 (NCS) |
| 7 | P0.09 | Net **SENS_MOTION** → U2 pin 8 (MOTION) |
| 8 | P0.10 | Net **SENS_NRESET** → U2 pin 7 (NRESET) |
| 10 | P0.12 | Net **WHEEL_A** → ENC1 pin A |
| 11 | P0.14 | Net **WHEEL_B** → ENC1 pin B |
| 13 | P0.16 | Net **BTN_L** → SW2 pin 1 (COM) |
| 14 | P0.18 | Net **BTN_R** → SW3 pin 1 (COM) |
| 15 | P0.20 | Net **BTN_FN** → SW4 pin 1 (COM) |
| 26 | P0.25 | Net **BTN_SCRL** → SW5 pin 1 (COM) — wheel middle-click |
| 2, 3, 12, 27, 28 | P0.00, P0.01, P0.15, P0.28, P0.30 | **Unconnected (no-connect flags)** — reserved spare GPIOs, not used by this design |

The GPIO-to-signal assignment above is this project's own choice (the electrical design left it unconstrained — any of the 16 available GPIOs works for any of the 11 signals). Reassigning any of them is a layout-convenience decision, not a re-design — just relabel the net.

## U2 — PMW3610DM-SUDU (16-pin DIP)

| Pin | Name | Connects to |
|---|---|---|
| 1 | +VCSEL | Direct trace to pin 10, plus a PWR_FLAG (internal laser-driver node, not literally externally powered) |
| 2 | SDIO | Net **SPI_SDIO** |
| 3 | SCLK | Net **SPI_SCLK** |
| 4 | NC | Unconnected (pin is electrically typed no-connect in the symbol) |
| 5 | NCS | Net **SPI_NCS** |
| 6 | VDDIO | Net **+VSYS**, plus C10 (100nF) + C11 (1uF) to GND |
| 7 | NRESET | Net **SENS_NRESET**; R1 (10k) pull-up to +VSYS, populated |
| 8 | MOTION | Net **SENS_MOTION** |
| 9 | VCP | C12 (10uF X7R) + C13 (10nF X7R) to GND, in parallel — per PixArt datasheet Figure 6 |
| 10 | PASS_T | Direct trace to pin 1 |
| 11 | GND | Net **GND** |
| 12 | CP | C14 (100nF X7R) flying cap to pin 13 |
| 13 | CN | C14 (100nF X7R) flying cap to pin 12 |
| 14 | VDD | Net **+VSYS**, plus C8 (10uF X7R) + C9 (100nF) to GND |
| 15 | XYLASER | Direct trace to pin 16 |
| 16 | −VCSEL | Direct trace to pin 15 |

## U3 — TLV61220DBVT (SOT-23-6, adjustable boost)

| Pin | Name | Connects to |
|---|---|---|
| 6 | VBAT | Net **VBAT_SW** — SW1 pin 1, the switched output of the power path (J2 → F1 → Q1 → SW1) |
| 1 | SW | L1, other end to VOUT node |
| 2 | GND | Net **GND** |
| 3 | EN | Tied to VBAT (pin 6) — always-on, no software shutdown |
| 4 | FB | Junction of R2 (to VOUT) and R3 (to GND) |
| 5 | VOUT | Net **+VSYS**; C16 (10uF) to GND at this node; R2 also connects here |

C15 (10uF) sits directly across VBAT to GND, close to pin 6.

## SW1 — JS202011SCQN (DPDT slide switch)

Only section A is used:

| Pin | Connects to |
|---|---|
| 1 (1A) | Net **VBAT_SW** — the switched output, feeding U3 pin 6 (VBAT) and pin 3 (EN) |
| 2 (2A) | Q1 pin 3 (Drain) — the common/input, fed from the protected battery rail |
| 3 (3A) | Unconnected (no-connect flag) — the switch's other throw position |
| 4, 5, 6 (section B) | Unconnected (electrically typed no-connect in the symbol) |

## J2 — battery input (JST B2B-XH-A)

| Pin | Connects to |
|---|---|
| 1 (+) | F1 pin 1 |
| 2 (−) | Net **GND** |

## F1 — short-circuit protection (Littelfuse 0603L010 PPTC fuse)

| Pin | Connects to |
|---|---|
| 1 | J2 pin 1 (+) |
| 2 | Q1 pin 2 (Source) |

## Q1 — reverse-polarity protection (Diodes Inc. DMG2305UXQ, P-channel MOSFET)

| Pin | Name | Connects to |
|---|---|---|
| 1 | Gate | Net **GND** |
| 2 | Source | F1 pin 2 |
| 3 | Drain | SW1 pin 2 (2A) — feeds the switch, which feeds U3 |

## ENC1 — TTC/Kailh-style mouse scroll wheel encoder

No integrated pushbutton — see SW5 below for the middle-click switch
(currently unwired, pending a part swap to a lower-profile switch that
fits under the wheel).
Pin functions (A/B/COM) below are correct per the symbol; **physical
pin positions on the real part are unconfirmed** (see
[`hardware/libraries/vendored/ttc-kailh-mouse-encoder/ATTRIBUTION.md`](../../hardware/libraries/vendored/ttc-kailh-mouse-encoder/ATTRIBUTION.md)).

| Pin | Connects to |
|---|---|
| A | Net **WHEEL_A** |
| B | Net **WHEEL_B** |
| COM | Net **GND** |

## SW5 — wheel middle-click switch (Omron B3U-1000P)

**Currently unwired**, as of the 2026-09-27 part swap. SW5 previously
used the same Omron D2FC-F-7N(20M) as SW2-4, but that part's 6.5mm
body is too tall to fit underneath the scroll wheel, which mounts on
ENC1's shaft directly above SW5. Replaced with the Omron B3U-1000P
(1.6mm height, 2-pin SPST-NO) — see
[`hardware/libraries/vendored/omron-b3u-1000p/ATTRIBUTION.md`](../../hardware/libraries/vendored/omron-b3u-1000p/ATTRIBUTION.md)
for the part-selection detail.

This is a simpler 2-terminal part (no COM/NO/NC distinction like the
D2FC), and its previous connections (pin 1 → `BTN_SCRL`, pin 3 → `GND`)
were removed along with the old symbol rather than carried over blind,
since the new part's pinout isn't a 1:1 match. To restore the same
electrical behavior:

| Pin | Suggested connection |
|---|---|
| 1 | Net **BTN_SCRL** |
| 2 | Net **GND** |

Both pins are physically symmetric (per the datasheet: "No terminal
numbers are indicated on the Switches"), so either pad may take either
net. Still needs: schematic wiring, PCB re-placement under the wheel
(the new footprint is far smaller and not yet positioned), and a
physical mounting height check once the wheel/carriage mechanical
design exists (see [open-items.md](open-items.md)).

## J1 — SWD header (Samtec TSW-104-07-T-S)

A plain, unkeyed 4-pin 0.1" header — this pin order is this project's own
choice, not an external standard (there is no universal pinout for a bare
4-pin SWD header the way there is for ARM's shrouded 10-pin Cortex Debug
connector or a Tag-Connect footprint). Anyone wiring a probe to this header
should wire to the labels below, not assume a conventional SWDIO-first
ordering.

| Pin | Signal |
|---|---|
| 1 | nRESET |
| 2 | SWDCLK |
| 3 | SWDIO |
| 4 | GND |
