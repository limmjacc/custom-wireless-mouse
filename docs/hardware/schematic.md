# Schematic

The schematic lives at [`hardware/custom-wireless-mouse.kicad_sch`](../../hardware/custom-wireless-mouse.kicad_sch) — a single A3 sheet, sectioned into four visually boxed zones rather than split into KiCad hierarchical sub-sheets (a reasonable call at this part count, and how the reference PMW3610 project itself is drawn).

## Sections

- **Power Supply** (top-left) — J2 (battery input connector) → F1 (PPTC resettable fuse) → Q1 (P-channel MOSFET, reverse-polarity ideal-diode protection) → SW1 (power switch) → U3 (TLV61220 boost) → the shared **+VSYS** rail, with the R2/R3 feedback divider and input/output bulk caps.
- **MCU — U1 (nRF52810)** (top-right) — U1 with its decoupling network, 32MHz crystal (Y1) and load caps, SWD header (J1), and the antenna net.
- **Optical Sensor — U2 (PMW3610)** (bottom-left) — U2 with its VDD/VDDIO/VCP decoupling and the CP–CN charge-pump flying cap.
- **User Input — Wheel & Buttons** (bottom-right) — ENC1 (mouse scroll wheel encoder), SW2–SW4 (L/R/FN buttons), and SW5 (wheel middle-click). ENC1 and SW2–SW5 are placed but not yet wired in — see [pinout.md](pinout.md) for their pin functions and [open-items.md](open-items.md) for what's still pending on this section specifically.

## Conventions used

- **Global power nets**: `+VSYS` and `GND` are drawn as power symbols (not plain wires threaded across the page), each defined once in
  [`hardware/libraries/local/symbols/local.kicad_sym`](../../hardware/libraries/local/symbols/local.kicad_sym) and reused everywhere that net appears — this is what makes every `+VSYS`/`GND` glyph on the sheet the same electrical net without a single wire connecting them visually.
- **Cross-section signals use net labels, not long wires.** SPI_SCLK, SPI_SDIO, SPI_NCS, SENS_MOTION, SENS_NRESET, WHEEL_A, WHEEL_B, WHEEL_SW, BTN_L, BTN_R, and BTN_FN each appear as a short labeled stub at both ends (e.g., at U1's GPIO pin and again at U2 or the relevant switch) rather than as a wire routed physically across the sheet. This is the standard way to keep a schematic legible once wires would otherwise cross section boundaries.
- **PWR_FLAG markers**: KiCad's ERC expects every power net to be "driven" by something it recognizes as a power source. Since several real nodes on this board (the battery's pins, the PMW3610's internal charge-pump nodes) are electrically real but not typed as power sources in their symbols, a small `PWR_FLAG` symbol marks each such net as intentionally externally driven — this is standard KiCad practice, not a workaround specific to this project.
- **No-connect flags** (the small "X" marks) appear only on pins whose electrical type doesn't already declare them unconnected (e.g., U1's spare GPIOs, SW1's unused throw). Pins already typed `no_connect` in their own symbol (U2 pin 4, SW1's section-B pins) are left bare, since adding a flag there is redundant and ERC treats the combination as a contradiction.

## Verification

Checked with `kicad-cli sch erc` against the actual project (not a standalone file — library resolution depends on `hardware/sym-lib-table` and `fp-lib-table`).

With ENC1 and SW2/SW3/SW4/SW5 placed but not yet wired (see above), ERC currently reports 15 `pin_not_connected` errors (3 unconnected pins each, on those 5 parts) plus a handful of `unconnected_wire_endpoint`/`isolated_pin_label` warnings on the WHEEL_A/WHEEL_B/WHEEL_SW/BTN_L/BTN_R/BTN_FN net stubs left over for wiring them in — all expected for this in-progress state, not bugs. Once those parts are wired, the design returns to its otherwise-clean state: **0 errors, 1 informational item**, expected rather than a bug:

- `isolated_pin_label` on the `ANT` net — genuinely a single connection point by design (a PCB trace antenna, not a second schematic pin to connect to).

A full bill of materials with footprints, generated directly from the schematic (`kicad-cli sch export bom`), matches [`docs/hardware/bom.md`](bom.md) exactly.

## What isn't drawn on the schematic

- **LENS1** (the PMW3610's matched lens) — a mechanical part with no electrical connection. Noted in a text callout next to U2.
