# CAD Library

A general repository for CAD models and 3D-printing assets.

This repo contains original designs, modified models, and organized
assets used for prototyping, shop organization, and hardware projects.

## Repository Structure

    3mf/    Printable project files and slicer-ready builds
    stl/    Exported geometry for printing or reuse
    docs/   Documentation and conventions

### `3mf/`

Project files in **3MF format**, typically exported from slicers. These
may contain:

-   multiple objects
-   build plates
-   print settings
-   supports
-   arranged layouts

Subdirectories organize projects or systems (for example `grids/` or
`nystrom_performance/`).

### `stl/`

Raw geometry intended for printing or remixing.

Current organization follows a functional hierarchy such as:

    stl/
      base/
        baseplates/
          magnet/

### `docs/`

Repository documentation.

Currently includes:

    docs/naming.md

which describes file naming conventions for exported models.

## Conventions

-   Prefer **`.3mf` for printable projects**
-   Use **`.stl` for distributable geometry**
-   Keep slicer-specific files in `3mf/`
-   Follow naming rules in `docs/naming.md`

## Included Systems

Currently includes models related to:

-   Gridfinity-compatible storage
-   Shop drawer organizers
-   Custom tray layouts

Additional CAD projects may be added over time.
