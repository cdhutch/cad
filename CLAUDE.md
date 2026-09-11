# CLAUDE.md — CAD Repository Context

This file gives Claude context about the structure, conventions, and current state of this repository so each session can start with full situational awareness.

---

## What This Repo Is

A personal CAD library for 3D-printed shop organization, focused primarily on **Gridfinity**-compatible storage and tool holders. The primary design workflow is:

1. **tooltrace.ai** — photograph a tool to extract its 2D profile
2. **Gridfinity export** — ToolTrace's own native "Gridfinity" mode lays out
   traced tools and exports a finished tray (STEP/STL) directly, with no CAD
   step in between. This is the default path. Onshape is only used as a
   fallback for layouts that need a tight interlocking nest beyond simple
   grid placement, or to hand-repair bad export geometry — see
   `docs/tooltrace-to-gridfinity-workflow.md`.
3. **Export** — STL for remixing, 3MF slicer projects (Bambu Studio) for printing

Designs are parametric where possible. The repo is **project-first**: each major CAD project gets its own top-level folder alongside `gridfinity/`.

---

## Active Branch

`tooltrace-misc-handtools` — branched from `main` after the Wera 367/6 TORX tray (built on the now-retired `tooltrace-wera-367-6-torx` branch) was merged. Holds a lighter-weight, ongoing project for miscellaneous hand tools (not single-brand sets like the prior Wera trays).

---

## Git Workflow Constraint

**Always provide git commands for the user to run; never execute them directly in the shell.** Running git in the sandbox causes stale lock files (`.git/index.lock`, `.git/HEAD.lock`) that block the user's terminal. This also applies to push/pull — Claude never pushes to or pulls from GitHub; the user runs every git command themselves.

---

## Repo Structure

