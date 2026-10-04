# Bill of materials

**Status:** fully audited against real, currently-orderable distributor listings — every line below is a specific manufacturer part number with a live DigiKey.ca (or, for the two parts absent from standard distribution, a named reseller) listing, confirmed in stock or on a known restock date as of **2026-09-27**. Every part also has a symbol, footprint, and 3D model in the project. See [`docs/hardware/schematic.md`](schematic.md) for how these are wired together, and [`docs/hardware/open-items.md`](open-items.md) for anything still unconfirmed.

Sourcing was checked against Canadian-facing distributors — primarily DigiKey.ca, with Mouser.ca as a secondary source where DigiKey.ca data was unavailable — since this board is built and ordered from Alberta, Canada. Prices below are DigiKey.ca CAD list price at low quantity (1-25 pcs) unless noted; re-check before placing a purchase order, since stock and pricing move week to week.

## Major components

**Note:** SW4 (the dedicated function/DPI button) was removed from the design during PCB layout — the board didn't have room for a fourth button footprint once routing was underway. See [open-items.md](open-items.md) and [architecture.md](architecture.md#dpi-control).

| Ref | Part | Manufacturer | Package | Qty | Distributor / SKU | Price (CAD) | Stock status |
|---|---|---|---|---|---|---|---|
| U1 | **nRF52810-QCAA-T** | Nordic Semiconductor | 32-QFN, 5x5mm, 0.5mm pitch | 1 | DigiKey.ca [4823-NRF52810-QCAA-T-ND](https://www.digikey.ca/en/products/detail/nordic-semiconductor-asa/NRF52810-QCAA-T/7725411) | $5.02 | **Active, in stock** (8,643 units) |
| U2 | **PMW3610DM-SUDU** (+ LM18-LSI lens) | PixArt Imaging | 16-pin DIP | 1 | [AliExpress, item 1005007118767775](https://de.aliexpress.com/item/1005007118767775.html) — "New and Original PMW3610DM-SUDU + LM18-LSI DIP" | ~CAD $8.64 (per your own listing check) | Confirmed live listing, ships from a specialty reseller — this part is genuinely absent from DigiKey/Mouser/LCSC, so this is the correct purchasing channel, not a fallback |
| LENS1 | **LM18-LSI** | PixArt Imaging | optical lens | 1 | Bundled with the U2 listing above, not sold separately | — | Same listing as U2 |
| U3 | **TLV61220DBVT** | Texas Instruments | SOT-23-6 | 1 | DigiKey.ca [296-43576-1-ND](https://www.digikey.ca/en/products/detail/texas-instruments/TLV61220DBVT/3588875) | $2.06 | **Active, in stock** (1,612 units) |
| Y1 | **NX2016SA-32MHZ-EXS00A-CS06654** | NDK America | 4-pad SMD, 2.0x1.6mm | 1 | DigiKey.ca [644-CS06654-32MCT-ND](https://www.digikey.ca/en/products/detail/ndk-america-inc/NX2016SA-32MHZ-EXS00A-CS06654/9172029) | $0.76 | **Active, in stock** (102,352 units). 32MHz, 8pF load capacitance, ±10ppm tolerance — matches Nordic's own reference circuit. This is the full, correct orderable part number for the generic "NX2016SA-32MHZ" family designation. |
| ENC1 | TTC/Kailh-style **mouse scroll wheel encoder** | TTC or Kailh (mod-market) | THT, ~1.74mm D-shaft, body height TBD (5-14mm depending on wheel) | 1 | [Ausmodshop — Kailh mouse scroll wheel encoder](https://ausmodshop.com/products/kailh-mouse-scroll-wheel-encoder) ($4.95 AUD, 7/8/10/11/12/13/14mm in stock) or [TTC Gold variant](https://ausmodshop.com/products/ttc-gold-mouse-scroll-wheel-encoder) ($5.95 AUD, 7/8/9mm in stock) | ~$4-6 AUD | Confirmed live stock at time of writing. No manufacturer datasheet exists for this part class (mod-market only), so footprint remains an unconfirmed placeholder — see [open items](open-items.md). No standard-distributor substitute exists at this shaft diameter (checked Bourns PEC11/12 and Alps EC11, both ~6mm shafts). |
| SW1 | **JS202011SCQN** | C&K (Littelfuse) | SMD slide switch, DPDT | 1 | DigiKey.ca [401-2002-1-ND](https://www.digikey.ca/en/products/detail/c-k/JS202011SCQN/1640098) | $1.28 | **Active, in stock** (100,379 units) |
| SW2, SW3 | **D2FC-F-7N(20M)** | Omron | THT, 12.8x5.8x6.5mm SPDT snap-action | 2 | DigiKey.ca [39-D2FC-F-7N(20M)-ND](https://www.digikey.ca/en/products/detail/omron-electronics-inc-emc-div/D2FC-F-7N-20M/20484121) | $0.86 | **Manufacturer-discontinued (EOL)** — DigiKey's own listing states it will no longer be stocked once depleted. 4,658 units remain at DigiKey.ca as of this pass; sufficient for a small-batch build, but buy now rather than treat this as a long-term-available part. No same-footprint active replacement was found at DigiKey/Mouser — this exact body/pin layout is otherwise a mod-market-only part (Kailh/Huano clones). |
| SW5 | **B3U-1000P** | Omron | SMD, 3.0x2.5mm, 1.6mm height, SPST-NO tactile | 1 | DigiKey.ca [SW1020CT-ND](https://www.digikey.ca/en/products/detail/omron-electronics-inc-emc-div/B3U-1000P/1534338) | $1.83 | **Active, in stock** (129,510 units). Middle-click switch for the scroll wheel — deliberately a different part from SW2-4: the D2FC-F-7N(20M)'s 6.5mm body doesn't fit under the scroll wheel, which mounts on ENC1's shaft directly above SW5. Swapped 2026-09-27 for this ultra-low-profile part instead — see [`hardware/libraries/vendored/omron-b3u-1000p/ATTRIBUTION.md`](../../hardware/libraries/vendored/omron-b3u-1000p/ATTRIBUTION.md) for the full candidate comparison. 2-pin SPST (no COM/NO/NC distinction like the D2FC) — rewired (pin 1 → BTN_SCRL, pin 2 → GND, matching the old part's COM/GND mapping) and re-placed on the PCB next to ENC1. |
| J1 | **TSW-104-07-T-S** | Samtec | 4-pin, 2.54mm pitch, THT vertical | 1 | DigiKey.ca [612-TSW-104-07-T-S-ND](https://www.digikey.ca/en/products/detail/samtec-inc/TSW-104-07-T-S/1101620) | $0.23 | **Active, in stock** (2,855 units + 1,744 factory stock). Pin assignment (this project's own choice — see [pinout.md](pinout.md#j1--swd-header-samtec-tsw-104-07-t-s)): 1=nRESET, 2=SWDCLK, 3=SWDIO, 4=GND. |
| J2 | **B2B-XH-A(LF)(SN)** | JST | 2-position, 2.50mm pitch, THT vertical | 1 | DigiKey.ca [455-B2B-XH-A-ND](https://www.digikey.ca/en/products/detail/jst-sales-america-inc/B2B-XH-A-LF-SN/1651045) | $0.15 | **Active, in stock** (303,971 units). "B2B-XH-A(LF)(SN)" is the full orderable catalog number — the bare "B2B-XH-A" used in earlier passes is JST's family name, not a purchasable SKU. This is the vertical/top-entry variant; JST also sells a right-angle version under a different part number (B2B-XH-AS), not used here. Battery-side mating harness (single-AAA holder + JST XH pigtail) sourced separately — see [open-items.md](open-items.md) item 7. |
| F1 | **0603L010YR** | Littelfuse | 0603 SMD, PPTC resettable fuse | 1 | DigiKey.ca [F2900CT-ND](https://www.digikey.ca/en/products/detail/littelfuse-inc/0603L010YR/1920183) | $2.10 | **Active, in stock** (120,808 units). 0.10A hold / 0.30A trip, 15V max. "0603L010YR" is the full orderable part number (Y = tape-and-reel qty code, R = packaging) — "0603L010" alone is the family designation, not a purchasable SKU. |
| Q1 | **DMG2305UXQ-7** | Diodes Incorporated | SOT-23, P-channel MOSFET | 1 | DigiKey.ca [31-DMG2305UXQ-7CT-ND](https://www.digikey.ca/en/products/detail/diodes-incorporated/DMG2305UXQ-7/5768821) | $0.70 | **Active, in stock** (17 units — thin, sufficient for a small build; re-check before a larger run). AEC-Q101 automotive-qualified. See the note below — this replaces the originally-specified DMP2035U-7, and is a genuine improvement, not just a stock swap. |

## nRF52810 support passives

| Ref | Value | Manufacturer | MPN | Package | Qty | Distributor / SKU | Price (CAD) | Stock |
|---|---|---|---|---|---|---|---|---|
| C1–C4 | 100nF | Yageo | CC0603KRX7R9BB104 | 0603 | 4 | DigiKey.ca [311-1344-1-ND](https://www.digikey.ca/en/products/detail/yageo/CC0603KRX7R9BB104/2103082) | $0.07 | On backorder at DigiKey.ca as of this pass (0 on hand; 4,000 due 2026-09-28 — effectively next-day). One per DEC1–DEC4 pin per Nordic's own regulator decoupling spec, not a shared net. |
| C5 | 1uF | Yageo | CC0603KRX5R6BB105 | 0603 | 1 | DigiKey.ca [311-1443-1-ND](https://www.digikey.ca/en/products/detail/yageo/CC0603KRX5R6BB105/2833608) | $0.10 | **In stock** (34,677 units). VDD bulk decoupling. |
| C6, C7 | 12pF NP0/C0G | Yageo | CC0402FRNPO9BN120 | 0402 | 2 | DigiKey.ca [311-1641-1-ND](https://www.digikey.ca/en/products/detail/yageo/CC0402FRNPO9BN120/5195050) | $0.06 | On backorder at DigiKey.ca as of this pass (0 on hand; 10,000 due 2026-10-12). Y1 load caps — matches Nordic's own published reference circuit (8pF crystal, 12pF load caps). |

## PMW3610 support passives

Values sourced from `github.com/siderakb/pmw3610-pcb`'s real KiCad schematic, cross-checked against PixArt's own datasheet Figure 6.

| Ref | Value | Manufacturer | MPN | Package | Qty | Distributor / SKU | Price (CAD) | Stock | Function |
|---|---|---|---|---|---|---|---|---|---|
| C8 | 10uF X5R | Murata | GRT188R61A106KE13J | 0603 | 1 | DigiKey.ca [490-GRT188R61A106KE13JCT-ND](https://www.digikey.ca/en/products/detail/murata-electronics/GRT188R61A106KE13J/13904783) | ~$0.17-0.26 | **In stock** (458 units) | VDD (pin 14) bulk decoupling. |
| C9 | 100nF | Yageo | CC0603KRX7R9BB104 | 0603 | 1 | Same as C1-C4 above | $0.07 | Backorder, restock 2026-09-28 | VDD (pin 14) decoupling, parallel with C8. |
| C10 | 100nF | Yageo | CC0603KRX7R9BB104 | 0603 | 1 | Same as C1-C4 above | $0.07 | Backorder, restock 2026-09-28 | VDDIO (pin 6) decoupling. |
| C11 | 1uF | Yageo | CC0603KRX5R6BB105 | 0603 | 1 | Same as C5 above | $0.10 | In stock | VDDIO (pin 6) bulk decoupling, parallel with C10. |
| C12 | 10uF X5R | Murata | GRT188R61A106KE13J | 0603 | 1 | Same as C8 above | ~$0.17-0.26 | In stock | VCP (pin 9) to GND — charge-pump reservoir, bulk. Per PixArt's own Figure 6, which specifies two parallel caps here (bulk + HF). |
| C13 | 10nF X7R | Yageo | CC0603KRX7R9BB103 | 0603 | 1 | DigiKey.ca [311-1085-1-ND](https://www.digikey.ca/en/products/detail/yageo/CC0603KRX7R9BB103/302819) | $0.05 | **In stock** (499,523 units) | VCP (pin 9) to GND — charge-pump reservoir, HF, parallel with C12. |
| C14 | 100nF X7R | Yageo | CC0603KRX7R9BB104 | 0603 | 1 | Same as C1-C4 above | $0.07 | Backorder, restock 2026-09-28 | CP(12)–CN(13) flying cap. |
| R1 | 10k, 1% | Yageo | RC0603FR-0710KL | 0603 | 1 | DigiKey.ca [311-10.0KHRCT-ND](https://www.digikey.ca/en/products/detail/yageo/RC0603FR-0710KL/726880) | $0.02 | **In stock** (659,892 units) | NRESET (pin 7) pull-up to +VSYS. |

## Boost regulator support passives

Pulled directly from TI's TLV61220 datasheet (SLVSB53A) application circuit.

| Ref | Value | Manufacturer | MPN | Package | Qty | Distributor / SKU | Price (CAD) | Stock |
|---|---|---|---|---|---|---|---|---|
| L1 | 4.7uH | Murata | **1269AS-H-4R7M=P2** | 2.5×2.0×1.0mm ("1008"/2520 metric) | 1 | DigiKey.ca [490-10577-1-ND](https://www.digikey.ca/en/products/detail/murata-electronics-north-america/1269AS-H-4R7M=P2/5272033) | $0.41 | **Active, in stock** (19,253 units). Toko's original inductor line (this part carries the legacy "1269AS" designation) was absorbed into Murata; the "=P2" packaging suffix is Murata/Toko's own separator convention, not a typo. |
| C15 (Cin) | 10uF, X5R | Murata | GRT188R61A106KE13J | 0603 | 1 | Same as C8 above | ~$0.17-0.26 | In stock | |
| C16 (Cout) | 10uF, X5R | Murata | GRT188R61A106KE13J | 0603 | 1 | Same as C8 above | ~$0.17-0.26 | In stock | |
| R2 (VOUT-to-FB) | **499kΩ, 1%** | Yageo | RC0603FR-07499KL | 0603 | 1 | DigiKey.ca [311-499KHRCT-ND](https://www.digikey.ca/en/products/detail/yageo/RC0603FR-07499KL/727267) | $0.02 | **In stock** (271,014 units). Confirmed standard E96 value. |
| R3 (FB-to-GND) | **180kΩ, 1%** | Yageo | RC0603FR-07180KL | 0603 | 1 | DigiKey.ca [311-180KHRCT-ND](https://www.digikey.ca/en/products/detail/yageo/RC0603FR-07180KL/726995) | $0.02 | **In stock** (35,626 units). Confirmed standard E96 value. |

### L1 footprint corrected during this pass

The real Murata 1269AS-H-4R7M=P2 body is **2.5 × 2.0 × 1.0mm** ("1008" imperial / 2520 metric case size). The schematic previously carried a placeholder footprint (`Inductor_SMD:L_1210_3225Metric`, a 3.2 × 2.5mm body) — oversized relative to the real part. This has been corrected to `Inductor_SMD:L_1008_2520Metric`, KiCad's own bundled footprint for this exact case size.

### Boost output voltage

VOUT = VFB × (1 + R2/R3), VFB typical 500mV. With R3 = 180kΩ, R2 = 499kΩ: **VOUT ≈ 1.89V** — comfortably clear of TLV61220's 1.8V absolute-minimum floor and clear of U2's 2.1V ceiling.

## Q1 — replaced DMP2035U-7 with DMG2305UXQ-7 (2026-09-27)

This design originally specified Diodes Incorporated's **DMP2035U-7**, an Active part that turned out to be out of stock at both DigiKey.ca and Mouser with a ~40-week manufacturer lead time. Three in-stock alternatives were checked against Diodes' own datasheets before deciding:

- **AO3401A** (Alpha & Omega Semiconductor, 1,831,820 units in stock at DigiKey.ca): VGS(TH) max **-1.3V** — worse than DMP2035U's -1.0V. Rejected: this board's reverse-polarity protection circuit has a documented low-battery corner case (see [open-items.md](open-items.md)), and a higher-magnitude threshold makes it worse, not better.
- **AO3415A** / **AO3415** (same family): both NRND or fully Obsolete at DigiKey.ca. Rejected on those grounds alone.
- **DMG2305UXQ-7** (Diodes Incorporated, 17 units in stock at DigiKey.ca): VGS(TH) max **-0.9V** — *better* than DMP2035U's -1.0V, narrowing the low-battery corner case rather than widening it. AEC-Q101 automotive-qualified (not a requirement here, but not a downside). **Selected.**

All three candidates use the identical SOT-23-3 Gate-Source-Drain pinout as DMP2035U-7, so this was a pure component substitution — no footprint or schematic rewiring was needed. The vendored library was renamed from `diodes-dmp2035u`/`DMP2035U` to `diodes-dmg2305uxq`/`DMG2305UXQ` (symbol, footprint, 3D model, and datasheet all updated to match); see [that library's ATTRIBUTION.md](../../hardware/libraries/vendored/diodes-dmg2305uxq/ATTRIBUTION.md) for the full comparison. ERC re-confirmed clean (0 violations) after the swap.

## Corrections made during this pass's audit

1. **Y1's full orderable part number.** The previous pass specified "NX2016SA-32MHZ-STD-CZS-5" (an LCSC-side catalog string). The real DigiKey.ca-orderable NDK America part meeting the same spec (32MHz, 8pF, ±10ppm) is **NX2016SA-32MHZ-EXS00A-CS06654**.
2. **F1's full orderable part number.** "0603L010" is Littelfuse's family designation; the orderable part is **0603L010YR**.
3. **J2's full orderable part number.** "B2B-XH-A" is JST's family name; the orderable part is **B2B-XH-A(LF)(SN)**.
4. **L1's footprint.** Corrected from an oversized placeholder to the real part's 2520-metric case size (see above).
5. **Q1's full orderable part number.** "DMP2035U" is the family designation; **DMP2035U-7** is the orderable 7"-reel part.

All five are reflected directly in the schematic's component fields (Manufacturer/MPN/Distributor/DPN, visible via `kicad-cli sch export bom`) as well as in the tables above.
