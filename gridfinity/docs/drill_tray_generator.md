# Parametric Drill Bit Tray Generator (Onshape)

This document describes how to build a **parametric drill-bit tray
generator** in Onshape.\
The goal is a single Part Studio that can generate trays for multiple
drill sets such as:

-   fractional
-   letter
-   number
-   metric
-   left-hand

The model should allow easy changes to tray size, hole spacing, and
drill diameters.

------------------------------------------------------------------------

# Design Goals

The generator should allow control over:

-   tray size (Gridfinity or custom drawer)
-   number of holes
-   hole diameters
-   hole spacing
-   labels
-   margins and walls

------------------------------------------------------------------------

# Step 1 --- Create Variables

At the top of the Part Studio create variables.

Example:

    #tray_width
    #tray_depth
    #tray_height = 12 mm

    #margin = 3 mm
    #row_spacing = 12 mm
    #column_spacing = 12 mm

    #hole_depth = 10 mm
    #wall_thickness = 1.6 mm

For Gridfinity compatibility:

    #grid = 42 mm
    #tray_width = 3 * #grid
    #tray_depth = 2 * #grid

------------------------------------------------------------------------

# Step 2 --- Tray Body

Create **Sketch 1 on the Top Plane**.

Draw a rectangle:

    width = #tray_width
    height = #tray_depth

Extrude the sketch:

    height = #tray_height

You now have the tray body.

------------------------------------------------------------------------

# Step 3 --- Pocket the Tray

Create a sketch on the **top face**.

Offset the outer rectangle:

    offset = #wall_thickness

Extrude remove:

    depth = #tray_height - 2 mm

This creates the interior tray pocket.

------------------------------------------------------------------------

# Step 4 --- Hole Pattern Layout

Create a sketch on the **tray floor**.

Place the first hole center:

    x = #margin
    y = #margin

Define spacing:

    horizontal spacing = #column_spacing
    vertical spacing = #row_spacing

------------------------------------------------------------------------

# Step 5 --- Hole Feature

Use the **Hole Tool** rather than extrude.

    diameter = configured
    depth = #hole_depth

Later this diameter will be controlled by configurations.

------------------------------------------------------------------------

# Step 6 --- Linear Pattern

Pattern the hole feature.

    columns = variable
    rows = variable
    spacing = #column_spacing / #row_spacing

This creates a grid of holes.

------------------------------------------------------------------------

# Step 7 --- Label Sketch

Create text labels near each hole.

Example:

    1/16
    3/32
    1/8
    5/32

Extrude remove:

    depth = 0.4 mm

This engraves the labels.

------------------------------------------------------------------------

# Step 8 --- Fillets

Add comfort edges:

    top edge fillet = 1 mm
    hole chamfer = 0.5 mm

------------------------------------------------------------------------

# Step 9 --- Configurations

Create configuration options such as:

    drill_set = fractional | letter | number | metric

Each configuration controls:

-   hole diameters
-   number of holes
-   label text

Example:

  Set          Holes
  ------------ ----------
  Fractional   29
  Letter       26
  Number       80
  Metric       variable

------------------------------------------------------------------------

# Step 10 --- Export Workflow

For each configuration:

1.  Right-click the part
2.  Export STL

Then create plate layouts in your slicer (for example Bambu Studio) and
save them as `.3mf`.

------------------------------------------------------------------------

# Recommended Feature Order

Your Onshape feature tree should look like:

    Variables
    Sketch: tray footprint
    Extrude: tray body
    Sketch: pocket
    Extrude remove
    Sketch: hole layout
    Hole feature
    Linear pattern
    Sketch: labels
    Extrude remove
    Fillets
    Configurations

Keeping the feature tree clean makes future edits much easier.

------------------------------------------------------------------------

# Possible Future Improvements

Instead of fixed hole sizes, hole diameters can be driven from a table
of drill sizes.

Example fractional set:

    1/16
    5/64
    3/32
    7/64
    1/8
    ...
    1/2

This allows a single model to generate multiple tray variants
automatically.