```
cad/
├── CLAUDE.md                        ← this file
├── README.md                        ← human-facing overview
├── .gitattributes                   ← Git LFS tracking (*.stl, *.3mf, *.step, *.stp, *.dxf)
├── docs/
│   ├── repo-conventions.md          ← naming rules and folder conventions
│   └── tooltrace-to-gridfinity-workflow.md  ← reproducible ToolTrace → Gridfinity export → Bambu Studio pipeline (Onshape as fallback)
└── gridfinity/                      ← only project currently
    ├── README.md
    ├── docs/
    │   ├── naming.md                       ← filename convention spec
    │   ├── notes.md                        ← design notes + per-tray status tables
    │   ├── allen-wrench-tray.md            ← design notes for Allen wrench tray project
    │   ├── wera-electrical-screwdrivers-tray.md  ← design notes for Wera screwdriver tray
    │   ├── wera-454-7-hf-set-1-tray.md     ← design notes for Wera 454/7 HF Set 1 T-handle tray
    │   ├── wera-phillips-flathead-screwdrivers-tray.md  ← design notes for combined Wera flathead+Phillips tray (printed)
    │   ├── wera-367-6-torx-tray.md         ← design notes for Wera 367/6 TORX tray (printed)
    │   ├── misc-handtools-tray.md          ← running doc for miscellaneous hand tool trays (lighter-weight, no per-item doc)
    │   ├── drill_tray_generator.md         ← step-by-step Onshape guide for parametric drill trays
    │   ├── bambu-tool-tray-profile.md      ← Bambu Studio print-profile writeup for low-strength/fast/low-filament trays
    │   └── gridfinity-tray-light.json      ← the corresponding Bambu Studio process preset (verified 2026-09-06)
    ├── source/
    │   ├── onshape/
    │   │   └── links.md             ← Onshape document URLs (stub — add links as docs are created)
    │   ├── step/                    ← STEP files for Onshape import, organised by tool
    │   │   ├── allen-wrenches/      ← body_1.step, body_2.step, body_3.step
    │   │   ├── wera-electrical-screwdrivers/  ← shadowbow.step
    │   │   ├── wera-454-7-hf-set-1/ ← current STEP export (wera-454-7-hf-set-1-tray_v1.step) plus 2 stale Onshape-era files
    │   │   ├── wera-phillips-flathead-screwdrivers/  ← wera-phillips-flathead-screwdrivers-tray_v1.step
    │   │   ├── wera-367-6-torx/            ← wera-367-6-torx-tray_v1.step
    │   │   └── misc-handtools/             ← 6 item subfolders (red-milwaukee-box, stud-finder, kobalt-25ft-tape-measure, klein-ncvt1p-voltage-tester, hypertough-77pc-electronics-kit, dewalt-drill-bit-sets), one -tray_v1.step each
    │   └── tooltrace/               ← raw tooltrace.ai exports (photos + STL/DXF), organised by tool
    │       ├── allen-wrenches/      ← body_1.stl, body_2.stl, colorful-wiha-hex-keys-mm.dxf
    │       ├── wera-electrical-screwdrivers/  ← body_1–7.stl, wera-electrical-screwdrivers-mm.dxf
    │       ├── wera-454-7-hf-set-1/ ← photos/, split-stl/ (4-plate tray+inserts STL export)
    │       ├── wera-phillips-flathead-screwdrivers/  ← photos/ (flathead.jpeg, phillips.jpeg), split-stl/ (3-plate tray+inserts STL export)
    │       ├── wera-367-6-torx/            ← photos/ (torx.jpeg), split-stl/ (4-plate tray+inserts STL export)
    │       └── misc-handtools/             ← 6 item subfolders, each with photos/ + one renamed tray STL (stamp STLs discarded)
    ├── stl/
    │   ├── baseplates/
    │   │   └── magnet/              ← STL baseplate exports (currently empty)
    │   └── inserts/                 ← finished tray STLs
    │       ├── allen-wrenches/      ← wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl
    │       ├── wera-electrical-screwdrivers/  ← (empty — STL not yet exported)
    │       ├── wera-phillips-flathead-screwdrivers/  ← 3 piece tray STLs
    │       ├── wera-367-6-torx/            ← 4 piece tray STLs
    │       ├── red-milwaukee-box/          ← red-milwaukee-box-tray_6x3x3u_v1.stl
    │       ├── stud-finder/                ← stud-finder-tray_5x3x3u_v1.stl
    │       ├── kobalt-25ft-tape-measure/   ← kobalt-25ft-tape-measure-tray_3x3x3u_v1.stl
    │       ├── klein-ncvt1p-voltage-tester/ ← klein-ncvt1p-voltage-tester-tray_4x1x3u_v1.stl
    │       ├── hypertough-77pc-electronics-kit/ ← hypertough-77pc-electronics-kit-tray_4x6x3u_v1.stl
    │       └── dewalt-drill-bit-sets/      ← dewalt-drill-bit-sets-tray_4x6x3u_v1.stl
    └── 3mf/
        ├── baseplates/
        │   └── magnet/              ← 2 baseplate slicer builds (see below)
        ├── grids/                   ← layout grids (currently empty)
        ├── wera-electrical-screwdrivers/  ← wera-kraftform-160i-tray_4x6x3.9u_v1.3mf
        ├── nystrom_performance/     ← 10 tool tray builds for Nystrom Performance cabinet
        ├── wera-phillips-flathead-screwdrivers/  ← 3-plate sliced project
        ├── wera-367-6-torx/            ← 4-plate sliced project
        ├── red-milwaukee-box/          ← red-milwaukee-box-tray_6x3x3u_v1.3mf
        ├── stud-finder/                ← stud-finder-tray_5x3x3u_v1.3mf
        ├── kobalt-25ft-tape-measure/   ← kobalt-25ft-tape-measure-tray_3x3x3u_v1.3mf
        ├── klein-ncvt1p-voltage-tester/ ← klein-ncvt1p-voltage-tester-tray_4x1x3u_v1.3mf
        ├── hypertough-77pc-electronics-kit/ ← hypertough-77pc-electronics-kit-tray_4x6x3u_v1.3mf
        └── dewalt-drill-bit-sets/      ← dewalt-drill-bit-sets-tray_4x6x3u_v1.3mf
```

> Note: `stl/` and `3mf/` deliberately use the same top-level split
> (`baseplates/`, `grids/`, then per-tool folders for `inserts/`-style trays)
> rather than each inventing its own layout — keep new folders consistent
> with that pattern. `gridfinity/3mf/allen-wrenches/` already exists (reserved
> via `.gitkeep`) even though no 3MF has been built yet — that's this repo's
> existing convention for stub folders, and it's a good one; keep using
> `.gitkeep` to reserve a destination folder ahead of the file landing in it.

---

## Current Design Inventory

### Baseplates (`gridfinity/3mf/baseplates/magnet/`)

