# Opening the Tableau workbook

`Video Game Sales Dashboard.twb` was built in **Tableau 2026.2**. A `.twb`
stores only the view definitions and a *reference* to the data, not the
data itself, so you need `vgsales.csv` locally before it will render.

## Steps

1. Download `vgsales.csv` into the repo's `data/` folder — see
   [`../data/README.md`](../data/README.md).
2. Open `Video Game Sales Dashboard.twb` in Tableau Desktop or Tableau
   Public (2026.2 or newer).
3. Tableau will prompt **"Where is the data file?"** because the workbook
   was authored against `C:\Users\<user>\Downloads\vgsales.csv`. Point it
   at your `data/vgsales.csv`. Tableau rebuilds its `.hyper` extract from
   the CSV automatically.

## Making it portable (recommended for the repo)

Once the data source is repointed, use **File ▸ Export Packaged Workbook**
to save a `.twbx`. That bundles the extract into the file so it opens
anywhere with no "find the data file" prompt. `.twbx` is a good thing to
attach to a portfolio; it is git-ignored here by default (binary, ~1 MB),
so add it explicitly if you want it tracked:

```bash
git add -f "tableau/Video Game Sales Dashboard.twbx"
```

## Worksheets in the workbook

KPI tiles: **KPI Total Sales**, **KPI Total Games**, **KPI Top Genre**,
**KPI Top Platform**.

Detail views: **Genre Sales**, **Platform Sales**, **Publisher Bubble**,
**Regional Trend**, **Manufacturer Trend** (PlayStation / Xbox / Nintendo),
**Industry Lifecycle**.

## Data provenance

The sales figures are VGChartz estimates, not audited numbers, and the
dataset thins out sharply after 2015 (a collection cutoff, not a real
market decline). Year-based views are most reliable for the 1996–2015
window. See section 11 of the notebook for the full list of caveats.
