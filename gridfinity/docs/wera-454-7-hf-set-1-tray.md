# Wera 454/7 HF Set 1 Hex Driver Tray — Design Notes

Gridfinity tray for the Wera 454/7 HF Set 1 (7-piece T-handle Hex-Plus hex
driver set: 2.5, 3, 4, 5, 6, 8, 10 mm). Built entirely with **ToolTrace.ai's
native "Gridfinity" export mode** — trace, lay out, and export STEP/STL
directly from ToolTrace, with no DXF import or Onshape boolean-subtract step.

This supersedes the DXF → Onshape workflow used for earlier trays (see
`wera-electrical-screwdrivers-tray.md`, `allen-wrench-tray.md`). That route
was abandoned for this job after repeated DXF-import failures — see
"Why not the Onshape DXF/STEP route" below.

---

## General Process: ToolTrace's native Gridfinity workflow

This section is written to be reproducible for the next tool set.

### 1. Photograph the tools

- One photo can hold multiple tools, but every tool in it must be fully
  separated from the others — no touching or overlapping outlines, and no
  tool touching the edge of the page/background (ToolTrace's trace can fuse
  a tool outline into the background boundary if it touches the edge).
- Shoot on a plain, high-contrast, colored background — this makes the trace
  outline much cleaner than a paper/white background.
- Shoot from further away and zoom in (physically or in-camera), rather than
  filling the frame at close range — this reduces lens distortion at the
  edges of the photo, which otherwise skews the traced outline.
- Avoid shadows — flat, even lighting so no shadow edge gets picked up as
  part of the tool outline.
- Include a calibration reference (ruler, checkerboard, or known-size object)
  in frame for ToolTrace's corner-calibration step.

### 2. Create one ToolTrace design per photo

- ToolTrace's upload does not accept iPhone HEIC photos ("Failed to convert
  HEIC file") — convert to JPEG first.
- Upload the photo, run corner calibration against the reference object so
  ToolTrace knows real-world scale.
- **Mode: Fast vs. Detail** — set this before adding any tool; it cannot be
  changed on a tool after it's added (changing it loses the tool and it must
  be re-added).
  - **Detail mode** segments by apparent contiguous color/material region.
    On a multi-material tool (e.g., matte handle + shiny metal shaft) this
    fragments the tool into multiple disconnected pieces instead of one
    outline.
  - **Fast mode** grabs the whole tool silhouette in a single click. Less
    precise on fine contour detail, but doesn't fragment multi-material
    tools. **Use Fast mode for tools with a handle + metal shaft
    (T-handles, screwdrivers, etc.).**
- Click each tool to trace it, name it, and — critically — **click OK to
  confirm the trace**. A trace that is never confirmed with OK does not
  persist: reopening the design will show the bare photo with no
  AI-selected tool, and the tool will not appear in "Import Traces" from
  other designs. (This bit us on the 8 mm tool — it looked done in the
  session but had never been confirmed, so the design came back empty.)

### 3. Fix any bad traces with Fine Tune

- If an exported STEP/STL later comes out looking inverted or corrupted
  (see the "singularity" issue below), go back to the Layout step's **Fine
  Tune** tool and manually smooth the offending outline. A hand-traced
  curve can contain a "sketch singularity" — a self-intersecting loop or an
  acute/degenerate point — that blows up the boolean subtraction used to
  generate the pocket, producing a solid tool-shaped plug instead of a
  recessed pocket. Fine Tune lets you clean up the outline without
  re-tracing from scratch.

### 4. Combine tools from multiple designs with Import Traces

