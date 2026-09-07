# Bambu Studio Print Profile: Gridfinity Tray - Light

A custom Bambu Studio process preset for **static tool trays** — printed on a
Bambu Lab P2S — that minimizes filament and print time. These trays only hold
tools by gravity (no clamping, no structural load beyond a tool resting in a
pocket), so wall count, infill, and supports can all be cut well below a
normal-quality default.

Verified 2026-09-06: created in Bambu Studio's Process panel, checked field-by-field
in the UI, exported, and confirmed to match. This replaces an earlier draft of this
doc/profile that had two real problems — its markdown table claimed a 1.2mm wall
while the JSON set a single 0.42mm-line-width wall loop (an unreconciled
inconsistency), and it enabled tree supports by default even though these tray
shapes are normally self-supporting. Both are fixed below.

## Settings

Preset name: **"Gridfinity Tray - Light"**, inherits from **"0.24mm Standard @BBL P2S"**
(all quality/speed/temperature settings come from that base preset, unchanged —
only the fields below are overridden):

| Setting | Value | Rationale |
|---|---|---|
| Wall loops | 2 | Matches the "0.24mm Standard" base already — 1 wall risks pinholes/fragile corners at low infill |
| Top shell layers | 2 | Enough to bridge sparse infill without holes; nothing presses on the surface |
| Bottom shell layers | 2 | Same — no load-bearing requirement |
| Sparse infill density | 8% | Just holds gravity-fed contents; far below a normal 15% default |
| Sparse infill pattern | Lightning | Purpose-built for "support the top surface, nothing else" — uses less material than any other pattern at a given density |
| Supports | Off | Tooltrace-derived tray pockets are normally flat-bottomed and self-supporting; check the slice preview per-model rather than defaulting supports on |
| Brim type | No brim | Tray footprints are normally large enough for bed adhesion without one |
| Layer height | 0.24mm (inherited) | Largest built-in preset for this printer/nozzle; cuts print time without hand-tuning speeds |

Everything not listed above (speeds, temperatures, cooling, retraction) is left
exactly as Bambu's own "0.24mm Standard @BBL P2S" preset has it — those are
already tuned for this printer, so there's no reason to guess at replacement
numbers.

## When to Use This Profile

✅ Static tool storage trays (hand tools, drill bits, etc.)
✅ Gridfinity-compatible inserts, gravity-fed only
✅ Drawer organizers

❌ Anything that needs to resist lateral force, clamping, or repeated stress
❌ Parts with real overhangs — check the slice preview; if it needs supports, this profile doesn't turn them on for you

## How to Import

1. Bambu Studio → File → Import → Import Configs (or the import icon near the
   preset dropdown)
2. Select `gridfinity-tray-light.json`
3. Confirm it appears in the Process dropdown as "Gridfinity Tray - Light"

To reproduce it by hand instead: start from "0.24mm Standard @BBL P2S" and change
only the fields in the Settings table above (wall loops, infill, top/bottom
shells, supports, brim — under the Strength / Support / Others tabs respectively).

## Notes

- This is PLA-tuned by inheritance from the base preset; if you switch materials,
  Bambu Studio's own material presets should still take precedence for temps.
- No filament-savings percentage is claimed here — the earlier draft's "45-55%
  savings" table was a guess, not a measurement. If you want a real number, compare
  the sliced filament estimate for the same model under this preset vs. "0.24mm
  Standard @BBL P2S" unmodified.
