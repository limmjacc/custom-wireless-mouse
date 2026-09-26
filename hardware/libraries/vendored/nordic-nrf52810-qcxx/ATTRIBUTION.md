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

No 3D model is included: the exact exposed-pad variant this footprint uses
(EP3.6x3.6mm) was not present in KiCad's bundled 3D model pack, and a
request for the same file from KiCad's upstream `kicad-packages3d`
repository returned nothing. Nearby exposed-pad variants (3.45mm, 3.7mm) do
exist, but were not substituted in to avoid implying a geometry that isn't
actually confirmed correct.