- If your tools are spread across several photos/designs (because some
  tools share a photo and some don't), open the design you want to build
  the final tray in and use **Import Traces** (button labeled "Import
  Tools") to pull in already-traced, OK-confirmed tools from your other
  ToolTrace designs.
- Imported tools show `Source: Imported` in their tool popup. Their
  Mode/Enforce Symmetry/Angle fields aren't shown (those only apply at
  trace time), but Pocket Depth remains editable per tool.
- An imported tool may show a generic "Imported" placeholder instead of a
  live thumbnail in the tool list — this appears to be cosmetic, not a sign
  the import failed.
- Rename each per-photo session immediately after tracing (ToolTrace's
  auto-generated names are generic and easy to confuse later). Stray or
  leftover sessions from earlier attempts can linger in the Import Traces
  picker under similarly generic names.
- Clicking a tool's delete "×" in the Tools panel removes it immediately
  with no confirmation dialog. If this happens by accident, re-import the
  tool via Import Traces from its original session rather than re-tracing.

### 5. Lay out the tools

- In the Layout step, arrange all tools in the workspace with no overlap.
  Freshly imported/added tools may all appear superimposed at first — drag
  them apart manually.
- Use **Add Simple Shapes → Finger Notch** to add a finger-access scallop to
  any pocket you'll need to pinch a tool out of: it's a circle with a live,
  draggable diameter. Position it straddling the edge of the pocket. Set its
  depth **deeper than the pocket it's attached to** (retrieval is handled by
  the notch reaching below the tool, not by the pocket itself), and deeper
  than every pocket in the layout if it's a shared/central notch.
- Other shapes available here (Circle, Square, Rectangle, Rounded Rect,
  Text) are for labels or general cutouts, not tool-specific.

### 6. Size and export in the Design step

Useful controls in the Design/SIZE/GRIDFINITY panels:

- **Pocket Depth** (per tool, via each tool's popup) — set individually for
  each tool; see the job-specific pocket-depth table below for the rule of
  thumb used.
- **Customize Overall Size → Grid Length / Grid Width** — sets the tray's
  footprint in Gridfinity grid units (1 unit = 42 mm standard pitch). Pick
  even numbers so a grid cell isn't split across a design boundary — though
  in theory a split cell would still print fine with additive manufacturing.
- **Custom Grid Size** — set to **42 mm** for standard Gridfinity pitch.
- **Split for Multiple Prints** — subdivides a layout larger than your
  printer's bed into multiple plates, each no larger than a size you
  specify (e.g. 252×252 mm = a 6×6 unit plate). If a single tool's pocket
  is bigger than one plate, ToolTrace deliberately splits that pocket
  across the shared edge of two adjacent plates — this is intentional, not
  a bug: the pocket halves align once the printed plates are placed next
  to each other.
- **Puzzle Piece Mode** (GRIDFINITY panel) — trims away empty grid cells so
  the printed outline hugs the tool shapes instead of staying a full
  rectangle. This is a separate feature from Split for Multiple Prints and
  can be combined with it.
- **Lip Design** (Default/None) and **Base magnets** (None/Corner/Full) —
  standard Gridfinity bin-bottom options.
- **Type: must stay "Gridfinity"**, not "Foam." Foam mode is believed to
  export a solid cutter/tool-shaped body rather than a tray with a
  recessed pocket — if an export ever looks inverted, check this first.
- Export **STEP and/or STL** directly from this step. For a "Split for
  Multiple Prints" layout, ToolTrace's STL export is a ZIP containing one
  **tray** STL + one **inserts** STL per piece, plus a `manifest.json`
  describing each piece's plate position/size. **Only the tray file is
  printed** — in Bambu Studio, load and print one tray STL per plate, one
  print job at a time; the inserts file is not sent to the printer.

### 7. Verify before printing

ToolTrace's own in-browser 3D preview can be unreliable to read — it has
been observed rendering one view for a few seconds and then switching to a
different view, and pocket depths can look visually deceptive (a very deep
value on one tool makes every other tool look shallow by comparison). For a
trustworthy check, load the exported STEP/STL into Bambu Studio (or
Onshape) and inspect it there directly.

### 8. Slice and print

Slice the tray STL in Bambu Studio, save as `.3mf` into
`gridfinity/3mf/<tool-name>/` per repo convention, and print.

### Why not the Onshape DXF/STEP route

Earlier trays in this repo used ToolTrace → DXF export → Onshape import →
manual boolean-subtract of the tool outline from a Gridfinity tray body.
For this job, DXF import into Onshape repeatedly dropped or corrupted tool
geometry — DXF analysis (via Python `ezdxf`) confirmed that a tool trace
touching the edge of the source photo/paper gets fused with the page
boundary into a single degenerate closed loop, which isn't cleanly
separable back into a usable tool outline. ToolTrace's native Gridfinity
export mode does the trace-to-pocket boolean work internally and skips the
DXF/Onshape round trip entirely, so this job was rebuilt on that path.

---

## Job-Specific: Wera 454/7 HF Set 1

### Tool set

7-piece T-handle Hex-Plus hex driver set. All per-tool data points in one
place:

| Hex size | Shaft length (catalog spec) | Total length (shaft + handle) | Handle block length | Shaft dia. (≈hex×1.2) | T-handle crossbar length | Crossbar thickness (used for pocket calc) | Pocket depth used | Finger notch depth |
|---|---|---|---|---|---|---|---|---|
| 2.5 mm | 100 mm | 132.0 mm | 32.0 mm | 3.0 mm  | 77.0 mm  | 15 mm | 10.5 mm | TBD¹ |
| 3 mm   | 100 mm | 133.1 mm | 33.1 mm | 3.6 mm  | 79.9 mm  | 19 mm | 13.5 mm | TBD¹ |
| 4 mm   | 100 mm | 135.2 mm | 35.2 mm | 4.8 mm  | 85.6 mm  | 19 mm | 13.5 mm | TBD¹ |
| 5 mm   | 150 mm | 187.3 mm | 37.3 mm | 6.0 mm  | 91.3 mm  | 22 mm | 15.5 mm | TBD¹ |
| 6 mm   | 150 mm | 189.5 mm | 39.5 mm | 7.2 mm  | 97.1 mm  | 22 mm | 15.5 mm | TBD¹ |
| 8 mm   | 200 mm | 243.7 mm | 43.7 mm | 9.6 mm  | 108.5 mm | 22 mm | 15.5 mm | TBD¹ |
| 10 mm  | 200 mm | 248.0 mm | 48.0 mm | 12.0 mm | 120.0 mm | 23 mm | 16.0 mm | TBD¹ |

Column notes:
- **Shaft length / total length / handle block length / shaft dia. / T-handle
  crossbar length** — from Wera's official datasheet, captured earlier in
  this project as a cross-check against the traced/photographed geometry.
  The shaft-length spec (e.g. "10.0×200") is the shaft only — total length
  ≈ shaft + handle, not the shaft-length spec alone.
- **Crossbar thickness** — Craig's own measurement of the T-handle
  crossbar's thickness/diameter (not its length — that's the separate
  "T-handle crossbar length" column above, and the two shouldn't be
  confused). This is the dimension the pocket depth is calculated from.