| File | Description |
|------|-------------|
| `base_frame_mag_frame_6x6_v1.3mf` | 6×6 magnet baseplate build |
| `base_frame_mag_frame_1x6_upper-drawer-x-expansion_v2_gcode.3mf` | 1×6 expansion baseplate for upper drawer (includes gcode); v2 with +10mm X offset to fit non-square drawer |

### Nystrom Performance Trays (`gridfinity/3mf/nystrom_performance/`)

Slicer builds for tool organization trays fitting a Nystrom Performance tool cabinet. Trays are numbered sequentially; the left-hand drill tray is explicitly named.

| File | Notes |
|------|-------|
| `tray-1_v1.3mf` through `tray-9_v1.3mf` | 9 tool trays, ~136–503 KB each |
| `left-hand-drill-tray_v1.3mf` | Left-hand drill bit tray |

> **TODO:** Document what each numbered tray holds — table stubbed out in `gridfinity/docs/notes.md`.

### tooltrace.ai Tray Projects (`tooltrace-tools` branch)

#### Colorful Wiha Hex Key Sets — SAE + Metric (`gridfinity/stl/inserts/allen-wrenches/`) — ✅ printed & installed 2026-09-06

| File | Description |
|------|-------------|
| `wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl` | STL exported from Onshape; 4×6 grid, 2.1u height |

- Printed and installed. Repo gap: the `.3mf` used to slice it was never archived to
  `3mf/allen-wrenches/` (still just `.gitkeep`) — see `gridfinity/docs/allen-wrench-tray.md`
- tooltrace source: `source/tooltrace/allen-wrenches/` (body_1.stl, body_2.stl, colorful-wiha-hex-keys-mm.dxf) and `source/step/allen-wrenches/` (body_1–3.step)

#### Wera Kraftform Plus 160i/6 Insulated Screwdriver Set (`gridfinity/3mf/wera-electrical-screwdrivers/`) — ✅ printed & installed 2026-09-06

| File | Description |
|------|-------------|
| `wera-kraftform-160i-tray_4x6x3.9u_v1.3mf` | Bambu Studio project; 4×6 grid, 3.9u height |

- Printed and installed. Repo gap: the `.stl` exported from Onshape to slice it was never
  archived to `stl/inserts/wera-electrical-screwdrivers/` (still empty) — see
  `gridfinity/docs/wera-electrical-screwdrivers-tray.md`
- tooltrace source: `source/tooltrace/wera-electrical-screwdrivers/` (body_1–7.stl, dxf) and `source/step/wera-electrical-screwdrivers/` (shadowbow.step)
- 6-piece set; 7 tooltrace bodies (body_7 is likely the rack/holder)

#### Wera 454/7 HF Set 1 T-Handle Hex-Plus Screwdrivers (`gridfinity/docs/wera-454-7-hf-set-1-tray.md`) — 🚧 printing in progress

7-piece set (2.5/3/4/5/6/8/10mm). Built via ToolTrace's native Gridfinity
export (not Onshape — the DXF/Onshape route was abandoned after repeated
import failures; see the project doc). All 7 tools traced, combined, laid
out on a 9u×11u grid, and split into 4 plates (252×252mm max) with per-tool
pocket depths and finger notches. STEP/STL exported and verified; printing
as of 2026-09-07. See the project doc for full status and the general
`docs/tooltrace-to-gridfinity-workflow.md` for the reusable procedure.

- tooltrace source: `source/tooltrace/wera-454-7-hf-set-1/` (photos/,
  split-stl/) and `source/step/wera-454-7-hf-set-1/`
  (`wera-454-7-hf-set-1-tray_v1.step` — current; the `tooltrace-combined_v1`
  / `_v2-separated` STEP files there are stale, from the abandoned Onshape
  route)

#### Wera Flathead + Phillips Screwdrivers (`gridfinity/docs/wera-phillips-flathead-screwdrivers-tray.md`) — ✅ printed 2026-09-09

7-tool combined ToolTrace design (3 slotted: Wera 335 0.5×3.0, Wera 334
0.8×5.0×100, Wera 334 1.2×6.5×150; 4 Phillips: Wera 350 PH0×60/PH1×80/
PH2×100/PH3×150), laid out on a 13u×3u grid and split into 3 print plates.
Flathead/Phillips are interleaved across the plates (not grouped). A
planned color-coded insert scheme (printing each plate's insert sheet
twice, once per color, hand-sorted by tool-head shape) was dropped — the
exported insert STLs bundle each plug at its real pocket depth rather
than flat on a bed, and the trays are usable without them. Printed as 3
single-color tray plates. Follows the ToolTrace-native workflow
(`docs/tooltrace-to-gridfinity-workflow.md`, Part 1).

