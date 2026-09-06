# CAD Library

A general repository for CAD models and 3D-printing assets.

This repository stores parametric design references, exported geometry,
and slicer projects used for prototyping, shop organization, and
hardware builds.

For the fuller working context (active branch, per-project inventory,
step-by-step workflow) see `CLAUDE.md`.

## Design Workflow (summary)

1. **tooltrace.ai** — photograph a tool to extract its 2D/3D profile (STEP + DXF)
2. **Onshape** — import the profile, subtract it from a Gridfinity tray body
3. **Export** — STL for remixing, `.3mf` slicer projects (Bambu Studio) for printing

## Repository Structure

    cad/
    ├── README.md
    ├── CLAUDE.md
    ├── docs/
    │   └── repo-conventions.md
    └── gridfinity/
        ├── README.md
        ├── docs/
        │   ├── naming.md
        │   ├── notes.md
        │   ├── allen-wrench-tray.md
        │   ├── wera-electrical-screwdrivers-tray.md
        │   └── drill_tray_generator.md
        ├── source/
        │   ├── onshape/
        │   │   └── links.md
        │   ├── step/
        │   │   ├── allen-wrenches/
        │   │   └── wera-electrical-screwdrivers/
        │   └── tooltrace/
        │       ├── allen-wrenches/
        │       └── wera-electrical-screwdrivers/
        ├── stl/
        │   ├── baseplates/
        │   │   └── magnet/
        │   └── inserts/
        │       ├── allen-wrenches/
        │       └── wera-electrical-screwdrivers/
        └── 3mf/
            ├── baseplates/
            │   └── magnet/
            ├── grids/
            ├── allen-wrenches/
            ├── nystrom_performance/
            └── wera-electrical-screwdrivers/

## Directory Purpose

### `docs/`

General documentation for the CAD repository: repo conventions, naming
rules, organizational guidance.

### `gridfinity/`

Gridfinity-compatible storage designs and experiments.

#### `source/`

Editable or reference CAD information: Onshape document links, STEP
exports for interoperability, and raw tooltrace.ai exports (STL + DXF)
kept as reference/import material.

#### `stl/`

Printable mesh geometry exported from CAD, split into `baseplates/`
(generic Gridfinity infrastructure) and `inserts/` (tool-specific trays).

#### `3mf/`

Slicer project files (Bambu Studio builds) — plate layouts, supports,
print profiles, often multiple parts per build. Subdirectories organize
prints by role or project, e.g. `baseplates/`, `grids/`, `nystrom_performance/`.

#### `docs/`

Project-specific notes, naming conventions, and per-tool design write-ups.

## File Type Conventions

Preferred formats and naming rules are defined in `docs/repo-conventions.md`
and, for Gridfinity specifics, `gridfinity/docs/naming.md`. In short:
lowercase, hyphenated, version-suffixed filenames; `.3mf`/`.stl`/`.step`/`.stp`/`.dxf`,
all tracked via Git LFS.

## Included Systems

Currently includes:

- Gridfinity storage components (baseplates, grids)
- Drawer organization trays (Nystrom Performance cabinet)
- Custom tool-specific inserts (Allen wrenches, Wera screwdrivers)

Additional CAD projects may be added as new top-level folders alongside
`gridfinity/`, following `docs/repo-conventions.md`.
