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

Open Phase2_Chess.ipynb in Google Colab and select Runtime > Run all. The first cell reads our compressed raw CSV directly from GitHub; pandas decompresses it automatically. No API call is needed to reproduce the cleaning or final sample. The notebook uses pandas, DuckDB SQL, Seaborn 0.13.2, and Matplotlib. Its setup cell installs DuckDB and Seaborn in Colab. Intermediate outputs are saved under /content/ in Colab.

The code keeps rated standard blitz games, removes invalid game IDs and ratings and duplicate games, extracts completed results, groups opening labels, and selects 150 games per White-rating group with seed 2950. The final sample contains 46 identified opening families and two unknown source labels. Opening labels do not change game selection. Unknown labels are excluded from named-family comparisons.

The saved EDA outputs were generated from the archived raw CSV; the original and decompressed archived bytes were checked for equality using the hash in manifest.json. Neither proposed regression has been fitted or tested. Statement 2 was narrowed in a dated October 18 amendment, selected using counts before model fitting.

## Source and limitations

[Chess.com Published-Data API documentation](https://www.chess.com/news/view/published-data-api)

Players were randomly sampled from a public US-listed recently active account snapshot, not from all platform games. Exact time controls vary within blitz, players repeat, and opening families are label-based. Equal rating-group samples do not estimate population-level frequencies. Outputs should be interpreted as aggregate associations, not causal opening recommendations or judgments of individual players.


## October 18 presentation and course-method revision

- [PDF submission](Phase2_Chess.pdf) contains both parts, code, tables, and saved figures.
- DuckDB SQL now performs filtering, rating-group creation, the opening-lookup join, and descriptive aggregation. pandas retains file handling, duplicate-ID checking, and the original random sampling. Seaborn draws the figures; Matplotlib handles labels and layout.
- [Opening lookup](data/opening_lookup.csv) records the previously documented family assignment for each of 4,808 observed URLs. It is a classification of the source, not another independent dataset.
- [All opening counts](data/all_opening_counts.csv) and [all opening scores](data/all_opening_scores.csv) preserve categories outside the eight-family main display. The main display chooses the top eight by count, breaking ties alphabetically.
- The 600 game IDs and every column value were checked against the peer-review sample. The 600-game sample and Statement 1 are preserved. An October 18 amendment narrows Statement 2 to a 63-game, four-cell opening/rating comparison selected by counts, and states the game-independence assumption with repeated-player dependence retained as a limitation. No preregistered regression has been fitted or tested.
- The prior peer-review version remains available at [commit d3f9d28](https://github.com/Toyman123/info2950-project/blob/d3f9d28/phase2/Phase2_Chess.ipynb).
- The data description defines all 21 CSV fields and explains rating, opening family, PGN, time controls, and White score.
- Sampling remains a limitation: only three source archives supplied the selected games in each of the two highest rating groups, and one source account supplied 23% of all 600 games. Source-account counts are not counts of every opponent represented.


### October 18 inference clarification

The planned models will treat each game as an independent observation and use conventional regression uncertainty estimates. This assumption was clarified before model fitting or testing; it does not establish that repeated-player games are independent. The notebook keeps that limitation explicit. The mean rating gap in the text is now 12.35, matching DuckDB's displayed rounding. The notebook is the current version; the earlier PDF export predates this text-only clarification.


### October 18 coverage amendment

Statement 2 now compares King's Pawn Opening with Queen's Pawn Opening across White-rating groups Under 1000 and 1000–1499. The four cells contain 11, 15, 25, and 12 games (63 total). The planned regression includes opening, rating group, their interaction, and rating difference. This count-based amendment was recorded before any formal model or significance test. It does not change the 600-game dataset or the descriptive outputs, and does not promise high power or establish independence. The original October 15 plan remains in commit history.
