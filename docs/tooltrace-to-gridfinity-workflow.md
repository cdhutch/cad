# Tool-Specific Gridfinity Tray Workflow (ToolTrace → Onshape → Bambu Studio)

A reproducible, step-by-step guide to the pipeline used for exact-fit tool
pockets (Allen wrenches, screwdrivers, anything with an irregular silhouette).
For simple rectangular bins/baseplates, don't use this — use a parametric
generator instead (see `docs/repo-conventions.md` and
`gridfinity/docs/naming.md`).

Written up while building the Wera 454/7 HF Set 1 tray
(`gridfinity/docs/wera-454-7-hf-set-1-tray.md`) — that doc has this project's
specific numbers; this doc is the general procedure.

---

## 1. Photograph the tools

- One sheet of **Letter (8.5×11") or A4 paper** per photo, laid flat, tool(s)
  on top — the paper is ToolTrace's scale reference, so it must be fully
  visible in frame with all 4 corners.
- Multiple tools *can* share one sheet/photo if they don't overlap — ToolTrace
  auto-detects each one separately. But tools from different photos can't be
  combined into one ToolTrace session at upload time (see step 3).
- Shoot top-down, as perpendicular to the paper as possible, in even lighting.
  **Avoid strong directional light** — cast shadows next to the tool can get
  traced as part of its silhouette (see step 6, cleanup).
- Export/save photos as **JPEG or PNG**. ToolTrace's HEIC decoding is
  unreliable server-side ("Failed to convert HEIC file") — convert HEIC
  photos before uploading (e.g. via Preview/Photos export, or
  `pillow-heif` if scripting it).

## 2. Measure/verify tool dimensions independently

Don't rely on the trace alone for critical dimensions — cross-check against
the manufacturer's datasheet and/or physical measurement:
- Watch for spec ambiguity (e.g. Wera's "10.0×200" is the *shaft* length only;
  the handle block adds on top of it — total tool length ≈ shaft + handle).
- A single WebFetch of a retailer product page can garble tables (columns
  merging, e.g. a "qty: 1" column bleeding into a size column) — if numbers
  look suspicious, fetch the manufacturer's PDF datasheet directly and
  cross-check.

## 3. Trace each photo in ToolTrace (tooltrace.ai)

- **New Tooltrace** → drag/browse one photo into the upload box. One photo =
  one ToolTrace session; there's no multi-photo upload into a single session.
- ToolTrace auto-detects and outlines the tool(s) on that sheet
  ("Tools were auto selected"). Use **Add Tool** only to trace an
  *additional* object ToolTrace missed on the *same* photo — it does not let
  you add a second photo to the session.
- Rename the session immediately (the `Name` field, top-left) to something
  identifiable — default names are generic/auto-generated (e.g. "Black Wera
  Tool") and easy to confuse with leftover sessions from earlier work.
- Repeat for each photo — one ToolTrace session per sheet.

## 4. Combine traces into one design

- In whichever session will become your final combined design (or a fresh
  one), go to the **Layout** step → **Import Tools** → this opens
  **Import Traces**, a picker listing your *other* ToolTrace sessions and
  their traced tool outlines.
- Check the specific tool outline(s) you want from each source session, then
  **Import N Traces**. Repeat/re-open as needed.
- **Gotchas:**
  - Leftover/stray sessions from past work can appear in this picker with
    generic names identical to what a fresh session would auto-name itself —
    double check thumbnails/dates before selecting, to avoid importing a
    duplicate of a tool you already have.
  - Clicking a tool's **×** in the right-hand Tools panel deletes it
    immediately with no confirmation. If you delete the wrong one, just
    re-open Import Traces and pull it back in (nothing is lost as long as
    the source session still exists).

## 5. Configure per-tool settings

Still in the **Layout** step, for each tool:
- **Pocket Depth** — click the tool to open its detail card; default is
  20.0mm, editable per tool.
- **Offset** (left panel, "Traces" section) — None/Small/Medium/Large
  clearance added around the traced outline. Medium is a reasonable default
  for a hand-inserted tool pocket.
- **Finger Notch** (Add Simple Shapes) — add one near each tool's handle so
  there's room to pinch and lift it out. Don't try to fake this with extra
  offset margin — the dedicated shape is cleaner and independently
  positionable.

## 6. Arrange and clean up

- ToolTrace's Layout canvas is **manual drag/rotate only** — there is no
  auto-nest or auto-arrange. It snaps to the grid and shows live size
  feedback (mm), and at 100% zoom the canvas is ~1:1 px:mm, but for a tight
  interlocking nest of many irregular shapes, **do the precise placement in
  Onshape instead** (numeric transforms, exact boolean splitting along plate
  boundaries) — use ToolTrace just to get clean individual offset outlines.
- **Check every traced outline for shadow artifacts** before treating it as
  final geometry — a cast shadow next to the tool in the source photo can
  get included in the silhouette, usually visible as an extra bump or
  elongation at one end. Clean these up in Onshape (trim back to the true
  tool edge) rather than trying to fix the trace itself.

## 7. Export from ToolTrace

- **Download → STEP** (also available: SVG, DXF, STL, 3MF, PDF).
- The export contains one solid per tool **plus an auto-generated
  baseplate/background solid** sized to the current layout's bounding box —
  discard that extra solid in CAD; you'll build your own tray body.
- Tool solids are thin (~0.5mm) flat "stamp" extrusions — 2D profiles meant
  to be re-extruded to your chosen pocket depth in CAD, not pre-cut cavities.
- Archive the STEP under
  `gridfinity/source/step/<project-name>/<descriptive-name>_v<n>.step`
  (tracked via Git LFS — see `.gitattributes`).

## 8. Onshape: import, clean, nest, model

1. **Import** the STEP into a new (or existing) Part Studio.
2. **Discard** the auto-generated baseplate solid from step 7.
3. **Clean up** each tool profile: trim shadow-elongated edges back to the
   true silhouette, verify dimensions against your independently-measured
   values from step 2 (traced bounding boxes can retain a slight rotation
   from the source photo angle, so don't assume axis-aligned = true
   length/width without checking).
4. **Nest** the cleaned profiles at exact coordinates, respecting your
   printer's practical build-plate cap in Gridfinity units (e.g. a 256mm-cube
   printer → 6×6 grid units = 252×252mm per plate). If everything doesn't
   fit on one plate, group tools into multiple plates and note the split.
5. **Extrude** a Gridfinity tray body per plate and **boolean-subtract** the
   tool pockets + finger notches.
6. Apply the **standard Gridfinity bin-bottom interface** (lip, 42mm grid,
   optional magnet pockets) — use the repo's usual approach (custom feature
   or generator) rather than hand-modeling it.
