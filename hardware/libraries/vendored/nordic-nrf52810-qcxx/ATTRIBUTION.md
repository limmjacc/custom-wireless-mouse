---
name: nordic-nrf52810-qcxx-attribution
---

# nRF52810-QCxx symbol and footprint — attribution

The KiCad symbol (`nordic-nrf52810-qcxx.kicad_sym`, part `nRF52810-QCxx`) and
footprint (`nordic-nrf52810-qcxx.pretty/qfn-32-1ep-5x5mm-p0.5mm-ep3.6x3.6mm.kicad_mod`)
in this directory were extracted from KiCad 10's own bundled official
library (`MCU_Nordic.kicad_sym` and `Package_DFN_QFN.pretty`, shipped with
the KiCad application itself), not drawn from scratch.

- Upstream source: KiCad's official symbol/footprint libraries,
  <https://gitlab.com/kicad/libraries/kicad-symbols> and
  <https://gitlab.com/kicad/libraries/kicad-footprints>.
- License: CC-BY-SA 4.0, reproduced in `license-cc-by-sa-4.0.md` in this
  directory. Per that license's own exception, using these files to produce
  an electronic design does not require attribution *of the design*; this
  attribution file exists because the raw library files themselves are
  being redistributed here as a vendored copy, which the license explicitly
  says must retain attribution and license text.
- Part vendored: `nRF52810-QCxx` (32-QFN, 5x5mm), matching U1
  (Nordic nRF52810-QCAA-T) exactly — confirmed via the symbol's own
  `ki_fp_filters` and footprint `descr` field, both of which reference
  `http://infocenter.nordicsemi.com/pdf/nRF52810_PS_v1.1.pdf`, the same
  datasheet this project's U1 is sourced against.

## 3D model

`3dmodels/qfn-32-1ep-5x5mm-p0.5mm-ep3.6x3.6mm.step` is Ultra Librarian's
real vendor-partner STEP model for the exact part (Nordic
NRF52810-QCAA-T,
<https://app.ultralibrarian.com/details/ff3fee79-22f4-11eb-9033-0a34d6323d74/Nordic-Semiconductor/NRF52810-QCAA-T>),
downloaded manually (the site sits behind an account-gated download
that blocks automated fetching) and placed here unmodified.

**Orientation note (2026-09-27):** this file's own STEP data uses a
Y-up axis convention (its Y axis is the part's true vertical/height
axis, confirmed by parsing the file's `CARTESIAN_POINT` entities: X and
Z both span the full 5mm package width, Y spans only ~0.9mm — the real
package height) rather than KiCad's Z-up footprint convention. The
footprint's `(model ...)` block applies a `-90°` rotation about X to
correct this — confirmed by rendering the part in place with
`kicad-cli pcb render` and checking the QFN body, pin-1 dot marker, and
gull-wing leads sit correctly centered on the pads rather than sheared
off to one side.
