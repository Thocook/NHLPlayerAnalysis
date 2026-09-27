# NHL Goalie Analysis

A compact local React app for MoneyPuck NHL goalie season metrics and within-season game-to-game volatility.

## Run

```sh
npm install
npm run update-data
npm run dev
```

`npm run update-data` downloads only published CSV links from [MoneyPuck's data page](https://moneypuck.com/data.htm), validates their headers and reconciles season totals against game data. Raw CSVs are streamed and never committed or written to the project; the compact result is `public/data/goalie-seasons.json`.

## Metrics and validation

- **Season GAA / SV%**: provider season-level `goalsAgainstAverage` and `savePercentage` fields (the script fails if unavailable).
- **Volatility**: sample standard deviation (`n - 1`) of game-level `goalsAgainstAverage` and `savePercentage` for the same goalie, team, season, and game type.
- **Games played**: number of distinct eligible game-level rows. The updater requires that it reconciles to the season-level `gamesPlayed` field; it fails on mismatches instead of guessing.
- Rows are kept separately for `regular` and `playoffs`; the app opens on regular season. Rows with no GAA or SV% are excluded before standard deviations.

The update script prints source URLs, discovered headers, selected columns, coverage, and any validation failures. This project is not an endorsement or quality ranking: volatility describes game-to-game variation, not goalie quality.

Data: MoneyPuck.com, used under its published data terms. Please credit MoneyPuck.com when displaying outputs based on these data.