- **Pocket depth used** — the value actually set in ToolTrace, per tool:
  crossbar thickness × 70%, leaving at least 2–3 mm of base material below
  the pocket floor.
- **Finger notch depth** — ¹TBD: one finger notch was added per tool
  pocket in the Layout step, and each notch's depth must exceed the pocket
  it serves; the deepest pocket in the layout is 16.0 mm (10 mm tool), so
  every notch depth used was at least that. The exact per-tool values
  Craig set in ToolTrace were not recorded in this session — fill in once
  known, along with total print height and base thickness (see Status).

Wera catalog shaft lengths (used as ground truth over photo-based
measurement) match the table above.

### Source photos → ToolTrace designs

| Photo | Tools traced |
|-------|-------------|
| `10mm.jpeg` | 10 mm |
| `8mm.jpeg` | 8 mm |
| `6mm.jpeg` | 6 mm |
| `5mm.jpeg` | 5 mm |
| `small.jpeg` | 4 mm, 3 mm, 2.5 mm (all three, traced together in Fast mode) |

All 7 tools were traced in **Fast mode** — Detail mode fragmented these
tools into disconnected pieces (matte handle vs. shiny metal shaft) and was
abandoned early on. The 10 mm, 6 mm, and 5 mm designs held their tools
directly; the 8 mm, 4 mm, 3 mm, and 2.5 mm tools were imported into the
combined layout via **Import Traces** from their respective designs.

### Layout

All 7 tools arranged by hand on a **9u × 11u** grid (42 mm pitch). Split
for Multiple Prints enabled at a **252 × 252 mm** (6×6 unit) max plate size
— the limit of the target printer's bed — producing **4 plates**. Where a
tool's pocket exceeded one plate, ToolTrace split it across the shared edge
of two adjacent plates by design (pocket halves align once the plates sit
next to each other).

