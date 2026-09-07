# Wera Flathead + Phillips Screwdriver Tray — Design Notes

Gridfinity tray for 7 Wera precision screwdrivers — 3 slotted (flathead) and
4 Phillips — built as **one combined ToolTrace design**, split into 3 print
plates. Follows the ToolTrace-native workflow in
`docs/tooltrace-to-gridfinity-workflow.md` (Part 1).

Flathead and Phillips tools are kept visually distinguishable **not** by
printing whole plates in different colors — each plate's pockets are a mix
of flathead and Phillips tools, so there's no clean per-plate color split —
but by printing each plate's **insert** sheet twice, once per color, and
hand-picking individual insert pieces by tool-head shape when assembling
the tray (see Exports below).

---

## Tool set

| Tool | Blade/head spec | Shaft length | Handle Ø | Pocket depth |
|------|-----------------|--------------|----------|--------------|
| Wera 335 | 0.5 × 3.0 mm slotted | TBD | 25 mm | 17.5 mm |
| Wera 334 | 0.8 × 5.0 mm slotted | 100 mm | 30 mm | 21.0 mm |
| Wera 334 | 1.2 × 6.5 mm slotted¹ | 150 mm | 36 mm | 25.0 mm |
| Wera 350 | PH 0 | 60 mm | 25 mm | 17.5 mm |
| Wera 350 | PH 1 | 80 mm | 32 mm | 22.5 mm |
| Wera 350 | PH 2 | 100 mm | 36 mm | 25.0 mm |
| Wera 350 | PH 3 | 150 mm | 40 mm | 28.0 mm |

¹ Originally listed as 1.2×5×150; corrected to 1.2×6.5×150 to match both
Craig's own handle measurement and Wera's official catalog variant
(part 05110010001).

- **Handle Ø** — measured by Craig with calipers (thickest point of the
  Kraftform grip, not the shaft/blade diameter — Wera's own spec sheets
  only publish the latter, which is far too small to be useful for pocket
  depth).
- **Pocket depth** — handle Ø × 70% rule, same as the Wera 454/7 tray,
  rounded to the nearest 0.5mm.
- **Finger notch depth: 28.0mm for all 7 tools** (not a per-tool value).
  ToolTrace enforces notch depth ≥ the deepest pocket in the design (28.0mm,
  the PH 3) *and* ≤ the same 28.0mm ceiling — so 28.0mm is the only value
  that satisfies both constraints, with no margin available above it.
- **Finger notch placement**: centered on the *end (tip) of the handle* for
  every tool, wrapping around the rounded end on three sides — not on the
  blade (too narrow to grip, and risks bending/scratching it) and not on
  the side of the handle (only exposes one flat edge, less useful for a
  pinch-and-lift than the rounded tip).

### Reference: Wera catalog specs

From Wera's own product pages (blade diameter here is the shaft, not the
handle — see note above):

| Tool | Blade Ø (shaft) | Handle length | Part number |
|------|-----------------|---------------|-------------|
| Wera 334, 0.8×5.0×100 | 5.0 mm | 98 mm | 05007610001 |
| Wera 334, 1.2×6.5×150 | 6.0 mm | 105 mm | 05110010001 |
| Wera 350 PH 0×60 | 3.0 mm | 81 mm | 05008705001 |
| Wera 350 PH 1×80 | 4.5 mm | 98 mm | 05008710001 |
| Wera 350 PH 2×100 | 6.0 mm | 105 mm | 05008720001 |
| Wera 350 PH 3×150 | 8.0 mm | 112 mm | 05008735001 |

(Wera 335 0.5×3.0 not confirmed against an exact catalog row.)

### Source photos → ToolTrace design

| Photo | Tools traced |
|-------|-------------|
| `flathead.jpeg` | Wera 335, Wera 334×100, Wera 334×150 (all 3, one photo) |
| `phillips.jpeg` | Wera 350 PH0, PH1, PH2, PH3 (all 4, one photo) |

Both photos traced into the same ToolTrace session (no Import Traces
needed — unlike the 454/7 job, all 7 tools ended up together directly).

### Layout

All 7 tools arranged on a **13u × 3u** grid (42mm pitch), split into
**3 plates**. ToolTrace's internal design name is "Green Screwdrivers"
(shows up in the split-STL `manifest.json`) even though the exported
files are prefixed `wera-phillips-flathead-*` — a naming quirk like the
454/7 job's "6.0x150" collection name; ignore it, it's not a dimension or
a hint about anything other than what the design happened to be named at
some point.

Each plate measures **182.04 × 126.03mm** (≈4.33u × 3u) — note this is
**not** a whole-number grid split (13 ÷ 3 = 4.33), unlike the 454/7 job's
plates, which were whole units (5u/4u). Worth knowing if these trays are
meant to dock into a shared Gridfinity baseplate layout later — the split
seams won't land exactly on 42mm grid lines. Craig reviewed the STEP/STL
in Bambu Studio and confirmed everything looks correct as exported, so
this is a documentation note rather than a problem to fix.

Tools are interleaved across the 3 plates rather than grouped by type, so
plate boundaries don't separate flathead from Phillips — color-coding
happens at the insert level instead (see Exports below), not per-plate.

### Exports

- `gridfinity/source/tooltrace/wera-phillips-flathead-screwdrivers/photos/`
  — `flathead.jpeg`, `phillips.jpeg`.
- `gridfinity/source/tooltrace/wera-phillips-flathead-screwdrivers/split-stl/`
  — 3 plates × {tray, inserts} STL pairs, plus `manifest.json`.
- `gridfinity/source/step/wera-phillips-flathead-screwdrivers/wera-phillips-flathead-screwdrivers-tray_v1.step`
  — STEP export of the whole combined design (not split per plate).

**Print plan for this project (differs from the 454/7 job, where only the
tray files were printed):** each plate's `*-tray.stl` is printed once
(one color, structural body). Each plate's `*-insert.stl` is printed
**twice — once per color** — since the insert sheet's individual
tool-shaped pieces need to end up color-coded by tip type once assembled.
After printing, hand-sort the insert pieces by shape (flathead vs.
Phillips) and drop the correct-color piece into each pocket. This
achieves the flathead/Phillips visual split at the insert level, since a
clean per-plate split isn't possible (each plate mixes both tool types).

---

## Status

- [x] All 7 tools photographed (2 photos: flathead.jpeg, phillips.jpeg)
- [x] All 7 tools traced in ToolTrace (Fast mode)
- [x] Laid out on a 13u × 3u grid, no overlap
- [x] Pocket depths set per tool (70%-of-handle-Ø rule)
- [x] Finger notches added per tool (28.0mm depth, handle-tip placement)
- [x] Split for Multiple Prints configured (3 plates)
- [x] STEP/STL exported and verified in Bambu Studio
- [x] Source photos, split-STL exports, and STEP copied into repo
- [ ] Trays sliced/printed (1 color, structural)
- [ ] Inserts sliced/printed twice (once per color)
- [ ] Insert pieces sorted by tool-head shape and matched into pockets
- [ ] Sliced `.3mf` saved to
      `gridfinity/3mf/wera-phillips-flathead-screwdrivers/`
- [ ] Printed
- [ ] STL archived to
      `gridfinity/stl/inserts/wera-phillips-flathead-screwdrivers/`
