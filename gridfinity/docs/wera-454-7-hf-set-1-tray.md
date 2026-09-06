# Wera 454/7 HF Set 1 (T-Handle Hex-Plus) Tray — Design Notes

Gridfinity tray for the Wera 05023450001 454/7 HF SET 1 screwdriver set — 7
T-handle Hex-Plus hex drivers with holding function (2.5, 3, 4, 5, 6, 8, 10mm).
Driven by tooltrace.ai STEP profiles imported into Onshape, same pattern as
`allen-wrench-tray.md` and `wera-electrical-screwdrivers-tray.md`, but this
project additionally needs a **compact/interlocking nest** (see Packing
Objective below) rather than a simple spacious layout, so it gets its own
notes doc to track that work in detail.

---

## Tool Set — Measured/Sourced Dimensions

Confirmed against the official Wera PDF datasheet (cross-checked after an
initial WebFetch of the product page garbled the size column). All values mm.

| Hex size | Shaft length (spec) | Handle block length | Shaft dia. (≈ hex×1.2) | Handle block width | Total length (shaft + handle) |
|---|---|---|---|---|---|
| 2.5 | 100 | 32.0 | 3.0  | 77.0  | 132.0 |
| 3   | 100 | 33.1 | 3.6  | 79.9  | 133.1 |
| 4   | 100 | 35.2 | 4.8  | 85.6  | 135.2 |
| 5   | 150 | 37.3 | 6.0  | 91.3  | 187.3 |
| 6   | 150 | 39.5 | 7.2  | 97.1  | 189.5 |
| 8   | 200 | 43.7 | 9.6  | 108.5 | 243.7 |
| 10  | 200 | 48.0 | 12.0 | 120.0 | 248.0 |

**Important convention note:** the shaft-length spec (e.g. "10.0×200") is the
shaft only — the handle block adds on top of it. Total tool length ≈
shaft + handle, NOT shaft length alone (confirmed by Craig's physical
measurement: 10mm tool ≈ 250mm overall vs. 200mm shaft spec).

Each tool was traced from its own sheet of paper (Letter, used as the scale
reference) per Craig's 4 photos:
- Sheet 1: 10.0×200 (1 tool)
- Sheet 2: 6.0×150 + 3.0×100 (2 tools)
- Sheet 3: 4.0×100 + 5.0×150 + 2.5×100 (3 tools)
- Sheet 4: 8.0×200 (1 tool)

---

## Printer Constraint

Bambu Lab P2S build volume is 256×256×256mm (confirmed via official spec
sheet). Practical Gridfinity cap per plate: **6×6 grid units = 252×252mm**.

## Packing Objective

