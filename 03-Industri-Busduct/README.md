# 03 — Industrial Facility: Busduct Distribution

Manufacturing facility 40 × 25 m, 8 m high, single storey. Power flows **Utility / Genset → ATS → LVMDP → Main Busduct → Tap-off → MCC/DB → Industrial Loads**, modelled with native Revit electrical circuits so that panel schedules and load totals are calculated by Revit.

![Render](images/01_3D-03_Render_Perspective.png)

## System

| Item | Value (training example) |
|---|---|
| Utility supply | TR-01 cast resin transformer 1000 kVA, 20 / 0.4 kV, Dyn11 |
| Standby supply | GEN-01 diesel generator set 500 kVA (outdoor, soundproof canopy, concrete pad) |
| Transfer | ATS-01 1600 A 4P, open transition, in line-up with LVMDP |
| System | 400/230 V, 50 Hz, 3P+N+PE (TN-S) |
| Main switchboard | LVMDP-01, 5 cubicles, ACB 1600 A, 50 kA + MPP-01 metering & protection |
| Power factor correction | CB-01 capacitor bank 100 kVAr, 6-step, detuned 7% |
| Main busduct | BUS-01 1600 A → JB-01 tee junction |
| Production busduct | BUS-02 800 A, 27.7 m, TP-01…TP-04 |
| Auxiliary busduct | BUS-03 400 A, 5.3 m, TP-05 |
| Busduct elevation | CL +5.80 m, 17 hangers (max. spacing 3.0 m), beam soffit +7.70 m |
| Panels | MCC-01 (3 sections), DB-PROD, DB-UTIL, DB-OFFICE |
| Loads | 10 (hydraulic press, injection molding, packaging line, 2× CNC, conveyor motor, air compressor, pump, ventilation fan, split AC) |
| Connected load | 285.2 kVA (calculated by Revit at ATS-01 / LVMDP-01) |
| Earthing | 3 earth pits (Cu-bonded rod 16 mm × 3 m), BC 95 mm² ring → MEB-01 → TR-01, GEN-01, LVMDP-01 |
| Native circuits | 17 (10 load circuits, 6 panel feeders, LVMDP-01 ← ATS-01) |

```
PLN 20 kV ─ TR-01 1000 kVA ─┐
                             ATS-01 ─ MPP-01 ─ LVMDP-01 ─┬─ BUS-01 1600A ─ JB-01 ─┬─ BUS-02 800A ─ TP-01 ─ MCC-01-S1 ─ PM-01 Hydraulic Press
GEN-01 500 kVA ──────────────┘                            │                         │               TP-02 ─ MCC-01-S2 ─ MTR-01 Conveyor
                                                          │                         │               TP-03 ─ MCC-01-S3 ─ CNC-01 Machining Center
                                                          │                         │               TP-04 ─ DB-PROD  ─ PM-02, PM-03, CNC-02
                                                          │                         └─ BUS-03 400A ─ TP-05 ─ DB-UTIL  ─ COMP-01, PMP-01, VF-01
                                                          ├─ Cable ─ DB-OFFICE ─ AC-01
                                                          └─ CB-01 capacitor bank 100 kVAr
EP-01..03 ─ BC 95 mm² ─ MEB-01 ─ PE of TR-01, GEN-01, ATS-01, LVMDP-01
```

## Images

| | |
|---|---|
| ![](images/02_3D-02_Electrical_System.png) 3D electrical system | ![](images/03_3D-01_Overall_Isometric.png) Overall isometric |
| ![](images/04_EL-01_Electrical_Layout_Plan.png) Electrical layout plan | ![](images/05_EL-02_Busduct_Layout_Plan.png) Busduct layout plan |
| ![](images/06_EL-03_Electrical_Room_Plan.png) Electrical room plan | ![](images/07_EL-04_Production_Area_Plan.png) Production area plan |
| ![](images/08_Section_A-A_Main_Busduct_-_Longitudinal.png) Section A-A (main busduct) | ![](images/09_Section_B-B_Tap-off_TP-01_-_Transverse.png) Section B-B (tap-off) |

![Single line diagram](images/10_SLD-01_Single_Line_Diagram_Simplified.png)

## Sheets

Full set: [`sheets/Industri_Busduct_Sheets.pdf`](sheets/Industri_Busduct_Sheets.pdf) (11 × A1). PNG per sheet in [`sheets/png`](sheets/png).

| Sheet | Content |
|---|---|
| E-000 | Single line diagram & legend |
| E-101 | Electrical layout plan |
| E-102 | Busduct layout plan |
| E-103 | Electrical room plan & section B-B |
| E-104 | Production area plan |
| E-201 | Section A-A (main busduct) |
| E-301 | 3D views |
| E-401 | Busduct, tap-off & distribution schedules |
| E-402 | Equipment & electrical circuit schedules |
| E-403 / E-404 | Native panel schedules (DB, MCC, LVMDP) |

## Modelling approach

- **Parametric families** — busduct, tap-off, junction, switchboards, MCC, DBs, ATS, capacitor bank, genset, earth pit and main earth bar are built on reference planes with labelled dimensions (Width / Depth / Height, busduct `Section Length`, earth rod `Rod Length`) and equality constraints, so they flex correctly. Multi-type families come with **type catalogs** (`.txt`): `BUS_Straight Length` (1600 / 800 / 400 A), `TP_Plug-in Tap-off Unit` (MCCB 63–250 A), `EQ_DB Wall Mounted`.
- **Busduct** — Revit has no busduct category, so busduct runs, elbow, tee, flanged end, end caps, hangers and tap-offs are *Electrical Equipment* families.
- **Connectivity** — the busduct → tap-off → panel link is represented in three layers: geometry (busduct + cable trays with native fittings), native power circuits (MCC/DB fed from LVMDP-01, LVMDP-01 fed from ATS-01; route noted in circuit comments) and shared parameters (`Connected From`, `Connected To`, `Busduct`).
- **Loads** — Mechanical Equipment families with a Power–Balanced connector (voltage, poles, apparent load, PF 0.85).
- **Standards** — English naming throughout, shared parameters, 10 view filters (one colour per system, including earthing), view templates `E-Plan Electrical (Busduct & Power)`, `E-Plan Busduct Only`, `E-Section Electrical`, `E-3D Electrical System`.
- **QC** — 0 clashes of busduct, cable trays, earthing conductors and equipment with columns, beams and roof; 0 clashes between cable trays and equipment; wall crossings are intentional penetrations; all 57 equipment have IDs; all 10 loads circuited and reached by a tray; busduct centreline consistent at +5800 mm.

## Files

- `model/Industri_Busduct.rvt` — Revit 2025 model
- `model/Industri_SharedParameters.txt` — shared parameter file
- `families/` — custom families (BUS_*, TP_*, EQ_*, GEN_*, LD_*, STR_*) and type catalogs

All ratings and sizes are training examples, not a final electrical design.
