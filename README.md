# Naphtha Hydrodesulfurization — Process Simulation & Techno-Economic Analysis

> **Course:** Petroleum Refining | Chemical Engineering, IIT Indore — 2026  
> **Tool:** Aspen Plus v14 | Property Method: Grayson-Streed  
> **Team:** Group-3 — Aarav Gupta, Mitanshu Kumawat, Mohak Dadhich, Priyanshu Patel

---

## Overview

This project presents a rigorous steady-state simulation of a **Naphtha Hydrodesulfurization (HDS)** unit built in Aspen Plus v14, targeting <10 ppm sulfur in the product stream to meet modern fuel quality regulations. The work covers four interconnected modules:

1. **Process Simulation** — Full flowsheet with reaction, separation, and recycle
2. **Sensitivity Analysis** — Five key operating parameters varied systematically
3. **Heat Integration & Pinch Analysis** — via Aspen Energy Analyzer
4. **Techno-Economic Assessment (TEA)** — 20-year DCF model with CAPEX, OPEX, and profitability metrics

---

## Process Description

Sour naphtha (3,000 kg/hr, C₅–C₉ with four organosulfur species) reacts with hydrogen over a CoMo catalyst in a fixed-bed plug-flow reactor at **350°C, 40 bar**, converting all reactive sulfur compounds to H₂S with **100% conversion**.

```
Feed (Sour Naphtha + H₂)
        ↓
  [PUMP + MIXER]
        ↓
  [HX1] ← Heat Integration (reactor effluent)
        ↓
  [HX2] ← Fired Heater → 350°C
        ↓
  [RPlug REACTOR] — 350°C, 40 bar, CoMo catalyst
        ↓
  [HX3] ← Cooling to 35°C
        ↓
  [FLASH DRUM] — 4 bar
   ↙          ↘
Vapor         Liquid
  ↓               ↓
[ABSORBER]    [DISTILLATION]
 MDEA, 20       25 stages
 stages          1 bar
  ↓               ↓
H₂S removed   Sweet Naphtha
  ↓             (<10 ppm S)
[SPLITTER]
 90% Recycle + 10% Purge
  ↓
[COMP1 → COMP2] — 4 → 12.6 → 41 bar
  ↓
Back to MIXER
```

### Feed Specification

| Component | Mass Flow (kg/hr) | HDS Conversion |
|---|---|---|
| n-Pentane to n-Nonane (C₅–C₉) | 2,740.5 | — |
| Methyl mercaptan (CH₃SH) | 20.7 | **100%** |
| Ethyl mercaptan (C₂H₅SH) | 44.1 | **100%** |
| Butanethiol (C₄H₈S) | 31.2 | **100%** |
| Dibenzothiophene (C₁₂H₈S) | 163.5 | Stabilised |

### Key Block Configuration

| Block | Type | Key Parameters |
|---|---|---|
| REACTOR (RPlug) | Fixed-bed PFR | 350°C, 40 bar, L=20m, D=2m, Power-Law kinetics |
| ABSORBER (RadFrac) | Amine absorber | 20 stages, 4 bar, MDEA solvent |
| DIST (RadFrac) | Distillation | 25 stages, 1 bar |
| COMP1+2 | Two-stage compressor | 4 → 12.6 → 41 bar, intercooled at 80°C |
| SPLITTER | FSplit | 10% purge, 90% recycle |

---

## Sensitivity Analysis

Five operating parameters were varied one-at-a-time (OAT) in Aspen Plus sensitivity blocks:

| Parameter | Range | Key Finding |
|---|---|---|
| Lean amine flow rate | 10–300 kmol/hr | Optimum ~100 kmol/hr; beyond this, excess solvent dilutes H₂S partial pressure |
| Lean amine temperature | 25–60°C | 35–40°C is practical optimum; lower requires costly refrigeration for marginal gain |
| Flash drum pressure | 1–10 bar | **4 bar optimal** — higher pressure forces H₂S into liquid phase, burdening distillation |
| Purge fraction | 0–30% | Economic optimum 10–15%; beyond 20%, H₂ purity gains become marginal |
| Distillation stages | 5–35 | H₂S stripping plateaus at **17 stages**; base 25-stage design adds product quality margin |

---

## Heat Integration & Pinch Analysis

Performed using the **Aspen Energy Analyzer** with ΔT_min = 10°C.

