# Automated CSV Profiler
CSCI 5502 · Assignment 02: From CSV to Evidence · Luis Echeverry (Individual Submission)

SYSTEM ARCHETECTURE: 
```
CSV file → Python profile and statistics → summary (JSON) → local LLM writes insights → Python checks the numbers → report
```
The LLM model only explains the results that Python computed from the CSV files. And all results from the LLM model is checked by python during the creation of the summary.

## 1. Purpose of the System
The system should produce a reproducible profiler for appropriate CSV files. The purpose of this profiler is to be able to understand what is inside a dataset, how trustworthy it is, and its limitations before any modeling is done. 

Given a CSV, the profile will:
1. Load every column as text, so my code decides each column's type instead of having pandas guess.
2. Infer each column's technical type ((integer, float, boolean, datetime, string, mixed or empty) and probable role (numeric measure, categorical attribute, Boolean field, date-like field, identifier-like field, free-text field, or unknown/mixed).
3. Check data quality: duplicate rows, columns with only one value, columns with 30% or more missing values, mixed types, identifier-like or high-cardinality columns, and potentially sensitive fields.
4. Calculate descriptive statistics: for numeric columns: the count, missing, min, max, mean, median, mode, standard deviation, Q1, Q3, IQR, and 1.5 * IQR outliers; for categorical columns: the number of categories, the most frequent value and the top 10 values with counts and percentages.
5. Find correlations between numeric columns(identifiers are excluded) and the strongest positive and negative pairs.
6. Pick plots based on the column typed (max 8), write under each plot why it was chosen, and list any plot type it skipped and why.
7. Send a summary of the results to a local LLM (Ollama), which then writes 5 to 8 insights, and flags any number in the answer that Python never calculated.
8. Save a report and all output files in a separate folder for each dataset.

An important part of my design is that Python does all the calculations first, and the LLM only explains results that Python already verified. Not only that, but the program never deletes or changes the data: duplicates, missing values and outliers are only flagged, and no column names from my datasets are written into the analysis code. 


## 2. Python Version Used
I used Python 3.13/9 on a MacBook Pro M3 with 18 GB of RAM.

## 3. Required Libraries
- pandas
- NumPy
- Matplotlib
- seaborn
- ollama (Python package)
- notebook (Jupyter)

The minimum versions are listed in `requirements.txt`. I tested everything with pandas 3.0.6, NumPy 2.5.3, Matplotlib 3.11.2, seaborn 0.13.2, ollama 0.6.2 and notebook 7.6.3. The Ollama app (https://ollama.com) is also needed for the AI insights.


## 4. Installation Steps

1. Download the repository and open a Terminal in its folder:
```bash
   git clone https://github.com/LRoman303/CSCI5502_Assignment02.git
   cd CSCI5502_Assignment02
```
2. Create and turn on a virtual environment (if you have Anaconda, run `conda deactivate` first):
```bash
   python3 -m venv .venv
   source .venv/bin/activate
```
3. Install the libraries:
```bash
   pip install -r requirements.txt
```
4. Install the Ollama app from https://ollama.com/download, open it, and download the model:
```bash
   ollama pull qwen2.5:7b
```
5. Download the two CSV files (links in section 10) and put them in the `data` folder. They are not included in the repository since both files are too large for GitHub.


## 5. Exact steps to run the program

1. With the virtual environment on, start Jupyter:
```bash
   python -m notebook
```
2. Open `src/profiler.ipynb`.
3. Update the two file paths in the configuration cell (see section 6).
4. Make sure the Ollama app is open.
5. Click **Kernel > Restart Kernel and Run All Cells**.
6. The results are saved in `output/dataset_a/` and `output/dataset_b/`.

The entry point is `generate_profile(csv_path, output_dir, use_llm=True)`.


## 6. How to select a CSV file

Only the configuration cell at the bottom of the notebook needs to change:
```python
# Configuration: change only these lines to profile a different CSV
DATASET_A = "/Users/luis/Documents/automated_csv_profiler/data/ElectricVehiclePopulation.csv"
DATASET_B = "/Users/luis/Documents/automated_csv_profiler/data/games.csv"
USE_LLM = True
```
Since these are the full paths on my Mac, change `DATASET_A` and `DATASET_B` to where the CSV files are on your computer. To profile a different CSV, change one of these paths to that file. None of the analysis code needs to change.


## 7. How to enable or disable the LLM component

- `USE_LLM = True` in the configuration cell turns on the AI insights.
- `USE_LLM = False` turns them off.

If Ollama is not running, the program still creates the full report and states that the AI insights were skipped because the model was unavailable.

## 8. Which model was used

I used `qwen2.5:7b`, running locally through Ollama, so no API key is needed. In Mini-Project 02, the smaller `qwen2.5:0.5b` invented values that weren't in the data, so I chose a larger model, and my Mac has 18 GB of RAM to run it.



## 9. Known Limitations

- **Column roles are guesses.** The program doesn't know what a column means or its units, so it guesses roles from the values and column names.
- **Placeholder values can distort the statistics.** In the EV data, 65.48% of `Electric Range` values are 0 because the range was never researched, which makes the median 0.
- **The 1.5 × IQR rule can over-flag outliers.** In the games data, every home team scoring 4 or more goals is flagged, even though those scores are normal.
- **Correlation is not causation.** The EV correlation between `Model Year` and `Electric Range` (r = -0.55) is mostly caused by those placeholder zeros.
- **The sensitive-field check is only a heuristic.** No warning does not mean the data is safe.
- **The number check can't catch every AI mistake.** It only checks that each number exists in the Python results. It caught two invented numbers (79,950 and 300,000), but it missed "Legislative District has 26.0% missing," where the real value is 0.26%. Because of this, every AI insight still needs to be read by a person.


## 10. Sources for Both Datasets

| | Dataset A | Dataset B |
|---|---|---|
| Organization | Washington State Department of Licensing (published on Data.gov) | Transfermarkt data, compiled by David Cereijo (dcaribou) |
| Title | Electric Vehicle Population Data | transfermarkt-datasets (`games.csv`) |
| Source link | https://catalog.data.gov/dataset/electric-vehicle-population-data | https://github.com/dcaribou/transfermarkt-datasets |
| Date accessed | 2026-09-25 | 2026-09-25 |
