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

## 3D model — visual approximation, not an exact match

`3dmodels/qfn-32-1ep-5x5mm-p0.5mm-ep3.6x3.6mm-approx.step` is copied from
KiCad's own bundled `Package_DFN_QFN.3dshapes/QFN-32-1EP_5x5mm_P0.5mm_EP3.7x3.7mm.step`.
The exact exposed-pad variant this footprint uses (EP3.6x3.6mm) has no
matching 3D model anywhere in KiCad's bundled pack — the closest real one
differs only in the exposed pad size (3.7mm vs. this part's 3.6mm), a
difference of 0.1mm on a pad that sits underneath the package and isn't
visible from outside. Body outline, pin count, and pin pitch are identical
for this whole package family, so this is accurate for a rendered board
view; it is not claimed to be an exact vendor-verified model the way the
rest of this project's 3D models are.

Real vendor-partner STEP models for the exact part (Nordic
NRF52810-QCAA-T) exist on Ultra Librarian and SnapEDA (Octopart aggregates
both), but both sites sit behind bot-protection/account-gated downloads
that block automated retrieval — same limitation already documented for
several sourcing channels elsewhere in this project. A human with a free
account can pull the exact model from either site in under a minute:
<https://app.ultralibrarian.com/details/ff3fee79-22f4-11eb-9033-0a34d6323d74/Nordic-Semiconductor/NRF52810-QCAA-T>
or <https://www.snapeda.com/parts/NRF52810-QCAA-T/Nordic%20Semiconductor%20ASA/view-part/>.
