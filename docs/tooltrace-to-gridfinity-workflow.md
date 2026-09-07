# Tool-Specific Gridfinity Tray Workflow (ToolTrace → Gridfinity)

A reproducible, step-by-step guide to building exact-fit tool pockets (Allen
wrenches, screwdrivers, anything with an irregular silhouette).

**Default path: ToolTrace's own native "Gridfinity" export** (Part 1 below)
— trace, lay out, and export STEP/STL directly from ToolTrace, with no CAD
step in between. Use this unless your layout needs something ToolTrace's
manual drag/rotate Layout canvas can't do — namely a **tight interlocking
nest** that packs irregular shapes tighter than simple non-overlapping grid
placement, to minimize wasted Gridfinity squares. For that case, fall back
to the Onshape path (Part 2).

Written up while building the Wera 454/7 HF Set 1 tray
(`gridfinity/docs/wera-454-7-hf-set-1-tray.md`) — that doc has this
project's specific numbers; this doc is the general procedure.

---

## Part 1: ToolTrace-native path (default)

### 1. Photograph the tools

- Shoot on a plain, high-contrast, colored background (cleaner trace than
  paper/white) or on one sheet of Letter/A4 paper with all 4 corners
  visible if you need ToolTrace's paper-based scale calibration instead.
- Multiple tools can share one photo, but every tool must be fully
  separated from the others — no touching/overlapping outlines, and no
  tool touching the edge of the page/background (a trace touching the edge
  can fuse into the background boundary).
- Shoot from further away and zoom in (physically or in-camera) rather than
  filling the frame at close range — reduces lens distortion at the edges
  of the photo, which otherwise skews the traced outline.
- Even, shadow-free lighting — a cast shadow next to the tool can get
  traced as part of its silhouette.
- Include a calibration reference (ruler, checkerboard, or known-size
  object) in frame for ToolTrace's corner-calibration step.
- Export/save as **JPEG or PNG** — ToolTrace's HEIC decoding is unreliable
  server-side ("Failed to convert HEIC file"); convert HEIC photos first.

### 2. Measure/verify tool dimensions independently

Don't rely on the trace alone for critical dimensions — cross-check against
the manufacturer's datasheet and/or physical measurement:
- Watch for spec ambiguity (e.g. Wera's "10.0×200" is the *shaft* length
  only; the handle block adds on top of it — total tool length ≈ shaft +
  handle).
- A single WebFetch of a retailer product page can garble tables (columns
  merging, e.g. a "qty: 1" column bleeding into a size column) — if numbers
  look suspicious, fetch the manufacturer's PDF datasheet directly and
  cross-check.

### 3. Trace each photo in ToolTrace

- One photo = one ToolTrace session/design; there's no multi-photo upload
  into a single session.
- **Mode: Fast vs. Detail** — set this before adding any tool; it cannot be
  changed on a tool after it's added (changing it loses the tool and it
  must be re-added).
  - **Detail mode** segments by apparent contiguous color/material region.
    On a multi-material tool (e.g. matte handle + shiny metal shaft) this
    fragments the tool into multiple disconnected pieces instead of one
    outline.
  - **Fast mode** grabs the whole tool silhouette in a single click. Less
    precise on fine contour detail, but doesn't fragment multi-material
    tools. **Use Fast mode for tools with a handle + metal shaft**
    (T-handles, screwdrivers, etc.).
- Rename the session immediately (the `Name` field) — default names are
  generic/auto-generated and easy to confuse with leftover sessions from
  earlier work.
- Click each tool to trace it, name it, and — critically — **click OK to
  confirm the trace**. A trace that is never confirmed with OK does not
  persist: reopening the design will show the bare photo with no
  AI-selected tool, and the tool will not appear in Import Traces from
  other designs.

### 4. Fix bad traces with Fine Tune

If an exported STEP/STL later comes out looking inverted or corrupted, go
back to the Layout step's **Fine Tune** tool and manually smooth the
offending outline. A hand-traced curve can contain a "sketch singularity"
— a self-intersecting loop or an acute/degenerate point — that blows up
the boolean subtraction used to generate the pocket, producing a solid
tool-shaped plug instead of a recessed pocket. Fine Tune lets you clean up
the outline without re-tracing from scratch.

### 5. Combine traces from multiple designs with Import Traces

