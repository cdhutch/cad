# CAD Repo Conventions

## Structure
- Each major project gets its own top-level folder.
- Within a project:
  - `source/` contains editable or exchange CAD sources
  - `stl/` contains printable/exported geometry
  - `3mf/` contains slicer/project/build files
  - `docs/` contains project-specific notes and naming conventions

## Naming
- Prefer lowercase
- Use hyphens for free-text descriptors
- Include version suffixes such as `_v1`, `_v2`
- Use semantic folders before long filenames where practical

## File Types
- `.3mf` for slicer/build projects
- `.stl` for mesh exports
- `.step` / `.stp` for exchange geometry
