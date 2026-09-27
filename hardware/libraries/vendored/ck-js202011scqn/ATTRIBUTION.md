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

## 3D model — confirmed to exist, not retrievable by automated fetch

A real STEP model for JS202011SCQN exists on Ultra Librarian and
SnapEDA (both aggregated by Octopart), confirmed via their own listing
pages. Both sites sit behind Cloudflare bot-protection/account-gated
downloads that returned a bot-check page rather than a file when
fetched automatically during this pass — the same class of limitation
already documented for other sourcing channels in this project. No
close substitute exists in KiCad's own bundled 3D model pack (this is
a fairly unique DPDT slide-switch body shape, not a generic package). A
human with a free account can pull the real model directly:
<https://app.ultralibrarian.com/details/3ef4ef6d-1930-11e9-ab3a-0a3560a4cccc/C-K-Components/JS202011SCQN>
or <https://www.snapeda.com/parts/JS202011SCQN/C%26K/view-part/>.
