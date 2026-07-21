# Wild Card Weighting

**Authors:** Jack Cook, Jackson Pond

Data science project investigating why wild card teams occasionally outperform division winners in the MLB postseason. Using a dataset of MLB games from 2014–2025, we train Random Forest and XGBoost models to identify the strongest features behind postseason success, and evaluate whether wild card teams have structural advantages not captured by regular season standings.

Full write-up: [`Paper/Draft.pdf`](Paper/Draft.pdf) (source in [`Paper/Draft.tex`](Paper/Draft.tex)).

Code source: [`final_report.ipynb`](notebooks/final_report.ipynb)

## Repo layout

```
data/
  raw/          scraped or downloaded source data, never hand-edited
  processed/    derived datasets built by the notebooks below (GAMES.csv, expected_stats.csv, ...)
scraping/
  scraper.py    scrapes pitcher game logs from Baseball Reference
notebooks/
  01_build_oaa_woba.ipynb   merges Statcast OAA + expected-stats + wildcard data -> data/processed/expected_stats.csv
  02_build_game_df.ipynb    combines pitcher logs + merged stats into data/processed/GAMES.csv
  03_eda.ipynb              exploratory analysis of team performance and matchups
  04_data_viz.ipynb         feature correlation and distribution plots
  final_report.ipynb        the full pipeline (acquisition -> cleaning -> EDA -> modeling) as turned in
docs/
  pitcher_log_glossary.md   column definitions for the scraped pitcher game logs
Paper/
  Draft.tex, refs.bib, figures/    LaTeX source for the paper
archive/
  MLB_algo.ipynb            earlier modeling draft, superseded by notebooks/final_report.ipynb
```

## Pipeline order

1. `scraping/scraper.py` — scrape pitcher game logs into `data/raw/`, following terms of use on the baseball reference site.
2. `notebooks/01_build_oaa_woba.ipynb` — combine OAA/expected-stats/wildcard data.
3. `notebooks/02_build_game_df.ipynb` — build the game-level dataset (`data/processed/GAMES.csv`).
4. `notebooks/03_eda.ipynb`, `notebooks/04_data_viz.ipynb` — explore the data.
5. `notebooks/final_report.ipynb` — clean, model (Random Forest, XGBoost), and analyze feature importance.

## Data sources

- Outs Above Average and expected stats: [Baseball Savant](https://baseballsavant.mlb.com)
- Pitcher game logs: scraped from [Baseball Reference](https://www.baseball-reference.com) via `scraping/scraper.py`
