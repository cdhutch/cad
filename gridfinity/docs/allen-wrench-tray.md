# Allen Wrench Tray — Design Notes

Gridfinity tray holders for Allen (hex) wrench sets, driven by
tooltrace.ai STEP profiles imported into Onshape.

---

## Source Files

Three STEP files exported from tooltrace.ai are in `source/step/allen-wrenches/`,
with matching STL + DXF reference copies in `source/tooltrace/allen-wrenches/`:

| File | Wrench size | Notes |
|------|-------------|-------|
| `body_1.step` | _(add size)_ | |
| `body_2.step` | _(add size)_ | |
| `body_3.step` | _(add size)_ | |

`colorful-wiha-hex-keys-mm.dxf` is the combined tooltrace trace of the full set.

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

The tray actually built (`wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl`) covers both
SAE and metric in one 4×6, 2.1u-tall tray.

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

Follow `naming.md`:

    allen-wrench-holder_<WxD>x<H>u_<variant>_v<N>.stl

Examples:
- `allen-wrench-holder_2x1x4u_metric_v1.stl`
- `allen-wrench-holder_3x2x4u_sae_v1.stl`

---

## Status

- [x] STEP files added to `source/step/allen-wrenches/`
- [x] Onshape Part Studio created (tray body + pockets)
- [x] Test pocket fit verified
- [x] Full tray STL exported → `stl/inserts/allen-wrenches/wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl`
- [x] **Printed and installed (2026-09-06)**
- [ ] 3MF archived to `3mf/allen-wrenches/` — confirmed (2026-09-06, via `git log --all`)
      this file was never committed on any branch. Nothing design-wise is lost: the STL that
      was sliced (`stl/inserts/allen-wrenches/wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl`)
      is already here — re-slice it in Bambu Studio (check recent projects first if you want
      the original plate/print settings) and save the `.3mf` here.
- [ ] Onshape link added to `links.md`
