# Wera 367/6 TORX Screwdriver Tray — Design Notes

Gridfinity tray for the Wera 367/6 TORX Kraftform Plus set (6 T-handle-less
straight Torx screwdrivers). Built with ToolTrace.ai's native "Gridfinity"
export mode — see `docs/tooltrace-to-gridfinity-workflow.md` (Part 1) for
the general, reusable procedure this project follows.

---

## Tool set

Per Wera's catalog (part 05028062001, plain 367/6 — **not** the HF
"holding function" variant, 05028059001, which has a 7th TX8×60mm tool and
different sizing on a couple of the others). Confirm against your physical
set before relying on this table:

| Tool | Tip size | Shaft length | Handle Ø | Pocket depth | Finger notch depth |
|------|----------|--------------|----------|-------------|---------------------|
| Wera 367 | TX 10 | 80 mm | 25 mm | 17.5 mm | 28.0 mm |
| Wera 367 | TX 15 | 80 mm | 32 mm | 22.5 mm | 28.0 mm |
| Wera 367 | TX 20 | 100 mm | 32 mm | 22.5 mm | 28.0 mm |
| Wera 367 | TX 25 | 100 mm | 36 mm | 25.0 mm | 28.0 mm |
| Wera 367 | TX 30 | 115 mm | 36 mm | 25.0 mm | 28.0 mm |
| Wera 367 | TX 40 | 140 mm | 40 mm | 28.0 mm | 28.0 mm |

- **Handle Ø** — measured by Craig with calipers (thickest point of the
  Kraftform grip, not the shaft/tip diameter).
- **Pocket depth** — handle Ø × 70% rule, same as the prior two trays,
  rounded to the nearest 0.5mm.
- **Finger notch depth** — expected to land at **28.0mm for all 6 tools**
  (matching the deepest pocket, TX 40), based on how the notch-depth
  constraint behaved on the flathead+Phillips tray (notch must be no
  lower than the deepest pocket, and the design's max achievable depth
  turned out to equal that same value, leaving no margin above it) — but
  confirm this holds once you're in ToolTrace, since it's an observed
  pattern, not a documented API guarantee.

### Source photos → ToolTrace design

All 6 tools traced from a single photo, `torx.jpeg` (all 6 on one sheet).

### Layout

All 6 tools arranged on a **7u × 9u** grid (42mm pitch), split into
**4 plates** (2×2), each plate **147 × 189mm** (3.5u × 4.5u — a
non-integer split, same pattern seen on the prior two trays; the split
seams won't land exactly on 42mm grid lines).

ToolTrace's internal design name is "Green Handled Screwdrivers" (from the
split-STL `manifest.json`) — same naming quirk as the prior two jobs
("6.0x150", "Green Screwdrivers"); it's not a dimension, just whatever the
design happened to be named at export time.

### Exports

- `gridfinity/source/tooltrace/wera-367-6-torx/split-stl/` — 4 plates ×
  {tray, inserts} STL pairs, plus `manifest.json`.
- `gridfinity/source/step/wera-367-6-torx/wera-367-6-torx-tray_v1.step`
  — STEP export of the whole combined design (not split per plate).
- `gridfinity/stl/inserts/wera-367-6-torx/` — the 4 tray STLs, archived
  and renamed per `naming.md`. Note: each tray's actual bounding box
  (measured directly from the STL) is noticeably smaller than the
  manifest's nominal 147×189mm tile size — tools don't fill their whole
  reserved tile, so the real per-plate footprints are ~2.5×4.5u for
  pieces 1/2/4 and ~2.5×1.5u for piece 3 (which has fewer/smaller tools).
  Total height 39.17mm (5.6u) matches the flathead+Phillips tray exactly,
  since both designs share the same 28.0mm deepest pocket.
- `gridfinity/3mf/wera-367-6-torx/wera-367-6-torx-tray_7x9x5.6u_v1.3mf`
  — sliced Bambu Studio project (all 4 plates).

---

## Status

- [x] Tool set confirmed against physical set — Craig's 6 handle
      measurements (T10/T15/T20/T25/T30/T40) match the plain 367/6 set,
      not the 7-piece HF variant
- [x] Tools photographed (colored background, distance + zoom, shadow-free)
- [x] Tools traced in ToolTrace (Fast mode)
- [x] Laid out on a 7u × 9u grid, no overlap
- [x] Pocket depths set per tool (70%-of-handle-Ø rule)
- [x] Finger notches added per tool (28.0mm depth, matching deepest pocket)
- [x] Sketch singularity found (via ToolTrace's Fine Tune UI) and fixed on
      one tool shape
- [x] STEP/STL exported; print came out well (per Craig, 2026-09-10)
- [x] Source photo (`torx.jpeg`), STEP export, and raw split-STL exports
      copied into repo
- [x] Tray STL archived to `gridfinity/stl/inserts/wera-367-6-torx/`
      (4 pieces, renamed per naming convention)
- [x] Printed (per Craig, 2026-09-10)
- [x] Sliced `.3mf` saved to `gridfinity/3mf/wera-367-6-torx/`

