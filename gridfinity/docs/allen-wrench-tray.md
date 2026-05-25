# Allen Wrench Tray — Design Notes

Gridfinity tray holders for Allen (hex) wrench sets, driven by
tooltrace.ai STEP profiles imported into Onshape.

---

## Source Files

Three STEP files exported from tooltrace.ai are in:

    gridfinity/source/step/allen-wrenches/

Each file represents the traced profile of one wrench (or one wrench set
size). Add them there and update this table:

| File | Wrench size | Notes |
|------|-------------|-------|
| _(add filename)_ | | |
| _(add filename)_ | | |
| _(add filename)_ | | |

---

## Onshape Workflow

1. **Import STEP** into Onshape as a new Part Studio or use Insert → Other documents.
2. **Orient** the wrench profile flat on the Top Plane.
3. **Trace the pocket**: create a sketch on the Top Plane, project or manually trace the
   profile outline with an offset (start with 0.3 mm clearance; adjust after test print).
4. **Tray body**: extrude a Gridfinity-sized rectangular block to the target height.
5. **Subtract the pocket**: extrude-remove the traced profile to the required depth.
6. **Gridfinity interface**: apply the standard bin bottom geometry
   (stacking lip, 42 mm grid alignment, optional magnet pockets).
7. **Export STL** → `gridfinity/stl/inserts/allen-wrenches/`
8. **Slice in Bambu Studio** → save `.3mf` → `gridfinity/3mf/allen-wrenches/`
9. **Add Onshape link** to `gridfinity/source/onshape/links.md`

---

## Sizing Notes

Allen wrenches taper significantly along their length. Decide early:

- **Short-arm pocket**: pocket depth matches the short arm; wrench drops straight in.
- **Long-arm pocket**: pocket runs the full long arm; wrench lays flat.
- **Angled slot**: wrench sits at ~15° so the ball-end (if present) clears the rim.

Recommended starting tray size: **2×1** grid units (84 × 42 mm) for a single-row set;
**3×2** for a complete SAE or metric set.

---

## Clearance and Fit

| Fit type | Offset from tooltrace profile |
|----------|-------------------------------|
| Loose (drop in) | +0.4 mm |
| Snug (press) | +0.2 mm |
| Reference only | 0 mm |

Test print a single pocket before committing to a full tray.

---

## Naming Convention

Follow `gridfinity/docs/naming.md`:

    allen-wrench-holder_<WxD>x<H>u_<variant>_v<N>.stl

Examples:
- `allen-wrench-holder_2x1x4u_metric_v1.stl`
- `allen-wrench-holder_3x2x4u_sae_v1.stl`

---

## Status

- [ ] STEP files added to `source/step/allen-wrenches/`
- [ ] Onshape Part Studio created
- [ ] First test pocket printed and fit verified
- [ ] Full tray exported and sliced
- [ ] Onshape link added to `links.md`
