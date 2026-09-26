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
| 18 | SWDIO | J1 pin 1 |
| 16 | P0.21 / RESET | J1 pin 4 (~RESET) |
| 31 | DCC | **Unconnected (no-connect flag)** — internal LDO only, no DC/DC inductor used (see [architecture.md](architecture.md#single-shared-power-rail)) |
| 4 | P0.04 | Net **SPI_SCLK** → U2 pin 3 (SCLK) |
| 5 | P0.05 | Net **SPI_SDIO** → U2 pin 2 (SDIO) |
| 6 | P0.06 | Net **SPI_NCS** → U2 pin 5 (NCS) |
| 7 | P0.09 | Net **SENS_MOTION** → U2 pin 8 (MOTION) |
| 8 | P0.10 | Net **SENS_NRESET** → U2 pin 7 (NRESET) |
| 10 | P0.12 | Net **WHEEL_A** → ENC1 pin A |
| 11 | P0.14 | Net **WHEEL_B** → ENC1 pin B |
| 12 | P0.15 | Net **WHEEL_SW** → ENC1 pin 1 |
| 13 | P0.16 | Net **BTN_L** → SW2 pin 1 |
| 14 | P0.18 | Net **BTN_R** → SW3 pin 1 |
| 15 | P0.20 | Net **BTN_FN** → SW4 pin 1 |
| 2, 3, 26, 27, 28 | P0.00, P0.01, P0.25, P0.28, P0.30 | **Unconnected (no-connect flags)** — reserved spare GPIOs, not used by this design |

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
| 7 | NRESET | Net **SENS_NRESET**; R1 (10k, optional/DNI) to +VSYS if installed |
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
| 6 | VBAT | SW1 pin 1 (switched B1+) |
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
| 1 (1A) | Unconnected (no-connect flag) — the switch's other throw position |
| 2 (2A) | B1 '+' (common) |
| 3 (3A) | U3 pin 6 (VBAT) — the switched output |
| 4, 5, 6 (section B) | Unconnected (electrically typed no-connect in the symbol) |

## ENC1 — PEC11R-4220F-S0012

| Pin | Connects to |
|---|---|
| A | Net **WHEEL_A** |
| B | Net **WHEEL_B** |
| C | Net **GND** |
| 1 (switch) | Net **WHEEL_SW** |
| 2 (switch) | Net **GND** |
| 3 (mounting tabs, ×2) | Net **GND** — tied for shielding |

## J1 — SWD header (Samtec TSW-104-07-T-S)

| Pin | Signal |
|---|---|
| 1 | SWDIO |
| 2 | SWDCLK |
| 3 | GND |
| 4 | ~RESET |