Craig's explicit requirement: this is a **constrained optimization problem**,
not just "make it fit" — minimize total Gridfinity grid squares consumed
across however many plates are needed, allowing interlocking/nested placement
(tools' bounding boxes may rotate and pack tightly against each other) rather
than a simple grid-spaced layout. A finger-clearance allowance around each
handle (to pinch and lift the tool out) must be included in the packing, not
just a uniform margin — ToolTrace has a native "Finger Notch" shape for this
(see below), which is cleaner than hand-modeling extra margin.

### Preliminary packing exploration (cloud-side heuristic, superseded by ToolTrace/Onshape real geometry)

Before switching to ToolTrace's actual traced+offset geometry, a standalone
Python bottom-left-fill + partition-search heuristic (modeling each tool as a
T-shaped raster mask) found a **2-plate split at 60 total grid squares**:
- Plate A (4×6 grid): 2.5mm + 8mm tools
- Plate B (6×6 grid): 3mm + 4mm + 5mm + 6mm + 10mm tools

This was a rough heuristic on modeled (not traced) dimensions and did not yet
account for finger clearance properly — **treat as a sanity-check baseline,
not the final layout**. The real nest will be done in Onshape using
ToolTrace's actual traced/offset footprints (see below).

---

## ToolTrace Workflow — Notes From This Session

1. **HEIC not supported.** ToolTrace's server-side upload rejects iPhone HEIC
   photos ("Failed to convert HEIC file"). Convert to JPEG first.
2. **One photo = one ToolTrace session.** The upload dropzone takes a single
   photo per "New Tooltrace" project; multiple tools on one sheet auto-trace
   together fine (e.g. sheet 2's two tools, sheet 3's three tools all
   auto-selected correctly), but combining tools from *different* photos into
   one design requires a separate step (next point) — there is no
   multi-photo upload into one session.
3. **"Import Traces" combines sessions.** Each per-sheet session is traced
   individually, then a master session uses **Import Tools → Import Traces**
   to pull specific tool outlines from other sessions into one combined
   design. This is how all 7 tools ended up in one "Wera 454/7 HF Set 1 -
   Full Tray" ToolTrace design.
   - Gotcha: stray/leftover sessions from earlier work (e.g. "Black Wera
     Tool", "Black Word Hex Keys") can appear in the import picker with
     generic auto-generated names — rename each new session immediately
     after tracing to avoid importing the wrong/duplicate one.
   - Gotcha: accidentally clicking a tool's delete "×" in the Tools panel
     removes it with no confirmation; re-import via Import Traces to recover.
4. **No auto-nest / no auto-split.** The Layout step is a manual drag/rotate
   canvas — ToolTrace does not automatically pack tools or split an oversized
   layout into plate-sized chunks. It does snap to the grid and shows live
   size feedback (mm), and the canvas is ~1:1 px:mm at 100% zoom, but precise
   arrangement is manual. **Decision: do the precise nest + plate-split in
   Onshape instead**, where exact numeric placement and boolean splitting are
   available. ToolTrace's job is just clean per-tool offset outlines.
5. **Pocket Depth is a real per-tool field**, default 20.0mm, editable per
   tool (found on the tool's detail card in the Layout step).
6. **Finger Notch** is a native "Add Simple Shapes" tool in the Layout step —
   use this instead of hand-modeling extra clearance margin around handles.
7. **Puzzle Piece Mode** exists as a toggle under the Gridfinity panel —
   not yet explored; may be relevant to interlocking pockets between
   adjacent bins (unclear if it applies within a single tray design).
8. **Shadow artifacts in traced outlines.** Some traced profiles pick up the
   tool's cast shadow as part of the silhouette, especially at extended
   portions (handle tips, shaft ends). **Action item for Onshape:** clean up
   each imported profile against the true tool geometry before using it as a
   pocket cutter — trim shadow-elongated edges, smooth noisy curves.
9. **STEP export includes an auto-generated baseplate/background solid** in
   addition to the tool profiles — 8 solid bodies exported for 7 tools. The
   extra solid auto-sizes to the bounding box of the current (messy/spread)
   layout and carries Gridfinity base detail (magnet holes etc. — large
   point count). **Discard this solid in Onshape**; we'll build our own
   baseplate.
10. Tool profile solids are thin (~0.5mm Z) flat "stamp" extrusions, not
    pre-cut pockets — they're meant to be used as 2D profiles/cutters in CAD,
    re-extruded to whatever real pocket depth we choose per tool.

### Extracted real footprint sizes (from STEP, axis-aligned bounding box, current rotation — not yet de-rotated/verified against known tool identities)

| Solid # | dx (mm) | dy (mm) |
|---|---|---|
| 54    | 136.3 | 268.6 |
| 2294  | 102.7 | 143.3 |
| 4534  | 136.4 | 214.8 |
| 6944  | 106.5 | 148.7 |
| 9354  | 89.4  | 138.6 (best match: 4mm tool) |
| 11339 | 136.0 | 215.4 |
| 14259 | 131.0 | 266.6 |

Confirmed stable across two separate STEP exports (only solid positions
changed after Craig manually separated the shapes in ToolTrace's Layout
step — the sizes themselves didn't change), so these are reliable. Some
values don't cleanly match the expected L/W pairs from the measured-dimension
table above, likely because the traced profiles retain a slight rotation
from the source photo angle (not purely axis-aligned to length/width) —
**needs verification once the actual geometry is visible in Onshape**, rather
than inferred from bounding boxes alone.

### Source files

- `gridfinity/source/step/wera-454-7-hf-set-1/wera-454-7-tooltrace-combined_v1.step`
  — first combined export (7 tools, overlapping default layout positions;
  small file, ~1MB).
- `gridfinity/source/step/wera-454-7-hf-set-1/wera-454-7-tooltrace-combined_v2-separated.step`
  — second export after Craig manually spread the 7 shapes apart in
  ToolTrace's Layout canvas (large file, ~47MB — mostly from the
  auto-generated baseplate solid's magnet-hole detail once it grew to
  ~1000×1000mm bounding box; discard that solid on import).

---

## Onshape Workflow (in progress)

New document created: **"Wera 454-7 HF Set 1 Tray"**
(https://cad.onshape.com/documents/e3d2663aa007421ab93823e3/w/04d6597c6283cc488d0a575c/e/c9e9925d189f10ceaff34c0d)
— created on Craig's Free (public-data-only) Onshape subscription, so this
document is public.

Planned steps from here:
1. Import the combined STEP (v1, small file) as reference geometry.
2. Identify and discard the auto-generated baseplate solid.
3. Clean up each of the 7 tool profiles — remove shadow-elongated edges,
   verify true dimensions against the measured-dimension table above.
4. Determine final grouping/nest (informed by, but not identical to, the
   60-grid-square 2-plate heuristic above) using exact Onshape placement.
5. Extrude tray body per plate, boolean-subtract tool pockets + finger
   notches, apply standard Gridfinity bin-bottom interface.
6. Export STL per plate → `gridfinity/stl/inserts/wera-454-7-hf-set-1/`.
7. Slice in Bambu Studio using the "Gridfinity Tray - Light" profile →
   `.3mf` → `gridfinity/3mf/wera-454-7-hf-set-1/`.
8. Add the Onshape link to `gridfinity/source/onshape/links.md`.

---

## Status

- [x] Tool set dimensions confirmed (Wera datasheet + Craig's measurements)
- [x] All 7 tools photographed (4 sheets) and traced in ToolTrace
- [x] All 7 traces combined into one ToolTrace design via Import Traces
- [x] STEP exported (2 versions — see Source files above) and archived to repo
- [x] Onshape document created
- [ ] STEP imported into Onshape
- [ ] Shadow-artifact cleanup on traced profiles
- [ ] Final nest / plate-split determined
- [ ] Tray body + pockets modeled
- [ ] STL exported
- [ ] 3MF sliced
- [ ] Printed
- [ ] Onshape link added to `links.md`
