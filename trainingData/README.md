# Training data (local only)

Place **your own copies** of datasets here (or in the project root next to `easyML.py`, matching each sample’s `DATAPATH`). This folder is for documentation and optional storage; **no data files are committed** to the repository.

## Expected formats

EasyML loads tabular data only:

| Format | Extension | Notes |
|--------|-----------|--------|
| **CSV** | `.csv` | Comma-separated (pandas default). UTF-8 encoding is recommended. First row should be column headers unless your file truly has no header (samples assume a normal header row). |
| **Excel** | `.xlsx` | First sheet is read by default (`pandas.read_excel`). |

All columns should be usable as a table: each row is one record, each column one variable. The interpreter’s `CLEAN` step drops rows with missing values and rows where Python’s per-cell `type()` does not match the column’s most common type—so avoid mixed-type columns if you want to keep rows.

---

## Sample scripts and what they need

Paths in the `.ezml` files are **relative to your current working directory** when you run `python easyML.py …` (often the repo root). If you keep files under `trainingData/`, set `DATAPATH` accordingly, e.g. `trainingData/Titanic.csv`.

### `sample1.ezml` — `running.xlsx`

- **File:** `running.xlsx` (or change `DATAPATH` to point at your file).
- **Purpose:** Load → clean → export CSV. **No target column** is required.
- **Layout:** Any reasonable tabular `.xlsx` works; cleaning is generic.

### `sample2.ezml` — `Titanic.csv` (classification)

- **File:** `Titanic.csv` (or change `DATAPATH`).
- **Script target:** `COLUMN J` → **0-based column index 9** (Excel-style letters: A=0, …, J=9). The **10th column** of the table (after the header row) is used as the **classification target**; all other columns are features.
- **Important:** Many public Titanic files (e.g. Kaggle’s `train.csv`) order columns so that **`Survived` is the 2nd column (`COLUMN B`)**, not the 10th. If you use Kaggle’s file as-is, **`COLUMN J` may point at a different field** (e.g. `Fare`) than survival. Either:
  - Reorder columns so your intended categorical target is in the **10th** position, or  
  - Edit `sample2.ezml` to use the letter that matches your target’s column (e.g. `COLUMN B` for Kaggle’s `Survived`).

**Where to get Titanic data (public):**

- Kaggle — *Titanic: Machine Learning from Disaster*: https://www.kaggle.com/competitions/titanic/data — download `train.csv` (rename to `Titanic.csv` if you like, or adjust `DATAPATH`).
- Many universities and tutorials mirror the same CSV; any standard Titanic table is fine as long as **column order matches the `COLUMN …` you use**.

### `sample3.ezml` — `housing.csv` (regression)

- **File:** `housing.csv` (or change `DATAPATH`).
- **Script target:** `COLUMN I` → **0-based column index 8** (the **9th** data column). That column is the **numeric regression target**; other columns are features.

**Typical layout that matches `COLUMN I`:** a **9-column** file where the **last** column is the median house value (common for California Housing–style exports: 8 feature columns + 1 target).

**Where to get a compatible housing dataset (public):**

- **California Housing** (regression, 8 features + median house value): bundled in **scikit-learn** as `sklearn.datasets.fetch_california_housing`. You can export it to CSV yourself (8 feature columns + target as the 9th column) and save as `housing.csv`.
- **StatLib / CMU** hosted copies of the California housing data are often linked from course materials; URLs change, so prefer generating from scikit-learn for a stable column layout.

If your `housing.csv` has a different column order or more than nine columns, **count columns from A=0** and set `COLUMN …` in `sample3.ezml` to the letter for your target column, or reorder the CSV.

---

## Quick check before you run

1. File exists at the path used in `DATAPATH` (or under `trainingData/` with matching path).
2. For `sample2` / `sample3`, the **target column index** matches the `COLUMN` letter in the script (A=0, B=1, …).
3. Run from the directory where those relative paths resolve, or use absolute paths in `DATAPATH`.

The repo does **not** ship `trainingData.zip` or any `.csv` / `.xlsx` binaries; obtain data from the sources above and add files locally.
