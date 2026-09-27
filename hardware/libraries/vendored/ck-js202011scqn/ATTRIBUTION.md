---
name: ck-js202011scqn-attribution
---

# JS202011SCQN slide switch footprint — attribution

- **Footprint**
  (`ck-js202011scqn.pretty/switch-slide-js202011scqn.kicad_mod`): copied from
  DigiKey's official KiCad library
  (`digikey-footprints.pretty/Switch_Slide_JS202011SCQN.kicad_mod`), then
  upgraded from its original legacy file format with `kicad-cli fp upgrade`
  (geometry unchanged).
  - Upstream source: <https://github.com/Digi-Key/digikey-kicad-library>
  - License: CC-BY-SA 4.0 — full text at
    [`../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md).
- **Symbol** (`ck-js202011scqn.kicad_sym`): hand-drawn for this project from
  the part's real 6-pad DPDT layout (two independent 3-pin sections).

## Part selection note

SW1 needed a simple SMD on/off power switch. C&K's own SPDT sibling
(JS102011SCQN) has no ready-made KiCad footprint in either KiCad's or
DigiKey's official libraries; JS202011SCQN (DPDT, same JS mechanical family,
confirmed active/in-stock at LCSC and DigiKey) does. This design uses only
one section (pins 1/2/3) as the power switch; the second section (pins
4/5/6) is left unconnected — a standard, common practice (a DPDT part used
as SPDT), not a design compromise. See
[docs/hardware/bom.md](../../../../docs/hardware/bom.md).

## Datasheet note

No directly-downloadable datasheet PDF is included in
`hardware/datasheets/` for this part — Littelfuse/C&K's own hosting
(`ckswitches.com`) and LCSC's datasheet mirror both blocked automated
download during this pass. The part itself (stock, active status, pinout)
was independently confirmed live at LCSC's own product page,
<https://www.lcsc.com/product-detail/C221666.html>, and via search of
DigiKey's listing; that LCSC page links its own datasheet PDF copy if you
need the full mechanical drawing before ordering.

## 3D model

`3dmodels/switch-slide-js202011scqn.step` is Ultra Librarian's real
vendor-partner STEP model for this exact part
(<https://app.ultralibrarian.com/details/3ef4ef6d-1930-11e9-ab3a-0a3560a4cccc/C-K-Components/JS202011SCQN>),
downloaded manually (the site sits behind an account-gated download
that blocks automated fetching) and placed here unmodified.

**Orientation note (2026-09-27):** this file's own STEP data uses a
Y-up axis convention (its Y axis is the part's true vertical/height
axis) rather than KiCad's Z-up footprint convention. The footprint's
`(model ...)` block applies a `-90°` rotation about X to correct this
— confirmed by rendering the part in place with `kicad-cli pcb render`
and checking it sits right-side-up on its pads, actuator facing up,
rather than appearing sheared off to one side. No plain offset alone
could fix this; it was an axis-convention mismatch, not a placement
error.
