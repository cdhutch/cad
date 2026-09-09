# Wera 367/6 TORX Screwdriver Tray — Design Notes

Gridfinity tray for the Wera 367/6 TORX Kraftform Plus set (6 T-handle-less
straight Torx screwdrivers). Built with ToolTrace.ai's native "Gridfinity"
export mode — see `docs/tooltrace-to-gridfinity-workflow.md` (Part 1) for
the general, reusable procedure this project follows.

---

## Tool set

Per Wera's catalog (part 05028062001, plain 367/6 — **not** the HF
"holding function" variant, 05028059001, which has a 7th TX8×60mm tool and
different sizing on a couple of the others). Confirm against your physical
set before relying on this table:

| Tool | Tip size | Shaft length |
|------|----------|--------------|
| Wera 367 | TX 10 | 80 mm |
| Wera 367 | TX 15 | 80 mm |
| Wera 367 | TX 20 | 100 mm |
| Wera 367 | TX 25 | 100 mm |
| Wera 367 | TX 30 | 115 mm |
| Wera 367 | TX 40 | 140 mm |

Handle diameter (for the pocket-depth calculation) and finger-notch depth
are TBD — fill in per `docs/tooltrace-to-gridfinity-workflow.md` Part 1,
steps 1–2 and 7, once tracing and measurement are done.

### Source photos → ToolTrace design

TBD — fill in once tools are photographed and traced.

### Layout

TBD.

### Exports

TBD — will land in `gridfinity/source/tooltrace/wera-367-6-torx/`
(photos/, split-stl/) and `gridfinity/source/step/wera-367-6-torx/`.

---

## Status

- [ ] Tool set confirmed against physical set (plain 367/6 vs. HF variant)
- [ ] Tools photographed (colored background, distance + zoom, shadow-free)
- [ ] Tools traced in ToolTrace (Fast mode)
- [ ] Laid out, no overlap
- [ ] Pocket depths set per tool
- [ ] Finger notches added per tool
- [ ] STEP/STL exported and verified in Bambu Studio
- [ ] Source photos and exports copied into repo
- [ ] Sliced `.3mf` saved to `gridfinity/3mf/wera-367-6-torx/`
- [ ] Printed
- [ ] STL archived to `gridfinity/stl/inserts/wera-367-6-torx/`
