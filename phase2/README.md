# Phase 2: Chess openings

Troy Goetz and Nicholas Grabowski

## Research question

Do some chess openings perform better at different player ratings, even after accounting for the rating gap between opponents?

## Files

- [Executed Phase 2 notebook](Phase2_Chess.ipynb): cleaning, sample selection, descriptive EDA, and two proposed analyses.
- [Analysis-ready CSV](data/chess_analysis_600.csv): exactly 600 unique games, with 150 per White-rating group; approximately 1.75 MB.
- [Raw collection CSV](data/raw/chess_games_raw.csv.gz): all 64,738 downloaded rows, losslessly gzip-compressed. This is a source archive, not the smaller analysis-ready CSV.
- [Source records](data/raw): player-list snapshot, selected accounts, archive response log, and hash manifest.
- [Collection notebook](Chess_Data_Collection.ipynb): the saved collection procedure, kept separate from the submitted notebook.

## Reproduce

Open Phase2_Chess.ipynb in Google Colab and select Runtime > Run all. The first cell reads our compressed raw CSV directly from GitHub; pandas decompresses it automatically. No API call is needed to reproduce the cleaning or final sample. pandas and matplotlib are the analysis dependencies. Intermediate outputs are saved under /content/ in Colab.

The code keeps rated standard blitz games, removes invalid game IDs and ratings and duplicate games, extracts completed results, groups opening labels, and selects 150 games per White-rating group with seed 2950. The final sample contains 46 identified opening families and two unknown source labels. Opening labels do not change game selection. Unknown labels are excluded from named-family comparisons.

The saved EDA outputs were generated from the archived raw CSV; the original and decompressed archived bytes were checked for equality using the hash in manifest.json. The two preregistered regression models have not been fitted or tested. Later changes to their plans should be identified explicitly.

## Source and limitations

[Chess.com Published-Data API documentation](https://www.chess.com/news/view/published-data-api)

Players were randomly sampled from a public US-listed recently active account snapshot, not from all platform games. Exact time controls vary within blitz, players repeat, and opening families are label-based. Equal rating-group samples do not estimate population-level frequencies. Outputs should be interpreted as aggregate associations, not causal opening recommendations or judgments of individual players.