- If your tools are spread across several photos/designs, open the design
  you want to build the final tray in and use **Import Traces** (button
  labeled "Import Tools") to pull in already-traced, OK-confirmed tools
  from your other ToolTrace designs.
- Imported tools show `Source: Imported` in their tool popup (Mode/Enforce
  Symmetry/Angle aren't shown — those only apply at trace time — but
  Pocket Depth remains editable). A generic "Imported" placeholder instead
  of a live thumbnail appears to be cosmetic, not a failed import.
- **Gotchas:**
  - Leftover/stray sessions from past work can appear in the import picker
    under similarly generic auto-generated names — double-check
    thumbnails/dates before selecting, to avoid importing a duplicate.
  - Clicking a tool's **×** in the Tools panel deletes it immediately with
    no confirmation. If this happens by accident, re-import it via Import
    Traces from its original session rather than re-tracing.

### 6. Lay out the tools

- Arrange all tools in the workspace with no overlap. Freshly
  imported/added tools may all appear superimposed at first — drag them
  apart manually.
- ToolTrace's Layout canvas is **manual drag/rotate only** — no auto-nest
  or auto-arrange. It snaps to the grid and shows live size feedback (mm).
  This is fine for "arrange without overlap"; it is **not** the tool for a
  tight interlocking nest that minimizes wasted grid squares — for that,
  use the Onshape path (Part 2) instead.
- Use **Add Simple Shapes → Finger Notch** to add a finger-access scallop
  to any pocket you'll need to pinch a tool out of: a circle with a live,
  draggable diameter. Position it straddling the edge of the pocket. Set
  its depth **deeper than the pocket it's attached to** (retrieval is
  handled by the notch reaching below the tool, not by the pocket itself).
- Other shapes here (Circle, Square, Rectangle, Rounded Rect, Text) are for
  labels/general cutouts, not tool-specific.

### 7. Size and export in the Design step

- **Pocket Depth** (per tool, via each tool's popup) — set individually.
  Rule of thumb: ≈70% of the tool's own handle/crossbar thickness (not the
  hex bit or fastener diameter), leaving ≥2–3mm of base material below the
  pocket floor.
- **Customize Overall Size → Grid Length/Grid Width** — tray footprint in
  Gridfinity grid units (1 unit = 42mm). Pick even numbers so a grid cell
  isn't split across a design boundary — though it would still print fine.
- **Custom Grid Size** — set to **42mm** for standard Gridfinity pitch.
- **Split for Multiple Prints** — subdivides a layout larger than your
  printer's bed into multiple plates, each no larger than a size you
  specify (e.g. 252×252mm = 6×6 units). If a tool's pocket exceeds one
  plate, ToolTrace deliberately splits it across the shared edge of two
  adjacent plates — intentional, not a bug: the pocket halves align once
  the printed plates sit next to each other.
- **Puzzle Piece Mode** (GRIDFINITY panel) — trims empty grid cells so the
  printed outline hugs the tool shapes instead of a full rectangle.
  Separate from, and combinable with, Split for Multiple Prints.
- **Lip Design** (Default/None) and **Base magnets** (None/Corner/Full) —
  standard Gridfinity bin-bottom options.
- **Type must stay "Gridfinity"**, not "Foam" — Foam mode is believed to
  export a solid cutter/tool-shaped body rather than a tray with a
  recessed pocket; check this first if an export ever looks inverted.
- Export **STEP and/or STL**. STEP exports the whole design as one file
  (not split per plate — the plate split is a print-file concept). For a
  split layout, the STL export is a ZIP containing one **tray** STL + one
  **inserts** STL per plate, plus a `manifest.json` with each plate's
  position/size. **Only the tray STL is printed** — load one tray STL per
  plate into Bambu Studio, one print job at a time; the inserts file isn't
  sent to the printer.

### 8. Verify before printing

ToolTrace's own in-browser 3D preview can be unreliable to read — it has
been observed rendering one view for a few seconds and switching to
another, and pocket depths can look visually deceptive (a very deep value
on one tool makes every other tool look shallow by comparison). For a
trustworthy check, load the exported STEP/STL into Bambu Studio (or
Onshape) and inspect it there directly.

### 9. Slice and print

