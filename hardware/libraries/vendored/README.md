# Vendored libraries

Third-party open-hardware KiCad libraries brought into this repository as
plain files, because the part has no suitable entry in KiCad's global
libraries. Vendored in directly (not as git submodules) so the project stays
self-contained and clones without an extra `--recurse-submodules` step.

Each subdirectory here is a separate vendored source and carries its own
`ATTRIBUTION.md` (what was taken, from where, and what if anything was
changed) plus a full copy of that source's license.

| Directory | Part | Source | License |
|---|---|---|---|
| `pmw3610dm-sudu/` | PixArt PMW3610DM-SUDU optical sensor | [siderakb/pmw3610-pcb](https://github.com/siderakb/pmw3610-pcb) | CERN-OHL-P v2 |
