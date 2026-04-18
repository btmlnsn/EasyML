# EasyML

> A small domain-specific language and Python interpreter for loading tabular data, basic cleaning, and training a choice of two sklearn models—built as a final project for a programming class.

## What it is

EasyML runs `.ezml` scripts line by line: set a file path, load CSV or Excel, clean rows, optionally fit classification or regression (picking between two fixed model pairs), and export datasets or models to `exported/`. It is a learning exercise, not a production ML system.

## Tech stack

Python 3.11, pandas, scikit-learn (linear/logistic regression, decision tree classifier, random forest regressor), joblib, openpyxl (Excel). Dependencies are pinned in `environment.yml` and `requirements.txt`.

## Prerequisites

- [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/) with `conda` on your `PATH`
- Your own CSV/XLSX data if you run the samples (see `trainingData/README.md`)

## Setup

1. Clone this repository and `cd` into the project root (the directory that contains `easyML.py` and `environment.yml`).
2. Create the environment:
   ```bash
   conda env create -f environment.yml
   ```
3. Activate it:
   ```bash
   conda activate undergrad-archive--easyml
   ```
4. Create an output directory (first `DOWNLOAD` will fail if it is missing):
   ```bash
   mkdir -p exported
   ```

## Usage

```bash
conda activate undergrad-archive--easyml
cd /path/to/EasyML
python easyML.py your_script.ezml
```

```text
DATAPATH myPath = 'data/myfile.csv'
DATASET myDf = LOAD myPath
CLEAN myDf
MODEL myModel = PREDICT_CAT(myDf, COLUMN J)
DOWNLOAD DATASET myDf
DOWNLOAD MODEL myModel
```

```text
DATAPATH myPath = 'data/myfile.csv'
DATASET myDf = LOAD myPath
CLEAN myDf
MODEL myModel = PREDICT_NUM(myDf, COLUMN I)
DOWNLOAD DATASET myDf
DOWNLOAD MODEL myModel
```

## Sample scripts

- **sample1.ezml** — Loads `running.xlsx`, cleans, exports the dataset only.
- **sample2.ezml** — Loads `Titanic.csv`, cleans, trains classification on `COLUMN J`, exports dataset and model.
- **sample3.ezml** — Loads `housing.csv`, cleans, trains regression on `COLUMN I`, exports dataset and model.

## Known limitations

- One statement per line; whitespace splitting (`line.split()`). Targets use `COLUMN` letters (A=0, …). `PREDICT_CAT` vs `PREDICT_NUM`; paths with spaces are fragile.
- No unit tests or CI; little error handling beyond a missing script file.
- No datasets in the repo; samples assume files exist at the given `DATAPATH` (see `trainingData/README.md` for formats and public sources).
- `exported/` is not created automatically.
- Model choice and metrics are simplistic; multiclass and messy real-world tables can still break edge cases.

## License

Apache License 2.0 — see `LICENSE`.