1. Import the STL(s) into Bambu Studio.
2. Use the **"Gridfinity Tray - Light"** process preset
   (`gridfinity/docs/gridfinity-tray-light.json` /
   `gridfinity/docs/bambu-tool-tray-profile.md`) — tuned for low-strength,
   gravity-load-only tool trays: minimal infill, fast print, no brim.
3. Save the sliced **project** as `.3mf` (not "export sliced file" — that
   embeds gcode and bloats the file) →
   `gridfinity/3mf/<project-name>/<descriptive-name>_v<n>.3mf`.
4. Archive source files: STEP/STL/photos under
   `gridfinity/source/tooltrace/<project-name>/` and
   `gridfinity/source/step/<project-name>/` (Git LFS tracks `*.stl`,
   `*.3mf`, `*.step`, `*.stp`, `*.dxf`).
5. Print, test-fit, and update the project doc's Status checklist.

---

## Part 2: Onshape path (fallback / advanced)

Use this instead of Part 1 only when you need a **tight interlocking nest**
that packs irregular tool shapes tighter than simple non-overlapping grid
placement (minimizing total Gridfinity squares consumed across however many
plates are needed), or when ToolTrace's native export produces geometry you
need to hand-repair in real CAD.

**Known reliability risk:** DXF import into Onshape has repeatedly dropped
or corrupted tool geometry on this repo's projects — a tool trace touching
the edge of its source photo/paper gets fused with the page boundary into
one degenerate closed loop that isn't cleanly separable back into a usable
outline (confirmed via DXF entity/geometry analysis with Python `ezdxf`).
This is why the Wera 454/7 HF Set 1 tray was rebuilt on the Part 1 path
after starting here. If you hit this, prefer the STL fallback procedure
below over DXF, or switch to Part 1 entirely if your layout doesn't
actually need interlocking nesting.

### Steps

1. **Trace each photo in ToolTrace** — same as Part 1, steps 1–3, but you
   only need clean individual tool outlines; you don't need to combine,
   lay out, or export a finished design from ToolTrace at all.
2. **Export from ToolTrace: Download → STEP** (also available: SVG, DXF,
   STL, 3MF, PDF).
   - The export contains one solid per tool **plus an auto-generated
     baseplate/background solid** sized to the layout's bounding box —
     discard that extra solid in CAD.
   - Tool solids are thin (~0.5mm) flat "stamp" extrusions — 2D profiles
     meant to be re-extruded to your chosen pocket depth in CAD, not
     pre-cut cavities.
   - Archive the STEP under
     `gridfinity/source/step/<project-name>/<descriptive-name>_v<n>.step`.
3. **Import into Onshape**: new/existing Part Studio → discard the
   auto-generated baseplate solid → clean up each tool profile (trim any
   shadow-elongated edges back to the true silhouette; verify dimensions
   against your independently-measured values from step 2 of Part 1 —
   traced bounding boxes can retain a slight rotation from the source
   photo angle).
4. **Nest** the cleaned profiles at exact coordinates, respecting your
   printer's practical build-plate cap in Gridfinity units (e.g. a
   256mm-cube printer → 6×6 grid units = 252×252mm per plate). Group tools
   into multiple plates if needed and note the split.
5. **Extrude** a Gridfinity tray body per plate and **boolean-subtract**
   the tool pockets + finger notches.
6. Apply the **standard Gridfinity bin-bottom interface** (lip, 42mm grid,
   optional magnet pockets) — use the repo's usual approach (custom
   feature or generator) rather than hand-modeling it.
7. **Export STL** per plate → `gridfinity/stl/inserts/<project-name>/`.
8. Record the Onshape document link in `gridfinity/source/onshape/links.md`.
9. Slice and print — same as Part 1, step 9.

### STEP import can hang forever — STL fallback procedure

STEP import into Onshape can get stuck at **"Post-processing..."**
indefinitely (not just slow) for a given file — confirmed by two separate
full-import attempts (default "Import to this document" mode, then
"Combine to a single Part Studio" mode) that both stalled identically for
10+ minutes, with Onshape's own status page showing "All Systems
Operational" at the time. If a STEP import is still stuck after several
minutes, cancel and fall back to STL:

1. **Export STL instead of STEP** from ToolTrace (Download → STL). This
   zips **one file per solid body** (`body_1.stl`, `body_2.stl`, ... one
   per tool, plus one for the auto-generated baseplate). Discard the
   baseplate STL (largest file by far).
