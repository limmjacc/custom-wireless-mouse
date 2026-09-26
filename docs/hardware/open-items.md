# Open items — verification checklist

## Resolved by the audited schematic pass

These were open in earlier drafts and are now closed — kept here for the record, not as action items:

- ~~Charge pump net mapping (C12, C13).~~ Resolved by reading the actual KiCad schematic file (not just the BOM) from `github.com/siderakb/pmw3610-pcb`, cross-checked against PixArt's own datasheet Figure 6. See [bom.md](bom.md#corrections-made-during-this-passs-independent-re-audit).
- ~~Boost regulator FB resistor final values.~~ R2 = 499kΩ, R3 = 180kΩ, both confirmed in stock (see [bom.md](bom.md)). VOUT ≈ 1.89V.
- ~~SW1 (slide switch) and J1 (SWD header) not stock-checked.~~ Both replaced with specific, individually verified, in-stock parts (C&K JS202011SCQN and Samtec TSW-104-07-T-S).
- ~~GPIO pin assignment.~~ Fixed in the schematic — see [pinout.md](pinout.md).
- **Crystal load capacitance exceeding Nordic's documented maximum** — not previously flagged as an open item, but caught during this pass's audit and fixed (see [bom.md](bom.md)).

## Still open

1. **Encoder mechanical fit.** ENC1's stock/documentation status is confirmed; its physical fit against the kit's actual wheel assembly is not, and requires the physical parts, not more research.
2. **Antenna trace geometry.** Nordic publishes reference PCB trace antenna designs for the nRF52 series; pull the actual geometry from that reference at layout time. The schematic marks pin 19 (ANT) with a single-connection label by design — there's nothing to wire on the schematic side, this is purely a layout task.
3. **U2/LENS1 sourcing channel.** Pick and confirm one specific reseller before ordering, given absence from DigiKey, Mouser, and LCSC. Live pricing on the AliExpress-style listings was not re-confirmed this pass (storefronts block automated fetch) — re-check price before ordering.
4. **L1 footprint.** The schematic uses a placeholder footprint (`Inductor_SMD:L_1210_3225Metric`) for L1 — confirm against Murata 1269AS-H-4R7M-P2's real package drawing before layout; no exact-match footprint was found in KiCad's bundled libraries.
5. **B1 footprint.** Left blank in the schematic — depends on the kit's actual battery holder, not a new part.
6. **PMW3610 direct-trace pins (1/10, 15/16) vs. PixArt's own reference.** This design follows the proven open-hardware board's direct-trace approach (no components between +VCSEL/PASS_T and XYLASER/−VCSEL). PixArt's own Figure 6 shows an alternate topology (a shared decoupled "VDD_SENSOR" rail instead of direct traces) — not adopted here since the direct-trace approach has real working-silicon precedent, but worth knowing if debugging the sensor ever points at this area.
7. **USB dongle storage slot.** If the mechanical kit expects a small USB receiver to live somewhere in the mouse body, that slot goes unused under this board's BLE-only architecture. Not yet confirmed against the physical kit parts.

## Explicitly not open items (by design, not oversight)

- **DCC (U1 pin 31) is unconnected.** Internal LDO only, no DC/DC converter used — see [architecture.md](architecture.md#single-shared-power-rail).
- **SW1 section B (pins 4/5/6) is unconnected.** SW1 is a DPDT part used as a simple SPST power switch — see [bom.md](bom.md).
- **U2 pin 4 (NC) is unconnected.** Typed no-connect in the vendored symbol itself.
