# Bambu Studio Print Profile: Tool Tray — Minimal Filament

Optimized for **static tool trays** on Bambu Lab P1S/P2S printers. Minimizes filament usage while maintaining structural integrity.

## Profile Settings Summary

| Setting | Value | Rationale |
|---------|-------|-----------|
| **Infill density** | 10% | Static load only; 10% provides rigidity with minimal material |
| **Infill pattern** | Grid or Cubic | Balanced strength-to-weight; easy to print |
| **Wall thickness** | 1.2 mm | Single perimeter sufficient for tool tray walls |
| **Top layers** | 3 | Minimal; surface doesn't need heavy reinforcement |
| **Bottom layers** | 3 | Minimal; no load-bearing requirement |
| **Perimeters** | 1 | Single wall is adequate for static storage |
| **Support type** | Tree supports | Faster, uses less filament than linear supports |
| **Support density** | 15% | Minimal; reduces material and print time |
| **Nozzle temperature** | Material default | PLA: 210°C, PETG: 230°C, ABS: 240°C |
| **Bed temperature** | Material default | PLA: 60°C, PETG: 80°C, ABS: 100°C |
| **Print speed** | 150–200 mm/s | Faster print times; static parts don't need slow speeds |
| **Layer height** | 0.2 mm | Standard; balances quality and speed |

## Optimization Notes

### Infill
- **10% is ideal** for tool trays—no bending loads, just containment
- Grid pattern provides consistent rigidity without waste
- Avoid sparse patterns (e.g., gyroid) at low % as they add complexity

### Walls & Perimeters
- **Single perimeter** (1.2 mm) is sufficient; tool trays don't need thick shells
- More perimeters add weight without meaningful benefit
- Keep top/bottom layers minimal (3 each); a tray doesn't need a solid block

### Supports
- **Tree supports** are default for P2S; they're efficient and break away cleanly
- **15% support density** is low but adequate for tray geometry
- If tray has deep overhangs (>45°), consider checking support preview before print

### Speed & Cooling
- Fast speeds are fine—static parts tolerate minor surface imperfections
- Default cooling is acceptable
- No benefit to slow speeds; print at 150–200 mm/s

### Material Choice
- **PLA** — easiest, fine for shelves; min. cost
- **PETG** — more durable; handles slight temperature variation
- **ABS** — overkill for a static tray; skip unless specifically needed
- **Multi-color via AMS** — color-code tool positions for organization, not strength

## Estimated Material Savings

Compared to default Bambu Studio settings:

| Factor | Default | Optimized | Saving |
|--------|---------|-----------|--------|
| Infill | 15% | 10% | ~33% |
| Perimeters | 2–3 | 1 | ~50% |
| Top/bottom | 4–5 each | 3 each | ~35% |
| **Combined** | — | — | **~45–55% less filament** |

Example: A tray using 100g at defaults → ~50g optimized

## When to Use This Profile

✅ Static tool storage trays (hand tools, drill bits, etc.)  
✅ Gridfinity-compatible inserts  
✅ Drawer organizers  
✅ Any non-structural storage  

❌ Functional parts needing strength (mechanical components, load-bearing)  
❌ Parts subject to impact or repeated stress  
❌ Outdoor or high-temperature use  

## How to Import

1. **Save the JSON profile** to your Bambu Studio profile directory:
   - **macOS**: `~/Library/Preferences/BambuStudio/process/`
   - **Windows**: `%APPDATA%\BambuStudio\process\`
   - **Linux**: `~/.config/BambuStudio/process/`

2. **Restart Bambu Studio** to see the profile in the Process tab

3. **Select the profile** when adding a model to your project plate

## Notes

- This profile is **material-agnostic**; adjust temperatures per your filament specs
- Test the first layer with your actual filament to confirm bed adhesion
- Monitor the first print to ensure supports break away cleanly
- No support blocker needed for tool trays; geometry is usually straightforward
