# Data

Place the two CSV files in this folder. The notebook reads them from `../data/`.

## Dataset A: Electric Vehicle Population Data
- **Organization:** Washington State Department of Licensing, published on Data.gov
- **Title:** Electric Vehicle Population Data
- **Source link:** https://catalog.data.gov/dataset/electric-vehicle-population-data (CSV resource)
- **Date accessed:** [DATE]
- **File name used:** `ElectricVehiclePopulation.csv`
- **Size:** 299,705 rows, 16 columns
- **Structure:** mostly categorical (10 categorical columns, 2 numeric measures, 4 identifier-like columns), almost no missing values (the highest is 0.26%), and no date columns.

## Dataset B: Transfermarkt games
- **Organization:** Transfermarkt data, compiled by David Cereijo (dcaribou)
- **Title:** transfermarkt-datasets, `games.csv`
- **Source link:** https://github.com/dcaribou/transfermarkt-datasets
- **Citation:** Cereijo, D. (2026). dcaribou/transfermarkt-datasets: extract, prepare and publish transfermarkt datasets. GitHub.
- **Date accessed:** [DATE]
- **File name used:** `games.csv`
- **Size:** 88,958 rows, 23 columns
- **Structure:** more numeric measures (6), real missing values (up to 28.53%), and a date column.

## Why these two datasets
The datasets have noticeably different structures, as the assignment requires:

| | Dataset A (EV) | Dataset B (games) |
|---|---|---|
| Mostly | Categorical columns | More numeric columns |
| Missing values | Almost none | Up to 28.53% |
| Dates | None | A `date` column |

Both datasets are public. They contain no private personal data. The games data includes names of professional managers and referees, which are publicly reported.
