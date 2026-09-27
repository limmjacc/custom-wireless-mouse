# Bill of materials

**Status:** fully audited and drawn into the schematic (`hardware/custom-wireless-mouse.kicad_sch`) — every line below is a real, individually re-verified part with a symbol and footprint in the project. See [`docs/hardware/schematic.md`](schematic.md) for how these are wired together, and [`docs/hardware/open-items.md`](open-items.md) for anything still unconfirmed.

## Major components

| Ref | Part | Package | Qty | Audit result |
|---|---|---|---|---|
| U1 | Nordic **nRF52810-QCAA-T** | 32-QFN, 5x5mm | 1 | **Verified.** LCSC (nRF52810-QCAA-R, same die/package): 3,696 in stock, $3.16 @ qty 1, Active. DigiKey lists both -T (tape) and -R7 (reel) variants; live stock count blocked by DigiKey's bot protection but the listing itself is confirmed current. Symbol/footprint vendored directly from KiCad's own official library — exact match confirmed via the datasheet URL embedded in both. |
| U2 | PixArt **PMW3610DM-SUDU** | 16-pin DIP | 1 | **Verified, non-standard channel.** Confirmed absent from DigiKey/Mouser/LCSC (checked directly, not just via search). Real and in production: full public datasheet (PMS0003-PMW3610DM-SUDU-DS-R2.4). AliExpress listings for PMW3610DM-SUDU+LM18-LSI confirmed to exist currently; live pricing not re-confirmed this pass (JS-rendered storefront blocks automated fetch). |
| LENS1 | PixArt **LM18-LSI** | optical lens | 1 | **Bundled** — sold alongside U2 by the same resellers, not separately listed. Mechanical only; no schematic connection (see U2's note on the schematic). |
| U3 | TI **TLV61220DBVT** | SOT-23-6 | 1 | **Verified.** Confirmed listed and active at DigiKey (ships-today status). Adjustable-output part, not the fixed-3.3V TLV61225. Datasheet: SLVSB53A. |
| Y1 | NDK **NX2016SA-32MHZ-STD-CZS-5** | 4-pad SMD, 2.0x1.6mm | 1 | **Verified — replaces the originally specified 16pF part.** 32MHz, **8pF load capacitance**, ±10ppm. Active, 12,615+ in stock at LCSC ($0.35 qty 1, MOQ 5). This substitution was made during this pass's audit — see the note below. |
| ENC1 | Bourns **PEC11R-4220F-S0012** | THT, vertical, 6mm flatted shaft | 1 | **Verified.** DigiKey: Active, 1,948 in stock, ~$2.02 qty 1. Datasheet confirmed at bourns.com. **Mechanical fit against the kit's wheel assembly still unverified** — needs the physical parts, not more research. Footprint vendored from DigiKey's own KiCad library (drawn for the S0024/24-PPR sibling; footprint is identical since PPR doesn't affect the pinout or panel-mount geometry). |
| SW1 | C&K **JS202011SCQN** | SMD slide switch, DPDT | 1 | **Verified — replaces the originally-unaudited generic slide switch.** Active, confirmed in stock at LCSC (41 units) and DigiKey. This is a DPDT part; only one section (pins 1‑2‑3) is used as a plain on/off power switch, the other section (4‑5‑6) is left unconnected. No suitable SPDT sibling had a ready-made KiCad footprint in either KiCad's or DigiKey's library, which is why DPDT was chosen over the simpler SPDT JS102011SCQN. |
| SW2, SW3, SW4 | Panasonic **EVQ-P7B01P** | SMD, side-actuated, 3.5x2.9mm | 3 | **Verified.** DigiKey part P16764CT-ND, confirmed Active (Panasonic's own product page agrees), real stock confirmed via a DigiKey-stock mirror (3,045 units). Datasheet confirmed at Farnell. |
| J1 | Samtec **TSW-104-07-T-S** | 4-pin, 2.54mm pitch, THT vertical | 1 | **Verified — replaces the originally-unaudited generic header.** DigiKey: 1,744 in stock, $0.27/ea. Datasheet confirmed directly from Samtec's own site. Pin assignment (this project's own choice, not tied to any external standard — see [pinout.md](pinout.md#j1--swd-header-samtec-tsw-104-07-t-s)): 1=nRESET, 2=SWDCLK, 3=SWDIO, 4=GND. |
| J2 | JST **B2B-XH-A** | 2-position, 2.50mm pitch, THT vertical | 1 | **Verified.** DigiKey 455-B2B-XH-A-ND, active/in-stock. The board-side battery input; mates with a pre-crimped JST XH wire harness on the battery pack side. Symbol/footprint/3D model vendored from KiCad's own official `Connector`/`Connector_JST` libraries. |
| F1 | Littelfuse **0603L010** | 0603 SMD, PPTC resettable fuse | 1 | **Verified.** 0.10A hold / 0.30A trip — comfortably above this design's peak draw, comfortably below a shorted cell's fault current. In series with J2's positive lead for short-circuit protection. Datasheet confirmed directly from Littelfuse. |
| Q1 | Diodes Inc. **DMP2035U** | SOT-23, P-channel MOSFET | 1 | **Verified.** V_GS(th) typ -0.7V (min -0.4V, max -1.0V per datasheet), low enough to fully enhance from a single-cell battery under typical conditions. Wired high-side (Source toward the battery, Drain toward the rest of the circuit, Gate to GND) as an ideal-diode reverse-battery-polarity protector ahead of SW1/U3. See [`hardware/libraries/vendored/diodes-dmp2035u/ATTRIBUTION.md`](../../hardware/libraries/vendored/diodes-dmp2035u/ATTRIBUTION.md) for the low-battery-voltage corner case this simple topology doesn't fully cover. |

## nRF52810 support passives

| Ref | Value | Package | Qty | Function |
|---|---|---|---|---|
| C1–C4 | 100nF | 0603 | 4 | One per DEC1–DEC4 pin per Nordic's own regulator decoupling spec — not a shared net. |
| C5 | 1uF | 0603 | 1 | VDD bulk decoupling. |
| C6, C7 | 12pF NP0, ±2% | 0402 | 2 | Y1 load caps. Matches Nordic's own published reference circuit exactly (8pF crystal, 12pF load caps) — see the note below. |

## PMW3610 support passives

Values sourced from `github.com/siderakb/pmw3610-pcb`'s real KiCad schematic (not just its BOM) and cross-checked against PixArt's own datasheet Figure 6 — this closes the charge-pump net-mapping open item from the previous pass.

| Ref | Value | Package | Qty | Function | Confidence |
|---|---|---|---|---|---|
| C8 | 10uF X7R | 0603 | 1 | VDD (pin 14) bulk decoupling. | Verified against both the open-hardware reference and PixArt's own Figure 6. |
| C9 | 100nF | 0603 | 1 | VDD (pin 14) decoupling, parallel with C8. | Same. |
| C10 | 100nF | 0603 | 1 | VDDIO (pin 6) decoupling. | Same. |
| C11 | 1uF | 0603 | 1 | VDDIO (pin 6) bulk decoupling, parallel with C10. | Same. |
| C12 | 10uF X7R | 0603 | 1 | VCP (pin 9) to GND — charge-pump reservoir, bulk. | **Per PixArt's own Figure 6**, which specifies two parallel caps here (bulk + HF) rather than the single 10nF the open-hardware board simplifies down to. This design follows the datasheet reference, not the simplified board. |
| C13 | 10nF X7R | 0603 | 1 | VCP (pin 9) to GND — charge-pump reservoir, HF, parallel with C12. | Same. |
| C14 | 100nF X7R | 0603 | 1 | CP(12)–CN(13) flying cap. | **Corrected value** — the previous pass's netlist doc guessed 10nF here; the real open-hardware schematic (and PixArt's Figure 6) both use 100nF. |
| R1 | 10k | 0603 | 1 | NRESET (pin 7) pull-up to +VSYS. Populated — matches the identical resistor (10k, same topology) in the proven `siderakb/pmw3610-pcb` reference design, whose schematic does not omit it. | Cross-checked directly against that project's `.kicad_sch` and against 19 pages of PixArt's own datasheet; no internal-pull-up claim for this pin was found in either. |

## Boost regulator support passives

Pulled directly from TI's TLV61220 datasheet (SLVSB53A) application circuit and BOM table, confirmed against the newer TLV61220A datasheet (SLVSIA2, same circuit).

| Ref | Value | Package | Qty | Audit result |
|---|---|---|---|---|
| L1 | 4.7uH | — | 1 | TI's own BOM part is **Toko 1269AS-H-4ZR7N**; Toko's inductor line was absorbed into Murata, and the current equivalent is **Murata 1269AS-H-4R7M-P2** (confirmed "ships today" at DigiKey). Schematic footprint is a placeholder (`L_1210_3225Metric`) — confirm against Murata's real package drawing at layout time, per [open items](open-items.md). |
| C15 (Cin) | 10uF, 6.3V, X5R | 0603 | 1 | Murata GRM188R60J106ME84D, confirmed in stock at DigiKey (29,362 units, $0.41/ea). |
| C16 (Cout) | 10uF, 6.3V, X5R | 0603 | 1 | Same part as C15, per TI's own reference circuit. |
| R2 (VOUT-to-FB) | **499kΩ** | 0603 | 1 | Yageo RC0603FR-07499KL, confirmed in stock (LCSC: 2,100 units). |
| R3 (FB-to-GND) | **180kΩ** | 0603 | 1 | Yageo RC0603FR-07180KL, confirmed in stock (LCSC: 260,500 units). |

### Boost output voltage

VOUT = VFB × (1 + R2/R3), VFB typical 500mV. With R3 = 180kΩ, R2 = 499kΩ: **VOUT ≈ 1.89V** — comfortably clear of TLV61220's 1.8V absolute-minimum floor (the previous pass's plan sat exactly on that floor with no margin) and clear of U2's 2.1V ceiling.

## Corrections made during this pass's independent re-audit

Two real design issues were caught and fixed, not just re-confirmed:

1. **Crystal load capacitance.** The previously specified crystal (16pF load capacitance) exceeds Nordic's own documented 12pF maximum for the nRF52810's HFXO oscillator (Nordic's reference circuitry uses an 8pF crystal with 12pF load caps). Substituted **NDK NX2016SA-32MHZ-STD-CZS-5** (8pF, ±10ppm) — same electrical role, now matching Nordic's own reference exactly, with a smaller footprint (2.0×1.6mm vs. 3.2×2.5mm) as a side benefit.
2. **Charge-pump flying-cap value.** The prior pass's netlist inferred 10nF for the CP–CN flying cap (C14) by guessing at pin-function names. This pass read the actual KiCad schematic file (not just the BOM) from the open-hardware reference project and cross-checked it against PixArt's own datasheet Figure 6: the real value is **100nF**, and the VCP reservoir (C12/13) uses two parallel caps (10uF + 10nF) per PixArt's reference, not the single 10nF the open-hardware board simplifies down to.

Both are reflected in the schematic and in the tables above.