- tooltrace source: `source/tooltrace/wera-phillips-flathead-screwdrivers/`
  (photos/, split-stl/) and `source/step/wera-phillips-flathead-screwdrivers/`
  (`wera-phillips-flathead-screwdrivers-tray_v1.step`)
- archived: `stl/inserts/wera-phillips-flathead-screwdrivers/` (3 tray STLs)
  and `3mf/wera-phillips-flathead-screwdrivers/` (sliced project, 3 plates)

#### Wera 367/6 TORX Screwdrivers (`gridfinity/docs/wera-367-6-torx-tray.md`) — ✅ printed 2026-09-10

6-piece Torx set (Wera 367/6, part 05028062001 — TX10×80, TX15×80,
TX20×100, TX25×100, TX30×115, TX40×140mm; confirmed as the plain 367/6 set
via Craig's handle measurements, not the 7-piece HF variant). 7u×9u grid,
split into 4 plates. Follows the ToolTrace-native workflow
(`docs/tooltrace-to-gridfinity-workflow.md`, Part 1).

- tooltrace source: `source/tooltrace/wera-367-6-torx/` (photos/,
  split-stl/) and `source/step/wera-367-6-torx/`
  (`wera-367-6-torx-tray_v1.step`)
- archived: `stl/inserts/wera-367-6-torx/` (4 tray STLs) and
  `3mf/wera-367-6-torx/` (sliced project)

#### Misc Hand Tools (`gridfinity/docs/misc-handtools-tray.md`) — ✅ printed 2026-09-11

Lighter-weight, ongoing project for odds-and-ends hand tools that don't
belong to a single branded set — no per-item doc, just one running doc,
with each item (or combined group) getting its own tray/print rather than
one shared design. All six queued items are done: Milwaukee driver bit
set and wall stud finder (each own tray, redone as separate single-item
prints after a 6u×6u combined tray failed to print); both DeWalt drill
bit boxes (combined into one tray); Klein Tools NCVT-1P voltage detector;
Hyper Tough 77-piece electronics repair kit; Kobalt 25' tape measure.
10mm pockets throughout, no finger notches needed. See the project doc
for the print-failure lesson (narrowed to 6u×6u specifically) and a note
on using ToolTrace's Trace Offset: Small for roughly-traced tools.

- tooltrace source: `source/tooltrace/misc-handtools/<item>/` and
  `source/step/misc-handtools/<item>/`, one subfolder per item/group
- archived: `stl/inserts/<item>/` and `3mf/<item>/` per item (see tree
  above for the six folder names)

---

## Empty / Stub Locations

- `gridfinity/stl/baseplates/magnet/` — STL exports of baseplates (not yet exported)
- `gridfinity/stl/inserts/wera-electrical-screwdrivers/` — STL pending Onshape export
- `gridfinity/3mf/grids/` — layout grid builds (not started)
- `gridfinity/3mf/allen-wrenches/` — 3MF pending Bambu Studio build (folder reserved via `.gitkeep`)
- `gridfinity/source/onshape/links.md` — Onshape document URLs (stub only; no docs created yet)
- `gridfinity/docs/notes.md` — has stub tables for Nystrom trays and baseplates; fill in as confirmed

---

## Naming Convention

Defined in `gridfinity/docs/naming.md`:

```
<name>_<WxD>x<height-u>u_<variant>_v<major>[.<minor>].<ext>
```

- `W` and `D` are Gridfinity grid units (1 unit = 42 mm)
- `height-u` is height in Gridfinity height units
- `variant` describes fit or subtype (e.g., `magnet`, `loose`, `tight`)
- Version suffix: `_v1`, `_v2`, or `_v1.1` for minor revisions

**Examples:**
- `baseplate_4x4x0u_magnet_v1.stl`
- `calipers-holder_2x1x6u_loose_v1.1.stl`

General rules (from `docs/repo-conventions.md`):
- Lowercase filenames
- Hyphens for multi-word descriptors
- Version suffix on every file

---

## File Types and Git LFS

All binary geometry is tracked via **Git LFS** (`.gitattributes`):

| Extension | Purpose |
|-----------|---------|
| `.3mf` | Slicer project files (Bambu Studio); include plate layout, supports, print profiles |
| `.stl` | Printable mesh exports; suitable for remixing or direct slicing |
| `.step` / `.stp` | CAD exchange geometry (Onshape exports for interoperability) |
| `.dxf` | 2D trace/sketch geometry (tooltrace exports) |

> `*.dxf` was documented here as LFS-tracked but was missing from `.gitattributes`
> until this reorganization — it's fixed now, but the two DXF files already
> committed on `tooltrace-tools` (1.7 MB and 2.8 MB) were committed as regular
> git blobs, not LFS objects. New commits of those files will now go through
> LFS; migrating the *existing* commits into LFS requires `git lfs migrate`,
> which rewrites history and would need a force-push — worth doing deliberately
> later, not as a side effect of this cleanup.

---

## Onshape Workflow

Source CAD lives in Onshape (cloud). This repo stores:
- Links to Onshape documents in `gridfinity/source/onshape/links.md`
- STEP exports in `gridfinity/source/step/` for non-Onshape use
- STL/3MF outputs from those designs

### Parametric Drill Tray Pattern

`gridfinity/docs/drill_tray_generator.md` is a complete step-by-step guide to building a **parametric drill-bit tray generator** in Onshape. Key design patterns:

- Variables at the top of the Part Studio (`#grid = 42 mm`, `#tray_width`, `#hole_depth`, etc.)
- Gridfinity sizing: `#tray_width = N * #grid`
- Tray body → pocket extrude → hole layout sketch → Hole Tool → Linear Pattern → label engrave → fillets
- **Configurations** to switch between drill sets (fractional / letter / number / metric / left-hand)
- Export each configuration as STL, then build a plate layout in Bambu Studio and save as `.3mf`

---

## Design Workflow (tooltrace.ai → Onshape → Print)

1. **tooltrace.ai**: Photograph the tool to extract its profile. Download **STEP + DXF** (skip SVG). STL is optional but also worth keeping.
   - STEP → `gridfinity/source/step/<tool>/` (used as Onshape boolean subtract body)
   - STL + DXF → `gridfinity/source/tooltrace/<tool>/` (reference; DXF can be imported as Onshape sketch)
2. **Onshape**: Import STEP as solid body. Boolean subtract (with `#clearance` offset) from tray body to create pocket. Apply Gridfinity bin geometry (lip, stacking interface, optional magnet pockets).
3. **Export STL** from Onshape → `gridfinity/stl/inserts/<tool>/<name>_<WxD>x<H>u_<variant>_v<N>.stl`
4. **Slice in Bambu Studio** → `File → Save Project` (NOT Export Plate Sliced File — that embeds gcode and produces a ~270 MB file). Save as `.3mf` to `gridfinity/3mf/<tool>/`
5. **Update `links.md`** with the Onshape document URL and version/config notes

### tooltrace.ai STEP File Characteristics

tooltrace STEP exports are **flat solid slabs** (~1.9–6 mm Z) representing the tool silhouette lying on a plane — not sketches. In Onshape, use boolean subtract rather than sketch projection. Apply a `#clearance` variable (start at 0.3 mm; see `gridfinity/docs/allen-wrench-tray.md` for clearance table).

---

## Git History Summary

The repo evolved from a standalone gridfinity repo (imported at commit `f6d3bdb`) into a general project-first CAD library. Notable commits:

- `c3eda36` — Restructure to project-first layout
- `c0b7810` — README updated for general CAD repo
- `2f13bba` — Added drill tray generator design guide

---

## Adding New Projects

When starting a new CAD project (e.g., a non-Gridfinity enclosure or jig):

1. Create a new top-level folder: `cad/<project-name>/`
2. Mirror the internal structure: `source/`, `stl/`, `3mf/`, `docs/`
3. Add a `README.md` describing the project
4. Follow naming conventions from `docs/repo-conventions.md`

---

## Reorganization Log

- **2026-09-06**: Flattened `stl/base/baseplates/magnet/` → `stl/baseplates/magnet/`
  to match `3mf/baseplates/magnet/`'s layout (was an empty, untracked folder —
  no git history affected). Added missing `*.dxf` LFS rule to `.gitattributes`.
  Synced `README.md`'s structure diagram with reality. Updated
  `allen-wrench-tray.md`'s status checklist to match files actually present,
  and added a matching `wera-electrical-screwdrivers-tray.md` doc and
  `notes.md` status tables. No git commands were run — see the session's
  git command list for what's staged for commit.
