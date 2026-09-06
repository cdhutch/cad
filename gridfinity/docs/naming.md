# Naming convention

    <name>_<WxD>x<height-u>u_<variant>_v<major>[.<minor>].<ext>

Applies to every exported file — `.stl`, `.3mf`, `.step`/`.stp` — not just STL.

- `W` and `D` are Gridfinity grid units (1 unit = 42 mm)
- `height-u` is height in Gridfinity height units (7 mm per unit)
- `variant` describes fit or subtype (e.g. `magnet`, `loose`, `snug`, `sae`, `metric`)
- Version suffix: `_v1`, `_v2`, or `_v1.1` for a minor revision

Examples:
- `baseplate_4x4x0u_magnet_v1.stl`
- `calipers-holder_2x1x6u_loose_v1.1.stl`
- `wera-kraftform-160i-tray_4x6x3.9u_v1.3mf`

General rules (see `../../docs/repo-conventions.md` for the repo-wide version):
- Lowercase filenames
- Hyphens for multi-word descriptors
- Version suffix on every exported file
