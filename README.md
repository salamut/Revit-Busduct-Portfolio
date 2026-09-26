# Revit Electrical Portfolio — LV Busduct Distribution

**Muhammad Sabiq Almuttaqin**

Three Revit 2025 projects on low-voltage power distribution with busduct: a small house, a 5-storey building with a vertical busduct riser, and a factory with a horizontal busduct system. Each folder has the `.rvt` model, families, sheets (PDF + PNG) and images.

![Industrial facility](03-Industri-Busduct/images/01_3D-03_Render_Perspective.png)

## Projects

| # | Project | What it shows |
|---|---|---|
| 01 | [Simple house](01-Rumah-Sederhana-Busduct/) | 10 × 8 m house, MDP → 400 A busduct in the corridor → 3 sub-panels |
| 02 | [5-storey building](02-Gedung-5-Lantai-Busduct/) | LVMDP → 800 A riser in an electrical shaft → tap-off on every floor → DB-L1…L5 → loads |
| 03 | [Industrial facility](03-Industri-Busduct/) | Transformer → LVMDP → 1600 A main busduct → 800 A / 400 A branches → 5 tap-offs → MCC & DBs → 10 machines, with Revit circuits and panel schedules |

## How this was built

I used AI-assisted automation (Revit API) to speed up the modelling. My part was the engineering and the review:

- defined the distribution concept for each building: topology, busduct ratings, routing, elevations, tap-off and panel positions;
- checked the model: clash check against structure, busduct continuity, circuit and panel assignments, schedules;
- fixed the problems found (e.g. cable tray elbows inside walls, distribution system voltage setup, overlapping tags and sheets);
- set up the documentation: view filters, tags, sections, sheets.

A fully manual rebuild of Project 03 in Revit is in progress (October 2026) and will be added to this repository.

## Colour code

Orange = busduct · Yellow = tap-off · Red = transformer / LVMDP · Blue = MCC / DB · Green = feeder tray · Cyan = outgoing tray · Purple = loads · Grey = architecture & structure

## Folder structure

```
0X-<project>/
  model/     .rvt (+ shared parameter file)
  families/  custom .rfa families
  sheets/    PDF sheet set, and png/ with one image per sheet
  images/    3D views, plans, sections
```

Open with Revit 2025 or newer.

## Note

Ratings, cable sizes and capacities are example values for practice, not a checked electrical design. A real design needs load calculation, voltage drop, short-circuit and protection coordination studies according to PUIL 2020 / IEC.
