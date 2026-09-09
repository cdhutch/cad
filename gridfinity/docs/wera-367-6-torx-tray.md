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

---

## Status

- [ ] Tool set confirmed against physical set (plain 367/6 vs. HF variant)
- [ ] Tools photographed (colored background, distance + zoom, shadow-free)
- [ ] Tools traced in ToolTrace (Fast mode)
- [ ] Laid out, no overlap
- [ ] Pocket depths set per tool
- [ ] Finger notches added per tool
- [ ] STEP/STL exported and verified in Bambu Studio
- [x] Source photo (`torx.jpeg`) and STEP/STL exports copied into repo
- [ ] Sliced `.3mf` saved to `gridfinity/3mf/wera-367-6-torx/`
- [ ] Printed
- [ ] STL archived to `gridfinity/stl/inserts/wera-367-6-torx/`
