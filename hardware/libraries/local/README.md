# Local libraries

Symbols, footprints, and 3D models authored specifically for this board —
anything not adequately covered by KiCad's bundled global libraries or by a
vendored third-party library.

- `symbols/local.kicad_sym` — project-original schematic symbols:
  - `GND` — copied unmodified from KiCad's bundled `power.kicad_sym`
    (CC-BY-SA 4.0, same license as the vendored Nordic library — see
    [`../vendored/nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md`](../vendored/nordic-nrf52810-qcxx/license-cc-by-sa-4.0.md)).
  - `+VSYS` — this project's single shared power rail, as a global power
    symbol. Adapted from KiCad's bundled `+1V8` power symbol template (same
    license), renamed since `+VSYS` is this project's own net name, not a
    fixed voltage — see
    [docs/hardware/architecture.md](../../../docs/hardware/architecture.md#single-shared-power-rail).
- `footprints.pretty/` — project-original footprints.
- `3dmodels/` — STEP/WRL 3D models referenced by local footprints.
