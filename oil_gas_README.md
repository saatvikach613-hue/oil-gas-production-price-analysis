# U.S. Oil & Gas Production Shocks and Retail Energy Prices

**OLS panel regression analysis examining whether production shocks in U.S. oil and gas significantly affect retail gasoline, diesel, and natural gas prices — and how refinery infrastructure moderates this relationship.**

---

## Research Question

Do unexpected changes in U.S. oil and gas production ("production shocks") pass through to retail energy prices for consumers? And does refinery infrastructure — capacity and utilization — amplify or dampen that effect?

---

## Project Overview

This study analyses monthly, state-level U.S. energy market data from 2015 to 2025, covering major disruptions including rapid domestic production growth, COVID-19 supply chain shocks, and geopolitical disruptions. Using OLS regression with HC1 robust standard errors, we estimate separate models for three fuel types and test whether refinery variables mediate the production shock–price relationship.

---

## Dataset

| Source | Description | Period |
|--------|-------------|--------|
| EIA — OGORB | State-level oil & gas production volumes | 2015–2025 |
| EIA — Retail Gasoline & Diesel Prices | U.S. regular gasoline and No. 2 diesel ($/gallon) | 2015–2025 |
| EIA — Natural Gas Prices | Residential consumer natural gas price ($/mcf) | 2015–2025 |
| EIA — Refinery Utilization & Capacity | Operable distillation capacity and utilization rate | 2015–2025 |

**Panel size:** ~6,000+ state-month observations before merging to national macro panel

---

## Methodology

### Production Shock Construction

The production shock is defined as:

```
Prod_Shock(t) = Production(t) − Rolling_12_Month_Average(t)
```

This isolates unexpected supply deviations from seasonal trends and long-run growth, following standard macroeconomics literature on supply shocks.

- **Positive shock** = production exceeds recent expectations (oversupply)
- **Negative shock** = production falls below recent expectations (undersupply)

### Baseline OLS Model

```
Price(t) = β0 + β1·Shock(t) + β2·Utilization(t) + β3·Capacity(t) + ε(t)
```

Estimated separately for gasoline, diesel, and natural gas with **HC1 robust standard errors**.

### Interaction Model

```
Price(t) = β0 + β1·Shock + β2·Utilization + β3·Capacity + β4·(Shock × Capacity) + ε
```

- Gasoline & Diesel: interaction with **Refinery Capacity**
- Natural Gas: interaction with **Refinery Utilization**

---

## Key Results

### Model Fit (R²)

| Model | R² |
|-------|-----|
| Gasoline (baseline) | **0.47** |
| Gasoline (interaction) | **0.47** |
| Diesel (baseline) | **0.40** |
| Diesel (interaction) | **0.40** |
| Natural Gas (baseline) | varies |
| Natural Gas (interaction) | varies |

### Correlations

| Variable Pair | ρ |
|--------------|---|
| Production Shock ↔ Production Volume | ~0.93 (expected by construction) |
| Production Shock ↔ Gasoline Price | ~0.00 (near-zero) |
| Production Shock ↔ Diesel Price | ~0.00 (near-zero) |
| Gasoline Price ↔ Diesel Price | ~0.95 (highly integrated markets) |
| Refinery Capacity ↔ Gasoline Price | ~-0.50 (more capacity → lower prices) |
| Refinery Capacity ↔ Diesel Price | ~-0.47 |

### Main Finding

> **Refinery capacity is the dominant driver of retail fuel prices, not production variability.** Production shocks show near-zero direct correlation with retail prices, suggesting national market integration limits local shock pass-through. Infrastructure constraints — not production swings — determine consumer prices.

---

## Visualisations

The script generates 5 charts:
1. `state_production_trends.png` — Monthly production by state (first 5 states)
2. `production_vs_gasoline_price.png` — National production vs retail gasoline price (dual axis)
3. `production_shock_time.png` — Production shock over time (positive = green, negative = red)
4. `shock_vs_prices_scatter.png` — Scatter: shock vs each of the 3 fuel prices
5. `correlation_matrix.png` — Heatmap of all key variable correlations
6. `energy_prices_over_time.png` — All 3 retail energy prices on one chart

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Primary analysis language |
| pandas | Data loading, cleaning, merging |
| numpy | Rolling averages, shock construction |
| statsmodels | OLS regression with HC1 robust SEs |
| matplotlib | Time series and scatter visualisations |
| seaborn | Correlation heatmap |

---

## How to Run

1. Clone the repository
```bash
git clone https://github.com/saatvikach613-hue/Oil-Gas-Production-Price-Analysis
cd Oil-Gas-Production-Price-Analysis
```

2. Install dependencies
```bash
pip install pandas numpy statsmodels matplotlib seaborn xlrd openpyxl
```

3. Place all 4 data files in the same folder as the script:
   - `OGORBcsv_cleaned.csv`
   - `Gasoline_and_Diesel_Retail_Prices.xls`
   - `Natural_Gas_Prices.xls`
   - `Refinery_Utilization_and_Capacity.xls`

4. Run the script
```bash
python oil_gas_analysis.py
```

---

## File Structure

```
Oil-Gas-Production-Price-Analysis/
├── oil_gas_analysis.py                      # Main analysis script
├── OGORBcsv_cleaned.csv                     # Production data
├── Gasoline_and_Diesel_Retail_Prices.xls    # Price data
├── Natural_Gas_Prices.xls                   # Price data
├── Refinery_Utilization_and_Capacity.xls    # Infrastructure data
└── README.md                                # This file
```

---

## Academic Context

This project was completed as a final project for **BUAN 6312 — Applied Econometrics and Time Series Analysis** at **The University of Texas at Dallas (UTD)** — MS Business Analytics & AI program.

**Group 3 members:** Aishwarya Balmoori, Chokkapu Saatvika, Matta Himakanthi, Karanam Kiran Simha, Mulakala Taejasvi, Bedi Amrinder Singh, Masomera Gladys, Ganaparthi Sravani, Naha Sucharita

---

## Author

**Saatvika Chokkapu**
MS Business Analytics & AI — UT Dallas (May 2026)
[LinkedIn](https://www.linkedin.com/in/saatvika-chokkapu/) | [GitHub](https://github.com/saatvikach613-hue)
