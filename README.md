# 🛢️ U.S. Oil & Gas Production Shocks and Retail Energy Prices

OLS panel regression analysis examining whether production shocks in U.S. oil and gas significantly affect retail gasoline, diesel, and natural gas prices — and how refinery infrastructure moderates this relationship.

---

## 🔎 Research Question

Do unexpected changes in U.S. oil and gas production pass through to retail energy prices? Does refinery infrastructure — capacity and utilization — amplify or dampen that effect?

---

## 📁 Project Overview

Monthly state-level U.S. energy market data from 2015 to 2025, covering COVID-19 supply chain shocks, geopolitical disruptions, and rapid domestic production growth. OLS regression with HC1 robust standard errors estimated separately for gasoline, diesel, and natural gas.

---

## 📊 Dataset

| Source | Description | Period |
|--------|-------------|--------|
| EIA — OGORB | State-level oil & gas production volumes | 2015–2025 |
| EIA — Retail Gasoline & Diesel Prices | U.S. regular gasoline and No. 2 diesel ($/gallon) | 2015–2025 |
| EIA — Natural Gas Prices | Residential consumer natural gas price ($/mcf) | 2015–2025 |
| EIA — Refinery Utilization & Capacity | Operable distillation capacity and utilization rate | 2015–2025 |

Panel size: 6,000+ state-month observations

---

## 🧑🏻‍💻 Methodology

### Production Shock Construction

Prod_Shock(t) = Production(t) − Rolling_12_Month_Average(t)

Isolates unexpected supply deviations from seasonal trends and long-run growth. Positive shock = oversupply. Negative shock = undersupply.

### Baseline OLS Model

Price(t) = β0 + β1·Shock + β2·Utilization + β3·Capacity + ε

Estimated separately for gasoline, diesel, and natural gas with HC1 robust standard errors.

### Interaction Model

Price(t) = β0 + β1·Shock + β2·Utilization + β3·Capacity + β4·(Shock × Capacity) + ε

Gasoline & Diesel use Shock × Refinery Capacity. Natural Gas uses Shock × Refinery Utilization.

---

## 🟩 Key Results

| Model | R² |
|-------|----|
| Gasoline baseline | 0.47 |
| Diesel baseline | 0.40 |

| Variable Pair | ρ |
|--------------|---|
| Production Shock ↔ Gasoline Price | ~0.00 |
| Gasoline Price ↔ Diesel Price | ~0.95 |
| Refinery Capacity ↔ Gasoline Price | ~-0.50 |

**Main finding:** Refinery capacity is the dominant driver of retail fuel prices — not production variability. Infrastructure constraints determine consumer prices more than production swings.

---

## Visualisations Generated

1. Monthly production by state (first 5 states)
2. National production vs retail gasoline price — dual axis
3. Production shock over time — positive and negative shocks highlighted
4. Shock vs each of the 3 fuel prices — scatter plots
5. Correlation matrix heatmap
6. All 3 retail energy prices over time

---

## 🖥️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Primary analysis language |
| pandas | Data loading, cleaning, merging |
| numpy | Rolling averages, shock construction |
| statsmodels | OLS regression with HC1 robust standard errors |
| matplotlib | Time series and scatter visualisations |
| seaborn | Correlation heatmap |

---

## 🏃🏻‍♀️ How to Run

Install dependencies:

pip install pandas numpy statsmodels matplotlib seaborn xlrd openpyxl

Place all 4 data files in the same folder as the script and run:

python oil_gas_analysis.py

---

## 🏫 Academic Context

Final project for BUAN 6312 — Applied Econometrics and Time Series Analysis at The University of Texas at Dallas — MS Business Analytics & AI program.

Group 3: Aishwarya Balmoori, Chokkapu Saatvika, Matta Himakanthi, Karanam Kiran Simha, Mulakala Taejasvi, Bedi Amrinder Singh, Masomera Gladys, Ganaparthi Sravani, Naha Sucharita

---

## 👩🏻 Author

Saatvika Chokkapu
MS Business Analytics & AI — UT Dallas (May 2026)
LinkedIn: https://www.linkedin.com/in/saatvika-chokkapu/
GitHub: https://github.com/saatvikach613-hue