### Finger notches

One finger notch per tool pocket, added in the Layout step as described
above (see the consolidated table under "Tool set" for per-tool depth
status). Other than depth, notches were sized and positioned by hand
(drag-resize in Layout) rather than to a fixed rule.

### The singularity issue

Initial STEP/STL exports came out inverted — solid tool-shaped plugs
instead of a tray with recessed pockets — in both ToolTrace's own preview
and in Bambu Studio. `Type` was confirmed still set to `Gridfinity` (ruling
out a Foam-mode mixup). Root cause: a "sketch singularity" (a
self-intersecting loop) in one hand-traced tool outline. Fixed using the
Layout step's **Fine Tune** tool to clean up the offending trace, after
which the export was correct.

### Exports

Final combined 7-tool layout, split into 4 plates, exported as STL (tray +
insert body per plate) plus a `manifest.json`:

- `gridfinity/source/tooltrace/wera-454-7-hf-set-1/split-stl/` — the 4
  plates × {tray, inserts} STL pairs, and `manifest.json` (ToolTrace's own
  piece-position/size metadata). Only the 4 `*-tray.stl` files are actually
  printed (one per plate, one print job at a time in Bambu Studio); the
  `*-inserts.stl` files are not sent to the printer. ToolTrace named this
  export collection `wera-454-hf-6.0x150` internally — that's just the name of one tool in
  the set (it names the collection after a tool, not the whole design) and
  is **not** a dimension of the tray; don't read it as such.
- `gridfinity/source/tooltrace/wera-454-7-hf-set-1/photos/` — the 5 source
  photos (`10mm.jpeg`, `8mm.jpeg`, `6mm.jpeg`, `5mm.jpeg`, `small.jpeg`).
- `gridfinity/source/step/wera-454-7-hf-set-1/wera-454-7-hf-set-1-tray_v1.step`
  — the STEP export of the current, correct combined 7-tool design (whole
  assembly, not split per plate — the plate split only applies to the STL
  print files). This is a parametric/CAD file, unlike the STL meshes above;
  it's the one to reopen in Onshape/FreeCAD if the tray geometry itself
  ever needs editing, rather than just re-slicing.

Stale/superseded artifacts still present from the abandoned DXF/Onshape
route (kept for now, not deleted):

- `gridfinity/source/step/wera-454-7-hf-set-1/wera-454-7-tooltrace-combined_v1.step`
- `gridfinity/source/step/wera-454-7-hf-set-1/wera-454-7-tooltrace-combined_v2-separated.step`

These predate the switch to ToolTrace's native Gridfinity export (and the
singularity fix) and are no longer part of the active workflow. Safe to
remove in a future cleanup pass — don't confuse them with the current
`wera-454-7-hf-set-1-tray_v1.step` above, which is unrelated despite the
similar filenames.

(The stray retrace DXF that was also sitting in
`gridfinity/source/tooltrace/wera-454-7-hf-set-1/` from this same abandoned
route was removed before it was ever committed — not needed.)

---

## Status

- [x] All 7 tools photographed (colored background, distance + zoom,
      shadow-free)
- [x] All 7 tools traced in ToolTrace (Fast mode)
- [x] Combined into one workspace via Import Traces
- [x] Laid out on a 9u × 11u grid, no overlap
- [x] Pocket depths set per tool (70%-of-width rule)
- [x] Finger notches added per tool
- [x] Sketch singularity found and fixed via Fine Tune
- [x] Split for Multiple Prints configured (252×252 mm, 4 plates)
- [x] STEP/STL exported and verified in Bambu Studio
- [x] Source photos and split-STL exports copied into repo
- [x] STEP export of the current design copied into repo
- [ ] Finger notch depth / total print height / base thickness recorded
      (TBD above)
- [ ] Printing in progress (per Craig, as of 2026-09-07)
- [ ] Sliced `.3mf` saved to `gridfinity/3mf/wera-454-7-hf-set-1/`
- [ ] Stale STEP artifacts from the abandoned Onshape route removed
      (`wera-454-7-tooltrace-combined_v1.step`, `_v2-separated.step`)
- [ ] STL archived to `gridfinity/stl/inserts/wera-454-7-hf-set-1/`