2. **Upload all the tool STLs to Onshape in one batch** (drag/drop or the
   file picker takes multiple files at once).
3. In the **Units** dropdown of the import dialog, change it to
   **Millimeter** — Onshape's STL importer defaults to Inch, so ToolTrace's
   mm-based exports come in 25.4× oversized otherwise. (Shortcut: focus the
   dropdown and press "m" twice — first press selects Meter, second
   cycles to Millimeter.) Leave "Create a composite part when importing
   multiple or non-solid bodies" unchecked if you want each tool as an
   independently-positionable part later.
4. Unlike STEP import, the STL import dialog has no "combine to a single
   Part Studio" option — each STL becomes its own Part Studio tab, plus one
   extra raw "CAD Imports" tab. Consolidate them yourself (next step).
5. **Consolidate into one working Part Studio using the "Derived" feature**
   (Search Tools → "derive", not on the default toolbar): in your target
   Part Studio, Search Tools → Derived → "Select Part Studio..." → pick a
   source tab → confirm. Repeat once per source tab.
   - **Copy/paste of parts between Part Studio tabs is unreliable** in this
     workflow — use Derived instead.
   - On a Mac, use **Cmd+click** (not Ctrl+click, not Shift+click) for
     additive multi-select in a feature/parts tree — Ctrl+click triggers
     macOS's native right-click instead.
6. **A body can import as open Surfaces instead of a solid Part** — a real
   mesh defect (missing wall/side geometry), not a cosmetic glitch. Onshape
   has no "Stitch" feature; the closest equivalent, Boolean Union, can't
   bridge an actual gap between disconnected surface patches (it reports
   "Boolean resulted in no geometry change" on a genuinely gapped pair).
   - **Diagnose first**: view the *original* (pre-Derived) Part Studio for
     that body from an orthographic side view. If it renders as a
     razor-thin line with no visible depth, the STL never had real wall
     geometry in that direction — don't hand-patch it; re-trace/re-export
     that one tool from ToolTrace instead, or rebuild it manually from its
     2D outline plus known real-world dimensions.

---

## Lessons learned (things that went wrong or wasted time)

General (apply to either path):
- Don't assume a retailer product page's parsed dimensions are correct —
  cross-check against the manufacturer's own PDF datasheet.
- Don't assume a "shaft length" spec is the tool's total length — check
  whether the handle/grip adds to it.
- HEIC photos will silently fail server-side in ToolTrace — convert first.
- A trace that's never confirmed with OK doesn't persist, and won't show
  up later in Import Traces — always click OK.
- A sketch singularity (self-intersecting loop) in a hand-traced outline
  can corrupt the boolean subtraction and invert the export — use Fine
  Tune to clean it up rather than re-tracing from scratch.
- Detail mode fragments multi-material tools (matte handle + shiny metal
  shaft) into disconnected pieces — use Fast mode for those.

Onshape path only:
- DXF import into Onshape has repeatedly dropped/fused tool geometry on
  this repo's projects, especially when a trace touches the source
  photo/paper edge — prefer the STL fallback over DXF, or use the
  ToolTrace-native path (Part 1) if your layout doesn't need interlocking
  nesting.
- ToolTrace has no bin-packing/auto-nest solver — don't try to get a tight
  interlocking layout by dragging in its Layout canvas; that's what
  Onshape nesting is for.
- A combined multi-body STEP import into Onshape can hang at
  "Post-processing..." forever, not just slowly — if stuck more than a few
  minutes with no Onshape outage reported, stop waiting and fall back to
  STL.
- Onshape's STL importer defaults Units to Inch, not Millimeter — always
  check/change this before importing a ToolTrace STL (mm) or everything
  comes in 25.4× oversized.
- Copy/paste of parts between Part Studio tabs is unreliable — use the
  Derived feature to consolidate multiple Part-Studio imports instead.
- On a Mac, use Cmd+click (not Ctrl+click, not Shift+click) for additive
  multi-select in Onshape's feature/parts tree.
- Onshape has no "Stitch" feature — a side-by-side orthographic view
  showing no real depth at all means the source mesh is missing geometry
  that can't be patched by hand; re-trace/re-export that tool instead.
