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
- [ ] DeWalt drill bit set #1
- [ ] DeWalt drill bit set #2
- [ ] Current (voltage) detector
- [ ] Small electronics tool set
- [ ] Kobalt tape measure

---

## Exports

Source photos, STEP, and STL exports land under
`gridfinity/source/tooltrace/misc-handtools/<item-group>/` and
`gridfinity/source/step/misc-handtools/<item-group>/`, one subfolder per
item/group (rather than the flat photos/split-stl/ layout used by the
single-design Wera projects), since items here get combined into trays in
different groupings — same idea, just organized per-group instead of
flat.

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

**Status:** exported, not yet verified in Bambu Studio or printed.

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

(Note: Craig's original Downloads filenames used "stub-finder" — corrected
to "stud-finder" in the repo, matching the actual item.)

**Status:** exported, not yet verified in Bambu Studio or printed.

## Superseded

The original combined `red-milwaukee-toolbox-and-stud-finder` tray
(6u × 6u, single print) was replaced by the two separate trays above and
removed from the repo — see git history if needed.
