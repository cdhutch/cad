# Misc Hand Tools Trays — Design Notes

A lighter-weight, running project for odds-and-ends hand tools that don't
belong to a single branded set — unlike the Wera tray projects, this one
doesn't get a full separate doc/folder per item. Built with ToolTrace.ai's
native "Gridfinity" export mode — see
`docs/tooltrace-to-gridfinity-workflow.md` (Part 1) for the general,
reusable procedure.

Each item (or small group of items) below gets its own subsection as it's
worked on — not necessarily its own ToolTrace design or print plate;
group items together in one design when their sizes/shapes make sense to
lay out together, and keep them separate when they don't.

---

## Item queue

- [x] Milwaukee driver bit set — its own tray (see below; originally
      combined with the stud finder, split apart after a print failure)
- [x] Wall stud finder — its own tray (see below; same split)
- [x] DeWalt drill bit sets (both boxes) — combined into one tray
- [x] Current (voltage) detector — Klein Tools NCVT-1P
- [x] Small electronics tool set — Hyper Tough 77-Piece Electronic Repair Kit
- [x] Kobalt tape measure — Kobalt 25' Self-Lock Tape Measure

---

## Exports

Source photos, STEP, and STL exports land under
`gridfinity/source/tooltrace/misc-handtools/<item-group>/` and
`gridfinity/source/step/misc-handtools/<item-group>/`, one subfolder per
item/group (rather than the flat photos/split-stl/ layout used by the
single-design Wera projects), since items here get combined into trays in
different groupings — same idea, just organized per-group instead of
flat. Finished trays are archived to `gridfinity/stl/inserts/<item-group>/`
(dimensioned filename) and `gridfinity/3mf/<item-group>/` (sliced Bambu
Studio project), one top-level folder per item/group — same split as every
other project in this repo, not nested under a shared `misc-handtools/`
folder at that stage.

---

## Print lesson: avoid a 6-unit Y dimension on the Gridfinity grid

The original combined Milwaukee box + stud finder tray (6u × 6u footprint)
had to be redone after a print failure. Craig's diagnosis: Gridfinity
grids with a **Y dimension of 6 units tend to fail** — the base is printed
as a series of disjoint square pads (gaps between them, not one continuous
first-layer perimeter), and the printer's calibration/nozzle-wipe routine
near the front (near-Y) edge of the plate collided with the first layer or
two.

I don't have independent confirmation this is a documented/named Bambu or
Gridfinity issue — I don't recognize it from anything I know — but the
mechanism is plausible: a non-continuous first layer near where a
calibration pass runs is a believable collision risk. Treat this as an
observed lesson from this project, not a verified general rule, unless it
recurs on future trays.

**Practical fix used**: split the combined tray into two separate,
smaller single-item prints instead, each avoiding a 6u Y dimension and
avoiding the near side of the build plate.

**Update**: on the electronics kit and combined drill-bit-set trays
(both 4u × 6u), Craig found that a 6u Y dimension is fine to print as
long as it isn't paired with a 6u X dimension too (i.e. avoid a 6u × 6u
footprint specifically) — a 4u × 6u tray can just be rotated on the plate
to keep clear of the near-Y edge issue above. So the practical rule is
narrower than originally stated: avoid **6u × 6u**, not any 6u dimension
on its own.

## Trace offset for rougher tool outlines

For the tape measure, voltage tester, electronics kit, and drill-bit-set
trays, Craig set ToolTrace's **Trace Offset to Small** rather than the
default — these tools' overall dimensions traced a bit rougher (less
precise/consistent edges) than earlier projects, and the smaller offset
tightened the fit back up. Worth trying first if a future tool's trace
looks noticeably imprecise.

## Milwaukee Driver Bit Set (own tray)

Rectangular box standing upright, ~2.5" (63.5mm) tall, reaching its
largest footprint within 1cm of the bottom.

- **Pocket depth: 10mm** (matching the "largest footprint within 1cm of
  the bottom" — no deeper, since nothing wider comes back into contact
  above that).
- **No finger notch** — stands ~53.5mm proud of the tray surface above
  its pocket, plenty to grab directly.
- **Layout**: single tray, ~6u × 3u × 3u (251.56 × 125.53 × 21.17mm
  measured directly from the exported STL).

### Files

- `gridfinity/source/tooltrace/misc-handtools/red-milwaukee-box/` —
  `photos/Milwaukee drill bits and stud finder.jpeg`,
  `red-milwaukee-box-tray.stl` (renamed from ToolTrace's `body_2.stl` —
  `body_1.stl`, a flat 0.5mm reference stamp, discarded as before).
- `gridfinity/source/step/misc-handtools/red-milwaukee-box/red-milwaukee-box-tray_v1.step`
- `gridfinity/stl/inserts/red-milwaukee-box/red-milwaukee-box-tray_6x3x3u_v1.stl`
- `gridfinity/3mf/red-milwaukee-box/red-milwaukee-box-tray_6x3x3u_v1.3mf`

**Status:** printed.

## Wall Stud Finder (own tray)

Rectangular box standing upright, ~2.5" (63.5mm) tall, reaching its
largest footprint within 1cm of the bottom.

- **Pocket depth: 10mm.**
- **No finger notch.**
- **Layout**: single tray, ~5u × 3u × 3u (209.55 × 125.53 × 21.17mm
  measured directly from the exported STL).

### Files

- `gridfinity/source/tooltrace/misc-handtools/stud-finder/` —
  `photos/Milwaukee drill bits and stud finder.jpeg`,
  `stud-finder-tray.stl` (renamed from ToolTrace's `body_2.stl` —
  `body_1.stl` discarded as before).
