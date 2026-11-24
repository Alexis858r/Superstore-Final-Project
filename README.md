# Growing Sales, Leaking Profit — Superstore Data Story

Final Project · Data Base Knowledge Extraction · Enterprise Multi-Modal Data Visualization & Storytelling
Presentation: November 24, 2026

## Team

| Role | Member |
|---|---|
| Data Architect & Wrangler | Jesus Ivan Tamay Balam (2302146) |
| BI Dashboard Lead | Laura Patricia Chavez Chi (2302053) |
| Python Visualization Specialist | Adriel Arturo Solano Peraza (2302019) |
| Narrative & Data Storytelling Lead | Alexis Alfredo Bustos Rodríguez (2302117) |
| QA & Integration Lead | Jesús Gallegos Gaspar (2302041) |

## Deliverables

| # | Deliverable | File |
|---|---|---|
| 1 | Interactive BI dashboard (open-source, Option C) | [`dashboard/superstore_dashboard.html`](dashboard/superstore_dashboard.html) |
| 2 | Python notebook (fully commented, executed) | [`notebook/final_visualizations.ipynb`](notebook/final_visualizations.ipynb) |
| 3 | Executive presentation deck | [`presentation/Superstore_Data_Story.pptx`](presentation/Superstore_Data_Story.pptx) · [PDF](presentation/Superstore_Data_Story.pdf) |
| 4 | Live presentation | Speaker notes for all 5 members are in the deck |

## Dataset

**Sample – Superstore** (public Tableau sample data, via a GitHub mirror). It has 9,994 order lines from 2015 to 2018.

- **Continuous:** Sales, Profit, Discount, Quantity
- **Categorical:** Category, Sub-Category, Segment, Ship Mode, Region
- **Temporal:** Order Date, Ship Date
- **Geospatial:** State, City, Postal Code

The raw CSV contains three stacked sheets. The notebook splits them into a star schema:

```
            dim_people (Region → Regional Manager)
                    │ Region
fact orders (clean_superstore.csv)
                    │ Order ID
            dim_returns (Returned orders)
```

## Why an open-source dashboard (Option C)

The dashboard is a single HTML file built with **Plotly.js** (MIT licence). We chose it because:

- It is free, runs in any browser (Windows, Mac or Linux) and needs no licence or install.
- The data and libraries are embedded, so it works offline.
- It has every required feature:
  - **cross-filtering:** click a state, region or discount band to filter every chart
  - **drill-down:** Category → Sub-category, and Region → Regional Manager
  - **date slicing:** From/To months, a year filter and drag-to-zoom
  - diverging and sequential **colour-blind-safe palettes**
  - **0-baseline bars**

To use it, download `dashboard/superstore_dashboard.html` and open it in Chrome or Edge.

## How to run the notebook

```bash
pip install pandas numpy matplotlib seaborn plotly jupyter
cd notebook
jupyter notebook final_visualizations.ipynb
```

The notebook reads `../data/raw_superstore.csv`. It writes the cleaned tables to `../data/` and the charts to `../assets/` (PNG at 300 dpi, SVG and interactive HTML).

## Repository structure

```
data/          raw + cleaned dataset, star-schema dimension tables
notebook/      final_visualizations.ipynb
assets/        exported charts (.png / .svg / .html)
dashboard/     superstore_dashboard.html (interactive BI dashboard)
presentation/  Superstore_Data_Story.pptx + .pdf
```

## Key findings

- Sales grew **51%** (2015→2018), but the profit margin is only **12.5%**.
- Order lines with a discount **above 20%** (14% of lines) lose **$135K**. Above 40%, 100% of the lines lose money.
- The discount vs profit margin correlation is **r = −0.86**.
- Losses concentrate in **Tables, Bookcases and Supplies**, and in **Texas, Ohio, Pennsylvania and Illinois**.
- **Recommendation:** cap discounts at 20%. Upper-bound estimate: **+$219K** profit and a margin of about **20%**.
