# CLAUDE.md — CAD Repository Context

This file gives Claude context about the structure, conventions, and current state of this repository so each session can start with full situational awareness.

---

## What This Repo Is

A personal CAD library for 3D-printed shop organization, focused primarily on **Gridfinity**-compatible storage and tool holders. The primary design workflow is:

1. **tooltrace.ai** — photograph a tool to extract its 2D profile
2. **Onshape** — build the holder around the profile, apply Gridfinity interface geometry
3. **Export** — STL for remixing, 3MF slicer projects (Bambu Studio) for printing

Designs are parametric where possible. The repo is **project-first**: each major CAD project gets its own top-level folder alongside `gridfinity/`.

---

## Active Branch

`tooltrace-tools` — all tooltrace.ai-driven tray work lives here. Not yet merged to main.

---

## Git Workflow Constraint

**Always provide git commands for the user to run; never execute them directly in the shell.** Running git in the sandbox causes stale lock files (`.git/index.lock`, `.git/HEAD.lock`) that block the user's terminal.

---

## Repo Structure

```
cad/
├── CLAUDE.md                        ← this file
├── README.md                        ← human-facing overview
├── .gitattributes                   ← Git LFS tracking (*.stl, *.3mf, *.step, *.stp, *.dxf)
├── docs/
│   └── repo-conventions.md          ← naming rules and folder conventions
└── gridfinity/                      ← only project currently
    ├── README.md
    ├── docs/
    │   ├── naming.md                ← filename convention spec
    │   ├── notes.md                 ← design notes (stub — populate as decisions are made)
    │   ├── allen-wrench-tray.md     ← design notes for Allen wrench tray project
    │   └── drill_tray_generator.md  ← step-by-step Onshape guide for parametric drill trays
    ├── source/
    │   ├── onshape/
    │   │   └── links.md             ← Onshape document URLs (stub — add links as docs are created)
    │   ├── step/                    ← STEP files for Onshape import, organised by tool
    │   │   ├── allen-wrenches/      ← body_1.step, body_2.step, body_3.step
    │   │   └── wera-electrical-screwdrivers/  ← STEP from tooltrace
    │   └── tooltrace/               ← raw tooltrace.ai exports (STL + DXF), organised by tool
    │       ├── allen-wrenches/      ← body_1.stl, body_2.stl, colorful-wiha-hex-keys-mm.dxf
    │       └── wera-electrical-screwdrivers/  ← body_1–7.stl, wera-electrical-screwdrivers-mm.dxf
    ├── stl/
    │   ├── base/
    │   │   └── baseplates/
    │   │       └── magnet/          ← STL baseplate exports (currently empty)
    │   └── inserts/                 ← finished tray STLs from Onshape
    │       ├── allen-wrenches/      ← wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl
    │       └── wera-electrical-screwdrivers/  ← (empty — STL not yet exported)
    └── 3mf/
        ├── baseplates/
        │   └── magnet/              ← 2 baseplate slicer builds (see below)
        ├── grids/                   ← layout grids (currently empty)
        ├── allen-wrenches/          ← (empty — 3MF not yet built)
        ├── wera-electrical-screwdrivers/  ← wera-kraftform-160i-tray_4x6x3.9u_v1.3mf
        └── nystrom_performance/     ← 10 tool tray builds for Nystrom Performance cabinet
```

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

> **TODO:** Document what each numbered tray holds in `gridfinity/docs/notes.md`.

### tooltrace.ai Tray Projects (in progress — `tooltrace-tools` branch)

#### Colorful Wiha Hex Key Sets — SAE + Metric (`gridfinity/stl/inserts/allen-wrenches/`)

| File | Description |
|------|-------------|
| `wiha-hex-key-tray_4x6x2.1u_sae-metric_v1.stl` | STL exported from tooltrace.ai; 4×6 grid, 2.1u height |

- Onshape CAD not yet started; see `gridfinity/docs/allen-wrench-tray.md` for full workflow and checklist
- 3MF slicer build not yet created
- tooltrace source: `source/tooltrace/allen-wrenches/` (body_1.stl, body_2.stl, colorful-wiha-hex-keys-mm.dxf) and `source/step/allen-wrenches/` (body_1–3.step)

#### Wera Kraftform Plus 160i/6 Insulated Screwdriver Set (`gridfinity/3mf/wera-electrical-screwdrivers/`)

| File | Description |
|------|-------------|
| `wera-kraftform-160i-tray_4x6x3.9u_v1.3mf` | Bambu Studio project; 4×6 grid, 3.9u height |

- STL not yet exported from Onshape → `stl/inserts/wera-electrical-screwdrivers/` is empty
- tooltrace source: `source/tooltrace/wera-electrical-screwdrivers/` (body_1–7.stl, dxf) and `source/step/wera-electrical-screwdrivers/`
- 6-piece set; 7 tooltrace bodies (body_7 is likely the rack/holder)

---

## Empty / Stub Locations

- `gridfinity/stl/base/baseplates/magnet/` — STL exports of baseplates (not yet exported)
- `gridfinity/stl/inserts/wera-electrical-screwdrivers/` — STL pending Onshape export
- `gridfinity/3mf/allen-wrenches/` — 3MF pending Bambu Studio build
- `gridfinity/3mf/grids/` — layout grid builds (not started)
- `gridfinity/source/onshape/links.md` — Onshape document URLs (stub only; no docs created yet)
- `gridfinity/docs/notes.md` — design decisions and fit observations (stub only)

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
