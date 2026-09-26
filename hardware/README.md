# Hardware

KiCad 10 project for the custom wireless mouse PCB. Fully self-contained and
portable: every symbol, footprint, and 3D model the schematic depends on is
vendored inside this folder and referenced through `${KIPRJMOD}`-relative
paths — nothing depends on KiCad's global library tables or an internet
connection to open and edit. See [`docs/hardware/schematic.md`](../docs/hardware/schematic.md)
for how the schematic itself is organized.

## Opening the project

Open `custom-wireless-mouse.kicad_pro` in KiCad 10. The project's
`sym-lib-table` and `fp-lib-table` are picked up automatically.

## Layout

```
hardware/
├── custom-wireless-mouse.kicad_pro   Project file
├── custom-wireless-mouse.kicad_sch   Schematic — complete, ERC-clean
├── custom-wireless-mouse.kicad_pcb   PCB layout — not started (no board outline yet)
├── sym-lib-table                     Project-local symbol library table
├── fp-lib-table                      Project-local footprint library table
├── datasheets/                       PDF datasheets for every non-passive part, kebab-case named
├── libraries/
│   ├── local/                        Symbols/footprints authored for this project
│   │   └── symbols/local.kicad_sym     GND, +VSYS, and PWR_FLAG
│   └── vendored/                     One directory per part, each with its own ATTRIBUTION.md
│       ├── nordic-nrf52810-qcxx/       U1 — from KiCad's own official library
│       ├── pmw3610dm-sudu/             U2 — from github.com/siderakb/pmw3610-pcb (CERN-OHL-P v2)
│       ├── ti-tlv61220/                U3 — symbol hand-drawn from TI's datasheet pinout
│       ├── ndk-nx2016sa/               Y1 — from KiCad's own official library
│       ├── bourns-pec11r/              ENC1 — from DigiKey's official KiCad library
│       ├── panasonic-evq-p7b01p/       SW2–SW4 — from KiCad's own official library
│       ├── ck-js202011scqn/            SW1 — from DigiKey's official KiCad library
│       └── samtec-tsw-104-07-t-s/      J1 — from KiCad's own official library
├── fab-outputs/                      Gerbers, drill, pick-and-place, and BOM exports per revision
└── 3d-renders/                       Exported board renders (PNG/STEP) for docs and reference
```

## Library policy

Every specific, individually sourced part (every IC, the crystal, the
encoder, every switch, the header) has its own symbol and footprint vendored
into `libraries/vendored/<part>/` — nothing depends on KiCad's global
libraries for these, since a global library's contents can differ across
KiCad installs and versions. Only truly generic, manufacturer-agnostic
passives (resistors, capacitors, the inductor) use KiCad's bundled `Device`
and footprint libraries directly, since there's no meaningful "sourcing"
decision attached to a 0603 resistor footprint.

Each vendored part's `ATTRIBUTION.md` records exactly where its symbol and
footprint came from and what license applies (mostly CC-BY-SA 4.0, matching
KiCad's own library license, since most of these were extracted from KiCad's
or DigiKey's official libraries; U2 is CERN-OHL-P v2 from its open-hardware
source; U3's symbol is original, hand-drawn from a public datasheet pinout
table rather than copied from anywhere).

## Datasheets

`datasheets/` holds a PDF for every part above the passive-component level —
downloaded from the manufacturer or a stable distributor mirror where a
direct link could be found. A couple of manufacturers' sites (Nordic's full
product specification, one slide-switch datasheet) sit behind bot-protection
that blocked a direct download; where that happened, the BOM notes it and
gives the page to fetch manually instead of a broken/substituted link.

## Fabrication outputs

`fab-outputs/` holds exports generated *from* the KiCad project (Gerbers,
drill files, pick-and-place, BOM) — never hand-edited. Regenerate per
revision; don't rely on stale exports. Nothing has been exported yet since
the PCB layout hasn't started.
