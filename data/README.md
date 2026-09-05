# data/

The datasets are **not committed** (see `.gitignore`). Download them here.

## 1. `vgsales.csv` — required

The core dataset: 16,598 video games with regional sales figures (North
America, Europe, Japan, Other), originally scraped from VGChartz.

- Source: https://www.kaggle.com/datasets/gregorut/videogamesales
- Save the file as `data/vgsales.csv`.

Columns: `Rank`, `Name`, `Platform`, `Year`, `Genre`, `Publisher`,
`NA_Sales`, `EU_Sales`, `JP_Sales`, `Other_Sales`, `Global_Sales`
(all sales in millions of units; `Global_Sales` is the sum of the four
regions, not an independent measurement).

## 2. `vgsales_for_tableau.csv` — generated

Section 12 of the notebook writes a long-format version (one row per
title per region, zero-sales rows dropped) used for some of the Tableau
views. It's produced by running the notebook; it is not committed.

## 3. Metacritic scores — optional, fetched at runtime

Section 9 of the notebook pulls critic/user scores directly from a public
URL (`Bakikhan/Video-Game-Sales-Dataset`), so there's nothing to download
for that step.
