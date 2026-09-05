# Opening the Tableau workbook

`Video Game Sales Dashboard.twb` was built in **Tableau 2026.2**. A `.twb`
stores only the view definitions and a *reference* to the data, not the
data itself, so you need `vgsales.csv` locally before it will render.

## Steps

1. Download `vgsales.csv` into the repo's `data/` folder — see
   [`../data/README.md`](../data/README.md).
2. Open `Video Game Sales Dashboard.twb` in Tableau Desktop or Tableau
   Public (2026.2 or newer).

The workbook's file connection is set to the **relative** path `../data/`
(i.e. `data/vgsales.csv` from the repo root), so as long as step 1 is done
it resolves with no "Where is the data file?" prompt.

On first open Tableau may report the cached extract is missing (it was a
`TableauTemp` file that no longer exists) and offer to **regenerate the
extract from the original data** — accept that and it rebuilds from
`../data/vgsales.csv`. If you'd rather not deal with the extract at all,
right-click the **vgsales** data source ▸ **Extract ▸ Remove ▸ Remove the
extract** to fall back to the live CSV connection.

## Making it portable (recommended for the repo)

Use **File ▸ Export Packaged Workbook** to save a `.twbx`. That bundles the
data into the file so it opens anywhere with nothing to download and no
path to resolve — the best format to attach to a portfolio. (This step
needs Tableau Desktop; it can't be scripted.) `.twbx` is git-ignored here
by default (binary, ~1 MB), so add it explicitly if you want it tracked:

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
