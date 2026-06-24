# NACA 2412 Airfoil CFD Analysis (ANSYS)

CFD study of a **NACA 2412** airfoil at **0° and 8° angle of attack**, using ANSYS with the **SST k-ω** turbulence model on a structured C-domain mesh. Airfoil coordinates were sourced from [Airfoil Tools](http://airfoiltools.com/) and the geometry, meshing, and post-processing were all done within ANSYS Workbench.

---

## 1. Overview

This repository contains the setup, meshing strategy, boundary conditions, and results for a steady, incompressible RANS simulation of a NACA 2412 airfoil. The goal was to visualize and compare the flow field (velocity/pressure distribution) around the airfoil at two angles of attack: 0° (baseline) and 8°.

---

## 2. Geometry

| Parameter | Value |
|---|---|
| Airfoil | NACA 2412 |
| Coordinate source | airfoiltools.com (200-point coordinate file, CSV) |
| Chord length | 1 m |
| Domain shape | C-shaped far-field domain (better wake/accuracy capture than a plain rectangular domain) |
| Leading-edge enclosure | C-shape: R = 7.5 m, L = 15 m, H = 15 m |
| Trailing edge treatment | Vertical split line added at the trailing edge for cleaner mesh transition in the wake region |
| Geometry split | Divided into 6 regions to allow structured/quad-dominant meshing |

---

## 3. Mesh

- Domain split into **6 regions**, each meshed independently for better control and quality.
- **Bias factor of 50,000** applied to the edges near the airfoil surface to heavily cluster cells close to the airfoil (capturing steep near-wall gradients).
- Vertical trailing-edge split line used specifically to improve mesh quality/transition in that region.

---

## 4. Solver Setup

| Parameter | Value |
|---|---|
| Solver | ANSYS Fluent *(edit if CFX was used instead)* |
| Turbulence model | SST k-ω |
| Simulation type | Steady-state |
| Wall friction | Not considered in this analysis |
| Freestream (inlet) velocity | 45.6 m/s |
| Reynolds number | 3.1 × 10⁶ (based on 1 m chord) |

---

## 5. Case Parameters

The inlet velocity was decomposed into x and y components based on angle of attack (Vx = V·cos α, Vy = V·sin α).

| Angle of Attack | Vx (m/s) | Vy (m/s) | Reynolds No. |
|---|---|---|---|
| 0° | 45.6 | 0 | 3.1 million |
| 8° | 45.156 | 6.34 | 3.1 million |

---

## 6. Methodology / Workflow

1. Downloaded the 200-point NACA 2412 coordinate file (CSV) from airfoiltools.com.
2. Imported the CSV into ANSYS (DesignModeler/SpaceClaim) and scaled the profile to a 1 m chord.
3. Built a C-shaped far-field enclosure around the airfoil (R = 7.5 m, L = 15 m, H = 15 m) for the leading-edge region, extended into a full C-domain.
4. Split the geometry into 6 regions and added a vertical line at the trailing edge to improve local mesh quality.
5. Meshed each region, applying a bias factor of 50,000 on edges near the airfoil to refine the boundary layer region.
6. Set up the case in Fluent: steady, pressure-based solver, SST k-ω turbulence model.
7. Applied a velocity inlet of 45.6 m/s, resolved into Vx/Vy components for the 8° case.
8. Ran simulations for α = 0° and α = 8°.
9. Post-processed and visualized the velocity and pressure flow fields for both cases (contours/streamlines around the airfoil).

> **Note / limitation:** Wall friction (viscous shear at the airfoil surface) was not accounted for in this analysis.

---

## 7. Results

Flow visualizations (velocity contours, pressure contours, streamlines) for both angles of attack are included below.

<!-- Add your images here, e.g.: -->
<!-- ![Velocity contour - 0 deg](images/velocity_0deg.png) -->
<!-- ![Velocity contour - 8 deg](images/velocity_8deg.png) -->
<!-- ![Pressure contour - 8 deg](images/pressure_8deg.png) -->
<!-- ![Mesh near airfoil](images/mesh_closeup.png) -->

---

## 8. Repository Structure

```
.
├── README.md
├── geometry/        # Airfoil CSV, geometry files
├── mesh/             # Mesh files / screenshots
├── results/          # Result files
└── images/           # Result/flow visualization images for this README
```

---

## 9. Tools Used

- ANSYS Workbench (Geometry, Meshing, Fluent)
- Airfoil coordinates: [airfoiltools.com](http://airfoiltools.com/)

---

## 10. Credits

- NACA 2412 airfoil coordinate data: Airfoil Tools (airfoiltools.com)