7. **Export STL** per plate → `gridfinity/stl/inserts/<project-name>/`.
8. Record the Onshape document link in `gridfinity/source/onshape/links.md`.

## 9. Bambu Studio: slice and save

1. Import the STL(s).
2. Use the **"Gridfinity Tray - Light"** process preset
   (`gridfinity/docs/gridfinity-tray-light.json` /
   `gridfinity/docs/bambu-tool-tray-profile.md`) — tuned for low-strength,
   gravity-load-only tool trays: minimal infill, fast print, no brim.
3. Save the sliced **project** as `.3mf` (not "export sliced file" — that
   embeds gcode and bloats the file) →
   `gridfinity/3mf/<project-name>/<descriptive-name>_v<n>.3mf`.
4. Print, test-fit, and update the project doc's Status checklist.

---

## Lessons learned (things that went wrong or wasted time)

- Don't assume a retailer product page's parsed dimensions are correct —
  cross-check against the manufacturer's own PDF datasheet.
- Don't assume a "shaft length" spec is the tool's total length — check
  whether the handle/grip adds to it.
- HEIC photos will silently fail server-side in ToolTrace — convert first.
- A combined multi-tool STEP export's solids can look confusingly similar in
  size if photographed/traced at a slight rotation — verify real dimensions
  in CAD rather than trusting a bounding-box readout at face value.
- ToolTrace has no bin-packing/auto-nest solver — don't spend time trying to
  get a tight interlocking layout by dragging in its Layout canvas; move to
  Onshape for anything beyond "make sure nothing overlaps."