- `gridfinity/source/step/misc-handtools/stud-finder/stud-finder-tray_v1.step`
- `gridfinity/stl/inserts/stud-finder/stud-finder-tray_5x3x3u_v1.stl`
- `gridfinity/3mf/stud-finder/stud-finder-tray_5x3x3u_v1.3mf`

(Note: Craig's original Downloads filenames used "stub-finder" — corrected
to "stud-finder" in the repo, matching the actual item.)

**Status:** printed.

## Kobalt 25' Self-Lock Tape Measure (own tray)

Blue Kobalt 25' Self-Lock Tape Measure, own single-item tray.

- **Pocket depth: 10mm.**
- **No finger notch.**
- **Layout**: single tray, ~3u × 3u × 3u (125.50 × 125.50 × 21.17mm
  measured directly from the exported STL).

### Files

- `gridfinity/source/tooltrace/misc-handtools/kobalt-25ft-tape-measure/` —
  `photos/Kobalt tape measure.jpeg`, `kobalt-25ft-tape-measure-tray.stl`
  (renamed from ToolTrace's `body_2.stl` — `body_1.stl` discarded).
- `gridfinity/source/step/misc-handtools/kobalt-25ft-tape-measure/kobalt-25ft-tape-measure-tray_v1.step`
- `gridfinity/stl/inserts/kobalt-25ft-tape-measure/kobalt-25ft-tape-measure-tray_3x3x3u_v1.stl`
- `gridfinity/3mf/kobalt-25ft-tape-measure/kobalt-25ft-tape-measure-tray_3x3x3u_v1.3mf`

**Status:** printed.

## Klein Tools NCVT-1P Voltage Tester (own tray)

Current (voltage) detector, own single-item tray. Shares its source photo
with the electronics kit below (photographed together).

- **Pocket depth: 10mm.**
- **No finger notch.**
- **Layout**: single tray, ~4u × 1u × 3u (167.50 × 41.50 × 21.17mm
  measured directly from the exported STL).

### Files

- `gridfinity/source/tooltrace/misc-handtools/klein-ncvt1p-voltage-tester/`
  — `photos/Current detector and small tool set.jpeg`,
  `klein-ncvt1p-voltage-tester-tray.stl` (renamed from ToolTrace's
  `body_2.stl` — `body_1.stl` discarded).
- `gridfinity/source/step/misc-handtools/klein-ncvt1p-voltage-tester/klein-ncvt1p-voltage-tester-tray_v1.step`
- `gridfinity/stl/inserts/klein-ncvt1p-voltage-tester/klein-ncvt1p-voltage-tester-tray_4x1x3u_v1.stl`
- `gridfinity/3mf/klein-ncvt1p-voltage-tester/klein-ncvt1p-voltage-tester-tray_4x1x3u_v1.3mf`

**Status:** printed.

## Hyper Tough 77-Piece Electronic Repair Kit (own tray)

Small electronics tool set, own single-item tray. Shares its source photo
with the voltage tester above (photographed together).

- **Pocket depth: 10mm.**
- **No finger notch.**
- **Layout**: single tray, ~4u × 6u × 3u (167.50 × 251.50 × 21.17mm
  measured directly from the exported STL). See the 6u-Y-dimension note
  above — printed fine once not paired with a 6u X dimension.

### Files

- `gridfinity/source/tooltrace/misc-handtools/hypertough-77pc-electronics-kit/`
  — `photos/Current detector and small tool set.jpeg`,
  `hypertough-77pc-electronics-kit-tray.stl` (renamed from ToolTrace's
  `body_2.stl` — `body_1.stl` discarded).
- `gridfinity/source/step/misc-handtools/hypertough-77pc-electronics-kit/hypertough-77pc-electronics-kit-tray_v1.step`
- `gridfinity/stl/inserts/hypertough-77pc-electronics-kit/hypertough-77pc-electronics-kit-tray_4x6x3u_v1.stl`
- `gridfinity/3mf/hypertough-77pc-electronics-kit/hypertough-77pc-electronics-kit-tray_4x6x3u_v1.3mf`

**Status:** printed.

## DeWalt Drill Bit Sets (combined tray)

Both DeWalt drill bit boxes, combined into one tray (single ToolTrace
design, two tool stamps + one finished tray in the export — same pattern
as the original combined Milwaukee/stud-finder export).

- **Pocket depth: 10mm** (both boxes).
- **No finger notch.**
- **Layout**: single tray, ~4u × 6u × 3u (167.54 × 251.56 × 21.17mm
  measured directly from the exported STL). See the 6u-Y-dimension note
  above.

### Files

- `gridfinity/source/tooltrace/misc-handtools/dewalt-drill-bit-sets/` —
  `photos/Dewalt drill bit sets.jpeg`, `dewalt-drill-bit-sets-tray.stl`
  (renamed from ToolTrace's `body_3.stl` — `body_1.stl`/`body_2.stl`,
  flat 0.5mm reference stamps, discarded).
- `gridfinity/source/step/misc-handtools/dewalt-drill-bit-sets/dewalt-drill-bit-sets-tray_v1.step`
- `gridfinity/stl/inserts/dewalt-drill-bit-sets/dewalt-drill-bit-sets-tray_4x6x3u_v1.stl`
- `gridfinity/3mf/dewalt-drill-bit-sets/dewalt-drill-bit-sets-tray_4x6x3u_v1.3mf`

**Status:** printed.

## Superseded

The original combined `red-milwaukee-toolbox-and-stud-finder` tray
(6u × 6u, single print) was replaced by the two separate trays above and
removed from the repo — see git history if needed.
