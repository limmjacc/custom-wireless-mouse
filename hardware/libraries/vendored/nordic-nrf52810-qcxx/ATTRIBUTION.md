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
