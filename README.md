# CAD Library

A general repository for CAD models and 3D‑printing assets.

This repository stores parametric design references, exported geometry,
and slicer projects used for prototyping, shop organization, and
hardware builds.

## Repository Structure

    cad/
    ├── README.md
    ├── docs/
    │   └── repo-conventions.md
    └── gridfinity/
        ├── README.md
        ├── docs/
        │   ├── naming.md
        │   └── notes.md
        ├── source/
        │   ├── onshape/
        │   │   └── links.md
        │   └── step/
        ├── stl/
        │   └── base/
        │       └── baseplates/
        │           └── magnet/
        └── 3mf/
            ├── baseplates/
            │   └── magnet/
            ├── grids/
            └── nystrom_performance/

## Directory Purpose

### `docs/`

General documentation for the CAD repository.

Includes:

-   repository conventions
-   naming rules
-   organizational guidance

### `gridfinity/`

Gridfinity‑compatible storage designs and experiments.

#### `source/`

Editable or reference CAD information.

Typical contents:

-   links to Onshape documents
-   STEP exports for interoperability

#### `stl/`

Printable mesh geometry exported from CAD.

These files are suitable for remixing or slicing.

#### `3mf/`

Slicer project files (for example Bambu Studio builds).

These often include:

-   plate layouts
-   supports
-   print profiles
-   multiple parts per build

Subdirectories organize prints by project or system.

Example:

-   `baseplates/` -- Gridfinity base frame builds
-   `grids/` -- layout grids
-   `nystrom_performance/` -- custom tool organization trays

#### `docs/`

Project‑specific notes and naming conventions.

## File Type Conventions

Preferred formats:

-   `.3mf` -- slicer project files
-   `.stl` -- printable mesh geometry
-   `.step` / `.stp` -- CAD exchange geometry

Large binary files are tracked using **Git LFS**.

## Naming Conventions

General rules:

-   lowercase filenames
-   hyphenated descriptors
-   version suffixes such as `_v1`, `_v2`, etc.

Detailed rules are defined in:

    gridfinity/docs/naming.md

## Included Systems

Currently includes:

-   Gridfinity storage components
-   drawer organization trays
-   custom tool‑specific inserts

Additional CAD projects may be added as new top‑level folders alongside
`gridfinity/`.
