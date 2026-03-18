# Customer Call List — Data Cleaning Project

A beginner-friendly data cleaning workflow using **Python** and **pandas**. Raw customer data from an Excel spreadsheet is cleaned, standardised, and filtered down to a actionable call list.

---

## Files

| File | Description |
|---|---|
| `customer_call_list.xlsx` | Raw source data — 21 customer records across 10 columns |
| `data_cleaning_in__pandas.ipynb` | Jupyter notebook containing the full cleaning pipeline |

---

## Dataset Overview

The raw Excel file (`customer_call_list.xlsx`) contains messy customer records with the following issues:

- **Inconsistent phone number formats** — delimiters include `-`, `/`, `|`, and raw digits
- **Dirty name fields** — stray characters (`/`, `.`, digits) embedded in last names
- **Inconsistent boolean values** — `Yes`/`No`/`Y`/`N`/blank used interchangeably for `Paying Customer` and `Do_Not_Contact`
- **Combined address field** — street, state, and zip stored in a single column
- **Duplicate rows** and a wholly irrelevant column (`Not_Useful_Column`)
- **Missing values** scattered across multiple columns

---

## Cleaning Steps

The notebook walks through the pipeline step by step:

1. **Load data** — read the Excel file into a pandas DataFrame
2. **Drop duplicates** — remove any fully duplicated rows
3. **Drop irrelevant column** — remove `Not_Useful_Column`
4. **Clean `Last_Name`** — strip leading/trailing junk characters (`1 2 3 . / _`)
5. **Standardise `Phone_Number`** — strip all non-alphanumeric characters, then reformat to `XXX-XXX-XXXX`; blank out malformed/missing entries
6. **Split `Address`** — expand the single address column into `Street_Address`, `State`, and `Zip_Code`
7. **Normalise `Paying Customer`** — convert all variants to `Y` / `N`
8. **Normalise `Do_Not_Contact`** — convert all variants to `Y` / `N`
9. **Fill nulls** — replace all remaining `NaN` values with empty strings
10. **Filter out do-not-contact records** — drop any row where `Do_Not_Contact == 'Y'`
11. **Filter out missing phone numbers** — drop any row with no valid phone number
12. **Reset index** — reindex the final DataFrame cleanly from 0

---

## Requirements

```
Python 3.14
pandas
openpyxl      # required by pandas to read .xlsx files
jupyter       # to run the notebook
```

Install dependencies:

```bash
pip install pandas openpyxl jupyter
```

---

## Usage

```bash
# Clone or download the project, then:
jupyter notebook data_cleaning_in__pandas.ipynb
```

Make sure `customer_call_list.xlsx` is in the **same directory** as the notebook before running.

---

## Output

After running all cells, the DataFrame contains only customers who:

- have consented to being contacted (`Do_Not_Contact != 'Y'`)
- have a valid, consistently formatted phone number

All columns are clean and ready for export or further analysis.
