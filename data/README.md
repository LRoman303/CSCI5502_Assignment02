# Data
Both of these data sets are public, one being the ElectricVehiclePopulation data from an open-government dataset. And the other dataset is structured from the public soccer dataset website Transfermarkt. These files are read into the profiler before cleaning to conduct the analysis.

## Dataset A: Electric Vehicle Population Data
- **Organization:** Washington State Department of Licensing, published on Data.gov
- **Title:** Electric Vehicle Population Data
- **Source link:** https://catalog.data.gov/dataset/electric-vehicle-population-data (CSV resource)
- **Date accessed:** 2026-09-25
- **File name used:** `ElectricVehiclePopulation.csv`
- **Size:** 299,705 rows, 16 columns
- **Dataset Description:** Shows the Battery Electric Vehicles (BEVs) and Plug-in Hybrid Electric Vehicles (PHEVs) that are currently registered through Washington State Department of Licensing (DOL).

## Dataset B: Transfermarkt games
- **Organization:** Transfermarkt data, compiled by David Cereijo (dcaribou)
- **Title:** transfermarkt-datasets, `games.csv`
- **Source link:** https://github.com/dcaribou/transfermarkt-datasets
- **Direct CSV**: https://pub-e682421888d945d684bcae8890b0ec20.r2.dev/data/transfermarkt-datasets.zip (Using `games.csv`)
- **Date accessed:** 2026-09-25
- **File name used:** `games.csv`
- **Size:** 88,958 rows, 23 columns
- **Dataset Description:** Clean, structured football (soccer) dataset built from Transfermarkt data -- 88,000+ games, 50,000+ players, 1,890,000+ appearances and more, across 12 joinable tables.

## Why these two datasets
These datasets have two very distinct domains electric cars & soccer, although these both have a lot of categorical data, the soccer data has a lot more missing values and numerical data to make them distinct enough from each other.


## Getting the CSV files
The CSV files are not included in this repository since both files are too large to upload to github
- `ElectricVehiclePopulation.csv` = 82 MB
- `games.csv` = 29 MB
The main suggestion is to download and insert these datasets into the data folder. 
