# CAD Repo Conventions

## Structure
- Each major project gets its own top-level folder (see `CLAUDE.md` → "Adding New Projects").
- Within a project:
  - `source/` contains editable or exchange CAD sources (e.g. Onshape links, STEP imports, tooltrace exports)
  - `stl/` contains printable/exported mesh geometry
  - `3mf/` contains slicer/project/build files
  - `docs/` contains project-specific notes and naming conventions

Within `stl/` and `3mf/`, split by role first (e.g. `baseplates/`, `grids/`, `inserts/`),
then by tool/part underneath — keep that split consistent between `stl/` and `3mf/`
rather than nesting extra nearly-synonymous folders (e.g. avoid `stl/base/baseplates/`;
use `stl/baseplates/` directly, matching `3mf/baseplates/`).

## Naming
- Prefer lowercase
- Use hyphens for free-text descriptors
- Include version suffixes such as `_v1`, `_v2`
- Use semantic folders before long filenames where practical
- Full pattern and Gridfinity-specific details: `gridfinity/docs/naming.md`

## File Types
- `.3mf` for slicer/build projects
- `.stl` for mesh exports
- `.step` / `.stp` for exchange geometry
- `.dxf` for 2D trace/sketch reference geometry (tooltrace exports)

All of the above are tracked via Git LFS — see the repo's `.gitattributes`.