| Utility | Before Integration | After Integration | Saving |
|---|---|---|---|
| Hot utility | 4.195 GJ/h | 1.148 GJ/h | **72.6%** |
| Cold utility | 3.986 GJ/h | 0.939 GJ/h | **76.4%** |

- **Process pinch** identified at ~100°C (coincides with distillation reboiler temperature)
- **HX1** (reactor effluent → feed preheat, 35→250°C) captures the largest internal recovery
- Fired heat/HP steam required above 200°C (above-pinch zone)
- **Annual utility cost savings: ~$135,000/yr** (fired heater fuel $134,052 + cooling water $1,219)

---

## Techno-Economic Analysis

Based on a 20-year discounted cash flow model. Plant capacity: **24,000 t/yr** sweet naphtha at 91% on-stream factor (8,000 hr/yr).

### Revenue Model

| Parameter | Value |
|---|---|
| Sour naphtha purchase price | $525/t |
| Sweet naphtha selling price | $635/t |
| Price spread (margin driver) | **$110/t** |
| Annual gross revenue | $12.74 M/yr |

### CAPEX Summary

| Item | Value |
|---|---|
| Purchased equipment cost | ~$392,000 |
| Total installed cost — ISBL (Lang factor 4.0) | $1,568,000 |
| Engineering + contingency (15% each) | included |
| OSBL + owner's costs + license | 40% of FCI |
| **Total Capital Investment (TCI)** | **$5,948,430** |
| Working capital | $65,000 |

### OPEX Summary

| Item | Value |
|---|---|
| Sour naphtha feedstock | ~$12.6 M/yr |
| Utilities (electricity, cooling water, steam) | $147,924/yr |
| Maintenance (3% TCI) + labour + insurance | $178,040/yr |
| **Total annual OPEX** | **$434,000/yr** (ex-feedstock net) |

### Profitability KPIs

| Metric | Value | Target | Status |
|---|---|---|---|
| Annual EBITDA | $502,000/yr | — | — |
| Annual net profit (after 30% tax) | $241,640/yr | — | — |
| **Simple payback period** | **4.6 years** | <5 yr | ✅ PASS |
| **ROI on CAPEX** | **15.4%** | >12% | ✅ PASS |
| **IRR (20-yr horizon)** | **~23%** | >15% | ✅ PASS |
| **NPV (10% discount, 20 yr)** | **~$2.1 M** | >0 | ✅ PASS |
| Discounted payback | ~5.2 years | — | — |
| 20-yr undiscounted net profit | $6.4 M | — | — |

### Sensitivity (OAT on TEA)

Most to least impactful on profitability:
1. **Sweet naphtha selling price (±20%)** — primary market risk; -20% extends payback beyond 7 years
2. **Feedstock price spread** — $105/t compression eliminates most EBITDA; long-term supply contracts recommended
3. **TCI overrun (±30%)** — project remains viable even at 30% CAPEX overrun given 23% base-case IRR

---

## Repository Structure

```
naphtha-hds-tea/
├── HDS_Final_Report.docx          # Full process simulation & TEA report
├── petro_final.pptx               # Presentation slides
├── stream_table.xlsx              # Complete Aspen Plus stream table (24 streams)
├── TEA_Naphtha_HDS_economic_analysis.xlsx  # 20-yr DCF model (5 sheets)
├── tower_details.jpeg             # APEA equipment sizing output
└── README.md
```

---

## Key Results Summary

| Module | Key Result |
|---|---|
| Reactor | 100% conversion of all reactive S-species; product <10 ppm S |
| Absorber optimum | ~100 kmol/hr lean MDEA at 35–40°C |
| Flash pressure | 4 bar optimal |
| Heat integration | 72.6% hot utility reduction; pinch at ~100°C |
| Simple payback | **4.6 years** |
| IRR | **~23%** |
| 20-yr NPV | **~$2.1 M** |

---

## Tools & Methods

- **Aspen Plus v14** — steady-state process simulation
- **Property method:** Grayson-Streed (accurate for H₂-rich hydrocarbon systems at high pressure)
- **Reactor model:** RPlug with Power-Law kinetics (4 HDS reactions)
- **Aspen Energy Analyzer** — pinch analysis & composite curves
- **Aspen Process Economic Analyzer (APEA)** — equipment sizing & costing
- **Excel (DCF model)** — 20-year TEA with CAPEX, OPEX, and sensitivity sheets

---

## Authors

- Aarav Gupta
- Mohak Dadhich
