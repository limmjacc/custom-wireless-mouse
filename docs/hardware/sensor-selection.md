# Sensor selection

## Evaluation history

Three sensors were evaluated in sequence before landing on the current pick.
Keeping this history because the reasoning matters if sourcing changes again.

### 1. MX8650A (Sigma Micro)

The sensor already present on the original kit board, fully characterized
(complete register map obtained from its datasheet) during the
reverse-engineering phase of this project. Considered for reuse in the new
design since it was already fully understood.

Rejected as the primary pick when its LCSC listing was checked live and
found to 404, with a site-wide LCSC search turning up nothing. Still viable
if desoldered from an existing kit board rather than newly purchased — see
[Desoldering MX8650A as a fallback path](#desoldering-mx8650a-as-a-fallback-path)
below.

### 2. PMW3360DM-T2QU (PixArt)

A gaming-tier sensor with a genuinely public official datasheet (unusual for
PixArt's current lineup, most of which is NDA-gated) and enormous hobbyist
precedent via the QMK/mechanical-keyboard community. Real, in production,
but sourced through regional distributors (EPS Global, Codico) or hobbyist
resellers, not DigiKey/Mouser/LCSC. Considered, then superseded once a
better-fitting part was identified.

### 3. PMW3610DM-SUDU (PixArt) — current pick

Purpose-built as a *low power laser mouse sensor* for wireless applications,
unlike PMW3360 which is a gaming sensor pressed into low-power service. Full
public 8-page datasheet with pin table and register map.

Real open-hardware precedent: [`github.com/siderakb/pmw3610-pcb`](https://github.com/siderakb/pmw3610-pcb)
(CERN-OHL-P licensed, includes an actual KiCad symbol/footprint — vendored
into this repository at [`hardware/libraries/vendored/pmw3610dm-sudu/`](../../hardware/libraries/vendored/pmw3610dm-sudu/))
and mainline Zephyr/ZMK driver support.

User-sourced at ~$4 CAD/unit via AliExpress; cross-checked against two
independent listings (Alibaba, $3 USD at MOQ 2, 475 buyers, 4.8/5.0 rating;
eBay, $6.40 from a Shenzhen seller) to confirm the price wasn't an outlier.

## Desoldering MX8650A as a fallback path

If sourcing PMW3610 falls through, or as a parallel option: the original kit
board's MX8650A can be desoldered and reused, since its complete register
interface is already known from the reverse-engineering phase of this
project.

This requires retargeting the shared rail to either 1.73–1.87V or 2.0–3.5V
(MX8650A's two supported modes) rather than the flat 1.8V assumed for the
PMW3610 path — **the two sensors are not pin- or voltage-compatible, this is
a fork in the design, not an add-on.** The current design (this documentation
set) assumes the PMW3610 path throughout; the MX8650A fallback path has been
discussed but not fully re-specced against a new rail voltage and net list.

## What research ruled out along the way

Documented here because it's genuinely useful to not repeat this work:

- **ADNS-2610 (Broadcom):** a live search suggested "ships today" at DigiKey.
  The actual product page states Part Status: Obsolete, no longer
  manufactured. Any search-snippet claim of stock needs verification against
  the live page, not the snippet — this was the clearest example of why.
- **MX8650A on LCSC:** listing page 404s; site-wide search for the part
  turns up nothing. Likely delisted since it was last checked (it was live
  when its datasheet was first pulled earlier in this project).
- **PixArt's current sensor line generally:** not found on DigiKey, Mouser,
  or LCSC in direct searches. Distributed through regional partners (EPS
  Global, Codico) and hobbyist resellers instead. This appears to be a
  structural gap in that specific market segment (cheap purpose-built
  optical mouse sensors), not a research shortfall.
