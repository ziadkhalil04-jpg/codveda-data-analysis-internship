# Codveda Data Analysis Internship – Level 1 (Basic)

Level 1 of the **Codveda Technologies** Data Analysis internship, completed on one real-world dataset:
**Capture fisheries vs. Aquaculture production** (metric tons per country, 1960–2018).

| Task | Topic | Notebook |
|------|-------|----------|
| Task 1 | Data Cleaning and Preprocessing | `Task_one/task1_data_cleaning.ipynb` |
| Task 2 | Exploratory Data Analysis (EDA) | `task_two/task2_eda.ipynb` |

**Tools:** Python, pandas, NumPy, matplotlib, seaborn

---

## Dataset

- **Rows / columns:** 14,674 rows × 5 columns
- **Columns:** `Entity`, `Code`, `Year`, `Aquaculture production (metric tons)`, `Capture fisheries production (metric tons)`
- **Coverage:** 1960–2018
- **Source:** *[add the link where you downloaded it, e.g. Kaggle / Our World in Data]*

The file mixes **countries** with **regional and income-group aggregates** (e.g. *High income*, *Europe & Central Asia*, *World*). Aggregates have no country `Code` (or the `World` code), so they must be separated from countries to avoid double counting.

---

## Project structure

```
level1/
├── README.md
├── Task_one/                      # Task 1 – Data Cleaning
│   ├── task1_data_cleaning.ipynb
│   ├── dataDirty/                 # raw dataset
│   ├── DataCleaning/              # cleaned dataset (cleaned_data.csv)
│   └── images/
└── task_two/                      # Task 2 – EDA
    ├── task2_eda.ipynb
    ├── Data/                      # dataset used for EDA
    └── images/                    # exported charts
```

---

## Task 1 – Data Cleaning and Preprocessing

**Objective:** load a raw CSV with pandas, handle missing values, and check for duplicates.

**What was done**
1. Loaded the raw CSV with pandas and inspected it (`head`, `info`, `duplicated`, `isnull`).
2. **Duplicates:** checked for duplicate rows, and none were found (0).
3. **Missing values found:**

   | Column | Missing |
   |--------|---------|
   | `Code` | 2,773 |
   | `Aquaculture production` | 3,017 |
   | `Capture fisheries production` | 158 |

4. **Handling:**
   - Missing `Code` filled with the label `"no Code"` (these rows are aggregates, not countries).
   - Missing production values filled with `0`.
5. Verified that no missing values remain, then exported `cleaned_data.csv`.

**Assumption to be aware of:** filling production with `0` assumes "not reported" means "no production". This keeps every row, but a missing value is not necessarily a true zero.

---

## Task 2 – Exploratory Data Analysis (EDA)

**Objective:** summary statistics, distributions, and correlations between numerical features.

**What was done**
1. Loaded the data and removed rows with missing values (`dropna`), which reduced it from 14,674 to 8,726 rows. Zero-filling was avoided here because it would distort the mean, median and correlation.
2. Renamed columns to short names and separated **countries** (194 countries, 8,670 rows) from the **World** aggregate.
3. **Summary statistics:** mean, median, mode, standard deviation, min and max.
4. **Visualizations:**
   - Histograms (raw and log scale)
   - Boxplots (overall and by decade)
   - Scatter plot of aquaculture vs capture (2018, log-log)
   - Top 10 aquaculture producers (2018)
5. **Correlation:** Pearson and Spearman matrices with heatmaps.

All charts are exported to `images/`.

### Key findings

- **The data is strongly right-skewed.** For aquaculture, the median is about **888 t** while the mean is about **222,652 t**. For capture fisheries, the median is about **52,317 t** and the mean about **485,321 t**. A few large producers pull the averages up, so the median describes a typical country better.
- **China is a major outlier** in aquaculture, with about **66.1 million t in 2018**, followed by Indonesia (about 14.8 M t) and India (about 7.1 M t).
- **Moderate positive correlation** between aquaculture and capture fisheries: Pearson ≈ **0.62**, Spearman ≈ **0.61**. This shows association, not causation.
- The mode of both columns is `0`, since many country-years have zero production.

### Limitations

- Removing every row with a missing value excludes some countries entirely and favors recent years, when reporting was more complete. Results describe the *reported* data, not necessarily all countries.
- Aggregates (regions and income groups) were excluded from country-level statistics to avoid double counting.


Open each notebook and choose **Run All**. Paths inside the notebooks are relative to the notebook's own folder.

---

## Author

**Ziad ElSayed** – Data Analysis Intern at Codveda Technologies
*[www.linkedin.com/in/ziad-khalil-dev] / [https://github.com/ziadkhalil04-jpg]*

#CodvedaInternship #CodvedaTech #CodvedaProjects #DataAnalysis #Python #pandas
