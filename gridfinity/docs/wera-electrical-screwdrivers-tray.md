# Wera Kraftform Plus 160i/6 Screwdriver Tray — Design Notes

Gridfinity tray for the Wera Kraftform Plus 160i/6 insulated electrical
screwdriver set, driven by tooltrace.ai STEP profiles imported into Onshape.
Mirrors the workflow in `allen-wrench-tray.md`.

---

## Source Files

`source/step/wera-electrical-screwdrivers/shadowbow.step` is the combined
tooltrace STEP export. Matching STL + DXF reference copies (7 bodies) are in
`source/tooltrace/wera-electrical-screwdrivers/`:

| File | Notes |
|------|-------|
| `body_1.stl` – `body_6.stl` | One per screwdriver in the 6-piece set |
| `body_7.stl` | Likely the rack/holder body — confirm |

`wera-electrical-screwdrivers-mm.dxf` is the combined trace.

---

## Onshape Workflow

Same pattern as `allen-wrench-tray.md`:

1. Import STEP, orient flat on the Top Plane.
2. Trace/offset the pocket per screwdriver (start at 0.3 mm clearance).
3. Extrude the Gridfinity tray body and subtract the pockets.
4. Apply the standard Gridfinity bin-bottom interface.
5. Export STL → `gridfinity/stl/inserts/wera-electrical-screwdrivers/` (not yet done).
6. Slice in Bambu Studio → `.3mf` → `gridfinity/3mf/wera-electrical-screwdrivers/`.
7. Add the Onshape link to `gridfinity/source/onshape/links.md`.

---

## Status

- [x] STEP/tooltrace source files added
- [x] Onshape Part Studio created (tray body + pockets)
- [x] Test pocket fit verified
- [x] 3MF sliced and saved → `3mf/wera-electrical-screwdrivers/wera-kraftform-160i-tray_4x6x3.9u_v1.3mf`
- [x] **Printed and installed (2026-09-06)**
- [ ] STL archived to `stl/inserts/wera-electrical-screwdrivers/` — still empty; the tray was
      exported to slice it, so grab that `.stl` from Onshape and drop it in here to keep the
      repo as the source of record
- [ ] Onshape link added to `links.md`
