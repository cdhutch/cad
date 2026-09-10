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

- [x] Milwaukee driver bit set — combined into one tray with the stud
      finder, see below
- [x] Wall stud finder — combined into one tray with the driver bit set,
      see below
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

## Milwaukee Driver Bit Set + Wall Stud Finder

Both are essentially rectangular boxes standing upright, ~2.5" (63.5mm)
tall, each reaching its largest footprint within 1cm of the bottom. Unlike
the round-handled Wera tools, pocket depth here isn't a percentage of a
handle diameter — it just needs to be deep enough to capture the widest
part of the base and hold the item from tipping/sliding, no deeper.

- **Pocket depth: 10mm for both** (matching the "largest footprint within
  1cm of the bottom" — going deeper wastes material/print time since
  nothing wider comes back into contact above that).
- **No finger notches** — both items stand ~53.5mm proud of the tray
  surface above their pockets, plenty to grab directly.
- **Layout**: single tray, roughly 6u × 6u × 3u (251.5 × 251.5 × 21.17mm
  measured directly from the exported STL) — no Split for Multiple Prints
  needed at this size.

### Export note

This export came out of ToolTrace as 3 separate STL bodies rather than the
usual tray+inserts pair — worth knowing since it doesn't match the naming
pattern from the Wera projects:
- `body_3.stl` — the actual tray, with the Gridfinity bottom interface and
  both tool cutouts. This is the one kept/archived/printed.
- `body_1.stl`, `body_2.stl` — flat 0.5mm-thick reference "stamps" of each
  tool's outline (not real 3D geometry, not usable for printing).
  **Discarded**, not copied into the repo.

### Files

- `gridfinity/source/tooltrace/misc-handtools/red-milwaukee-toolbox-and-stud-finder/`
  — `photos/Milwaukee drill bits and stud finder.jpeg`, and
  `red-milwaukee-toolbox-and-stud-finder-tray.stl` (renamed from
  ToolTrace's `body_3.stl`).
- `gridfinity/source/step/misc-handtools/red-milwaukee-toolbox-and-stud-finder/red-milwaukee-toolbox-and-stud-finder-tray_v1.step`

(Note: Craig's original Downloads filenames used "stub-finder" — corrected
to "stud-finder" in the repo, matching the actual item.)

**Status:** exported, not yet verified in Bambu Studio or printed.
