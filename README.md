# Revit Electrical BIM Portfolio — LV Busduct Distribution

Three Autodesk Revit 2025 projects that model low-voltage power distribution with **busduct (busway)**, from a simple house to a 5-storey building and an industrial facility. Each project includes the native `.rvt` model, the custom families, sheets (PDF + PNG), and rendered views.

![Industrial facility – electrical system](03-Industri-Busduct/images/01_3D-03_Render_Perspective.png)

| # | Project | Scope | Highlights |
|---|---|---|---|
| 01 | [Simple House + Busduct](01-Rumah-Sederhana-Busduct/) | 1 storey house, 10 × 8 m | Architectural model, 400 A busduct scheme, MDP → tap-off → 3 sub-panels |
| 02 | [5-Storey Building – Vertical Busduct Riser](02-Gedung-5-Lantai-Busduct/) | 20 × 15 m, 5 floors @ 4 m | LVMDP → 800 A vertical riser in electrical shaft → tap-off per floor → DB-L1…L5 → loads |
| 03 | [Industrial Facility – Busduct Distribution](03-Industri-Busduct/) | 40 × 25 m factory, 8 m high | Transformer → LVMDP → 1600 A main busduct → 800 A / 400 A branches → 5 tap-offs → MCC/DB → 10 industrial loads, **native Revit circuits & panel schedules** |

## Skills demonstrated

- **Revit modeling** — levels, grids, walls, steel columns/beams, roofs, stairs, rooms, openings.
- **Family creation** — parametric busduct sections (`Section Length`), elbows, tee junction, tap-off units, hangers, switchboards, MCC, DBs and industrial loads with **electrical connectors** (voltage, poles, apparent load).
- **Electrical BIM** — custom 400/230 V 3P4W 50 Hz distribution system, power circuits, panel/load assignment, automatic load totals (285.2 kVA on LVMDP-01 in project 03).
- **Data** — shared parameters (Equipment ID, System, Voltage, Phase, Rating, Power, Area, Connected From/To…), multi-category and circuit schedules, native panel schedules.
- **Coordination** — routing clear of structure, clash check vs columns/beams (0 clashes), consistent busduct elevation (CL +5.80 m), hanger spacing ≤ 3.0 m.
- **Documentation** — view filters / graphic overrides per system, tags, plans, sections through busduct and tap-off, 3D views, single-line diagram, sheets.

## Colour code used in all views

| Colour | System |
|---|---|
| Orange | Busduct |
| Yellow | Tap-off units |
| Red | Transformer / LVMDP / MDP |
| Blue | MCC & distribution boards |
| Green | Feeder cable tray (tap-off → panel) |
| Cyan | Outgoing cable tray (panel → loads) |
| Purple | Electrical loads |
| Grey / halftone | Architecture & structure |

## Repository structure

```
01-Rumah-Sederhana-Busduct/
02-Gedung-5-Lantai-Busduct/
03-Industri-Busduct/
    model/      .rvt model (+ shared parameter file)
    families/   custom .rfa families
    sheets/     sheet set (PDF) and sheets/png (one PNG per sheet)
    images/     3D views, render, plans, sections
```

## How to open

1. Autodesk Revit **2025** or newer (files are saved in Revit 2025 format).
2. Open `model/*.rvt`. Custom families are already loaded in the model. The `families/` folder is provided for reuse.
3. For shared parameters, point *Manage → Shared Parameters* to the `.txt` file in `model/`.

## Disclaimer

All ratings, sizes and capacities (kVA, A, kW, cable sizes, clearances) are **training examples**, not results of an electrical design. Final values must come from load calculation, voltage drop, short-circuit calculation, protection coordination and the applicable standards (e.g. PUIL 2020, IEC 60364, IEC 61439-6).
