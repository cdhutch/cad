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

## Repo Structure

```
cad/
├── CLAUDE.md                        ← this file
├── README.md                        ← human-facing overview
├── .gitattributes                   ← Git LFS tracking (*.stl, *.3mf, *.step, *.stp)
├── docs/
│   └── repo-conventions.md          ← naming rules and folder conventions
└── gridfinity/                      ← only project currently
    ├── README.md
    ├── docs/
    │   ├── naming.md                ← filename convention spec
    │   ├── notes.md                 ← design notes (stub — populate as decisions are made)
    │   └── drill_tray_generator.md  ← step-by-step Onshape guide for parametric drill trays
    ├── source/
    │   ├── onshape/
    │   │   └── links.md             ← Onshape document URLs (stub — add links as docs are created)
    │   └── step/                    ← STEP exports for interoperability (currently empty)
    ├── stl/
    │   └── base/
    │       └── baseplates/
    │           └── magnet/          ← STL baseplate exports (currently empty)
    └── 3mf/
        ├── baseplates/
        │   └── magnet/              ← 2 baseplate slicer builds (see below)
        ├── grids/                   ← layout grids (currently empty)
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

---

## Empty Placeholders (Planned, Not Yet Populated)

- `gridfinity/source/step/` — STEP exports for CAD interoperability
- `gridfinity/stl/base/baseplates/magnet/` — STL exports of baseplates
- `gridfinity/3mf/grids/` — layout grid builds
- `gridfinity/source/onshape/links.md` — Onshape document URLs (stub only)
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

1. **tooltrace.ai**: Photograph the tool against a reference surface to extract a 2D profile (DXF or SVG)
2. **Onshape**: Import the profile, build a holder body around it, apply Gridfinity bin geometry (lip, stacking interface, optional magnet pockets)
3. **Export STL** from Onshape → save to `gridfinity/stl/`
4. **Slice in Bambu Studio** → save `.3mf` project to `gridfinity/3mf/<project-name>/`
5. **Update `links.md`** with the Onshape document URL and version/config notes

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
