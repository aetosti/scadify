# Scadify — STL to OpenSCAD Converter

> Convert `.STL` mesh files into reusable OpenSCAD `polyhedron()` modules with live 3D preview, mesh analysis, and export tooling.

---

## Overview

**Scadify** is a desktop GUI application for converting 3D mesh files (`.STL`) into OpenSCAD-compatible `.SCAD` modules.

It provides:

- Interactive 3D mesh preview
- STL → OpenSCAD conversion
- Mesh statistics and diagnostics
- Scaling and centering tools
- Face winding correction
- Clean SCAD export generation

Scadify is designed for OpenSCAD workflows, CAD pipelines, and procedural modeling pipelines where STL meshes need to integrate with parametric OpenSCAD designs.

---

# Features

| Feature | Description |
|---|---|
| STL → SCAD Conversion | Converts STL meshes into OpenSCAD `polyhedron()` geometry |
| Live 3D Preview | Interactive mesh visualization |
| Wireframe + Solid Rendering | Inspect topology or final appearance |
| Mesh Statistics | Triangle count, vertices, dimensions |
| Adjustable Scaling | Resize models before export |
| Decimal Precision Control | Balance accuracy vs file size |
| Center Mesh Option | Automatically move mesh to origin |
| Face Winding Correction | Fix inverted normals |
| Multi-threaded Processing | Responsive UI during loading/conversion |
| Progress Tracking | Real-time conversion progress |

---

# Use Cases

Scadify is useful for:

- OpenSCAD workflows
- Procedural CAD pipelines
- 3D printing preparation
- Combining STL assets with parametric OpenSCAD designs
- Mesh cleanup and conversion
- Reverse engineering workflows

---

# Installation

## Clone Repository

```bash
git clone https://github.com/yourusername/scadify.git
cd scadify
```

---

## Install Requirements

### Using `requirements.txt`

```bash
pip install -r requirements.txt
```

### Manual Installation

```bash
pip install numpy numpy-stl matplotlib
```

---

# Requirements

| Dependency | Purpose |
|---|---|
| `numpy` | Numerical processing |
| `numpy-stl` | STL mesh loading |
| `matplotlib` | 3D preview rendering |

---

# Running the Application

```bash
python main.py
```

---

# GUI Overview

| Area | Description |
|---|---|
| Left Panel | File selection and conversion settings |
| Right Panel | 3D preview, SCAD output, logs |
| Bottom Bar | Status and progress information |

---

# FILES Section

## STL Input

Used to select the source `.stl` file.

### Browse Button

Opens a file dialog for selecting an STL mesh.

### Supported Formats

- Binary STL
- ASCII STL

---

## SCAD Output

Defines where the generated `.scad` file will be saved.

### Automatic Output Naming

If no output path is chosen:

```text
model.stl → model.scad
```

is generated automatically.

---

# MODULE Section

## Module Name

Defines the generated OpenSCAD module name.

### Example Generated Output

```scad
module gearbox() {
```

This allows the geometry to be reused inside OpenSCAD projects.

### Example Usage

```scad
gearbox();

translate([20,0,0])
gearbox();
```

---

## Scale Factor

Scales the mesh before export.

| Value | Result |
|---|---|
| `1.0` | Original size |
| `2.0` | Double size |
| `0.5` | Half size |

### Common Unit Conversions

| Conversion | Scale |
|---|---|
| mm → cm | `0.1` |
| inches → mm | `25.4` |

---

## Decimal Precision

Controls how many decimal places are written into the SCAD file.

### Lower Precision

- Smaller files
- Faster OpenSCAD rendering

### Higher Precision

- More accurate geometry
- Larger file size

### Recommended

```text
4
```

usually provides the best balance.

---

## Convexity

Controls OpenSCAD's `convexity` setting.

### Purpose

Helps OpenSCAD correctly preview complex geometry.

### Recommended Values

| Mesh Complexity | Suggested Value |
|---|---|
| Simple | `2–5` |
| Medium | `10` |
| Complex | `20+` |

> **Important:** Convexity does **not** modify model geometry.  
> It only affects OpenSCAD preview rendering behavior.

---

# OPTIONS Section

## Center Mesh at Origin

Moves the mesh center to:

```text
(0,0,0)
```

### Useful For

- Rotation
- Symmetrical operations
- Assembly alignment
- Easier OpenSCAD transformations

---

# MESH INFO Section

Displays information about the loaded STL mesh.

---

## Triangles

Number of mesh triangles.

Higher values generally mean:

- More detail
- Larger SCAD files
- Slower rendering

---

## Vertices

Unique vertex count after optimization.

Scadify automatically removes duplicate vertices.

---

## Size X / Y / Z

Bounding box dimensions of the mesh.

Useful for:

- Print sizing
- Scale verification
- CAD measurements

---

# Buttons

| Button | Action |
|---|---|
| Load STL | Loads and analyzes the selected STL file |
| Convert to SCAD | Generates the OpenSCAD output |

---

# 3D Preview Tab

Interactive mesh viewer.

---

## Preview Modes

### Solid Mode

Displays filled surfaces.

Best for:

- Surface inspection
- Final appearance checking

---

### Wire Mode

Displays mesh edges only.

Best for:

- Topology inspection
- Dense mesh debugging

---

## Automatic Preview Optimization

Large meshes are automatically simplified for preview rendering.

### Why?

This prevents UI lag and keeps interaction responsive.

---

# SCAD Output Tab

Displays generated OpenSCAD code.

---

## Available Actions

| Action | Description |
|---|---|
| Copy All | Copies generated SCAD code to clipboard |
| Save | Saves SCAD output manually |

---

## Statistics Display

Shows:

- Line count
- Output file size

---

# Log Tab

Displays application activity and errors.

### Example Logs

```text
[12:41:22] Loading: model.stl
[12:41:24] OK triangles=120000
[12:41:31] Saved: model.scad
```

---

# Generated OpenSCAD Structure

Generated SCAD files include:

- Reusable module definition
- Vertex point arrays
- Face index arrays
- Optional module call

---

# Typical Workflow

| Step | Action |
|---|---|
| 1 | Load an STL file |
| 2 | Inspect the mesh in the 3D preview |
| 3 | Adjust scaling, precision, centering, or winding |
| 4 | Convert to SCAD |
| 5 | Open generated file in OpenSCAD |
| 6 | Reuse the module inside larger projects |

---

# Example OpenSCAD Integration

```scad
include <gearbox.scad>

translate([0,0,10])
gearbox();
```

---

# Tips

| Recommendation | Reason |
|---|---|
| Use lower precision for huge meshes | Reduces SCAD file size |
| Enable centering for assemblies | Easier positioning |
| Use wireframe mode for debugging | Better topology visibility |
| Increase convexity for complex models | Improves OpenSCAD preview accuracy |

---

# Known Limitations

- Very high polygon meshes may generate extremely large SCAD files
- OpenSCAD performance depends heavily on mesh complexity
- Preview simplification only affects rendering, not export quality

---
