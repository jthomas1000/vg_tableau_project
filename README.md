# Video Game Sales — Analysis & Tableau Dashboard

Exploratory analysis and an interactive dashboard built on the
[Video Game Sales](https://www.kaggle.com/datasets/gregorut/videogamesales)
dataset: 16,598 titles (1980–2020) with regional sales figures, originally
scraped from VGChartz.

Two deliverables:

| | What | Tool |
|---|---|---|
| [`notebooks/video_game_sales_analysis_kaggle.ipynb`](notebooks/video_game_sales_analysis_kaggle.ipynb) | Data cleaning, EDA, and a few modeling experiments | Python (pandas / seaborn / scikit-learn / statsmodels) |
| [`tableau/Video Game Sales Dashboard.twb`](tableau/Video%20Game%20Sales%20Dashboard.twb) | KPI tiles + genre / platform / publisher / regional views | Tableau 2026.2 |

## Questions this project looks at

- Which genres and platforms have sold the most, and has that shifted over time?
- Are some publishers consistent "hit-makers", or is it mostly about releasing more games?
- Does regional demand differ by genre? (Japan vs. RPGs, NA vs. Shooters.)
- Can a game's platform, genre, publisher, and release year predict how well it sells?
- How have Nintendo, Sony, and Microsoft traded off across console generations?

## What the notebook does

1. **Loading & cleaning** — missing-data audit; `Year` kept as a nullable
   integer; a value check showing `Global_Sales` is a derived total of the
   four regional columns (so those can't be model features without leaking).
2. **Missing-year enrichment** — looks up the 271 titles with no `Year` via
   the RAWG API (optional; skipped cleanly with no API key, those rows are
   then dropped from year-based analysis).
3. **Genre & platform trends**, **publisher analysis**, **regional patterns**,
   **platform lifecycles & console manufacturers**.
4. **"Can we predict a hit?"** — a Random Forest on pre-release features only.
   Removing the leaky regional columns drops R² from ~0.82 to ~0.05: platform,
   genre, publisher, and year alone say little about commercial success.
5. **Time-series forecast** — exponential smoothing on 1996–2015 annual totals.
6. **Publisher clustering** — k-means recovers the hit-maker / volume-dealer split.
7. **Adding critic scores** — joins Metacritic scores from a companion dataset;
   R² roughly triples (~0.06 → ~0.18), with `Critic_Score` the dominant feature.
8. **Discussion & limitations** — including the post-2015 data-sparsity caveat.
9. **Tableau export** — reshapes the cleaned data to long format
   (`vgsales_for_tableau.csv`, one row per title/region).

## Setup

### Notebook

```bash
python -m venv .venv
# Windows:  .venv\Scripts\activate
# macOS/Linux:  source .venv/bin/activate
pip install -r requirements.txt
```

Download `vgsales.csv` into `data/` — see [`data/README.md`](data/README.md) —
then adjust the load path in section 1 if you're not running on Kaggle
(the notebook reads `/kaggle/input/videogamesales/vgsales.csv`).

```bash
jupyter notebook notebooks/video_game_sales_analysis_kaggle.ipynb
```

### Tableau

See [`tableau/CONNECTING.md`](tableau/CONNECTING.md). Short version: get
`vgsales.csv` into `data/`, open the `.twb`, and repoint the data source
when Tableau asks.

## Data provenance

VGChartz figures are estimates, not audited sales. The dataset thins out
sharply after 2015 (a collection cutoff, not a market crash), so
year-based analysis is most reliable for **1996–2015**. Section 11 of the
notebook lists the full set of caveats.

## Layout

```
data/          vgsales.csv goes here (git-ignored); see data/README.md
notebooks/     the analysis notebook
tableau/       the .twb workbook + CONNECTING.md
requirements.txt
```
