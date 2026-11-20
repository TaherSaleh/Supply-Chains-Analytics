# 2026 European Supply Chain Network Optimization (CFLP)

An Operations Research and Supply Chain Analytics project using **Mixed-Integer Linear Programming (MILP)** in Python (`PuLP`, `pandas`, `matplotlib`) to optimize manufacturing plant locations and monthly distribution flows across **Germany, France, Spain, Czechia, and Poland**.

## Business Problem
European manufacturers face a classic strategic trade-off between **nearshoring to Central/Eastern Europe** (lower wages and industrial rents in Czechia and Poland) versus **producing closer to Western demand hubs** (Germany and France) to minimize road freight, highway tolls, and grid carbon intensity.

This model determines:
1. **Facility Footprint:** Which `Low` (500k units/mo) or `High` (1,500k–2,000k units/mo) capacity plants to open.
2. **Allocation Flows:** How many units to ship across each origin–destination lane to satisfy **4.5M units/month** of total demand at minimum cost.

## 2026 Empirical Dataset
All cost, capacity, freight, and emissions inputs are anchored to 2026 European benchmarks (see [`Data/sources.md`](./Data/sources.md)):
* **Labor & Energy:** Eurostat Labour Cost Index (Q2 2026) & Non-Household Electricity Prices (`nrg_pc_205`, 2026 S1).
* **Road Freight:** IRU / Upply / Ti European Road Freight Benchmark 2026 (including German CO2 *LKW-Maut* and Poland *e-TOLL*).
* **Real Estate & CAPEX:** CBRE / BNP Paribas Real Estate European Logistics Prime Rents (Q1–Q3 2026).
* **Carbon Intensity:** European Environment Agency (EEA) 2026 National Grid Carbon Intensity (`gCO2e/kWh`).

## Multi-Scenario Results

| Scenario | Total Monthly Cost (€) | vs. Baseline | CO2 Emissions (Tons/Mo) | Optimal Plant Footprint |
| :--- | :---: | :---: | :---: | :--- |
| **1. Baseline (2026)** | €58,587,900 | — | 8,808 t | Spain (Low), Czechia (Low + High), Poland (High) |
| **2. Poland Mega-Hub (2x Cap)** | €57,848,400 | **-1.3%** | 10,384 t | Spain (Low), Poland (High - 4M Cap) |
| **3. Freight Surge (3x FTL)** | €69,203,700 | **+18.1%** | 8,808 t | Spain (Low), Czechia (Low + High), Poland (High) |
| **4. Green CO2 Cap (<=5,500t)** | €65,842,900 | **+12.4%** | **5,182 t** | France (Low), Spain (Low + High), Czechia (High) |

![Scenario Comparison 1](./Scenario%20Comparison_1.png)

![Scenario Comparison](./Scenario%20Comparison.png)

## Key Strategic Takeaways
* **Nearshoring Dominance:** Under 2026 cost structures, serving Germany from Czechia (€9.49/unit landed cost vs. €13.99/unit locally) and France from Poland (€11.11/unit vs. €13.57/unit) saves millions in fixed and variable costs.
* **Cost vs. Carbon Trade-Off:** Expanding Poland's capacity cuts total cost by **€739.5k/month** but raises emissions by **+17.9%** due to grid carbon intensity (`560 gCO2e/kWh`). Enforcing a **5,500-ton CO2 cap** shifts production into nuclear/renewable-heavy France (`48 gCO2e/kWh`) and Spain (`135 gCO2e/kWh`), cutting emissions by **41.2%** at a **+12.4%** cost premium.

## Repository Structure
```text
Capacitated-Facility-Location-Problem/
├── Data/
│   ├── EU_Supply_Chain_2026_Dataset_2.xlsx
│   └── sources.md
├── notebooks/
│   └── EU_Supply_Chain_Optimization_2026.ipynb
├── Scenario Comparison_1.png
├── Scenario Comparison.png
└── README.md
