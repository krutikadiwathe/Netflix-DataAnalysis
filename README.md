# Netflix Movie Data Analysis

Analyze ~9,000+ Netflix movies to answer practical business questions:

- What’s the most frequent **genre**?
- Which title has the **highest vote average**?
- Which title is **most** and **least** **popular** (and what are their genres)?
- Which **year** released the most movies?

This repo contains the data file, an exploratory Jupyter notebook.

---

## 🧭 Project Overview

This is a compact, reproducible analysis focused on exploratory data analysis (EDA) and clear storytelling. The notebook cleans the data, explores distributions, and surfaces trends in genre, ratings, popularity, and release year.

**Core artifacts**

- `data/mymoviedb.xls` — raw dataset
- `notebooks/moviedata-Netflix.ipynb` — main EDA notebook

---

## ✨ Highlights

- Robust type handling for dates and numeric columns
- Quantile-based bucketing for popularity/vote scores
- Clear visuals to explain distributions and outliers
- Simple, reproducible environment (just `pip install -r requirements.txt`)

---

## 📁 Repository Structure

## 📁 Repository Structure

```text
.
├── data/
│   └── mymoviedb.xls
├── notebooks/
│   └── moviedata-Netflix.ipynb
├── README.md
├── requirements.txt
└── .gitignore

---

## ⚙️ Setup & Run

1. **Clone** the repo
   git clone https://github.com/<your-username>/netflix-movie-analysis.git
   cd netflix-movie-analysis

2. **Create & activate** a virtual environment (optional but recommended)
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   # source .venv/bin/activate

3. **Install dependencies**
   pip install -r requirements.txt

4. **Launch the notebook**
   jupyter notebook notebooks/moviedata-Netflix.ipynb

---

## 🧹 Data Cleaning Notes

- Convert date columns to datetime (e.g., `Release_Date`) and extract `Release_Year` for year-based analysis.
- Ensure numeric columns are parsed correctly (e.g., `Vote_Average`, `Popularity`, `Vote_Count`). Use `pd.to_numeric(..., errors="coerce")`.
- Handle missing values with sensible defaults or explicit exclusion depending on the chart/metric.

Example snippet:

import pandas as pd

df = pd.read_excel("data/mymoviedb.xls")

# Dates
df["Release_Date"] = pd.to_datetime(df["Release_Date"], errors="coerce")
df["Release_Year"] = df["Release_Date"].dt.year

# Numerics
for c in ["Vote_Average", "Popularity", "Vote_Count"]:
    df[c] = pd.to_numeric(df[c], errors="coerce")

# Equal-frequency buckets for a score
labels = ["not_popular", "below_avg", "average", "popular"]
df["Popularity_Bucket"] = pd.qcut(df["Popularity"], q=[0, .25, .5, .75, 1.0],
                                  labels=labels, duplicates="drop")

---

## 📊 What’s in the Notebook

- Descriptive stats and distribution plots
- Top genres (overall and by year)
- Most/least popular titles with genres
- Highest vote average (with tie handling)
- Year with most releases

---

## ✅ Reproducible Results Checklist

- [ ] Notebook runs top-to-bottom without manual edits
- [ ] Environment is captured in `requirements.txt`
- [ ] Key plots exported to `reports/figures/`
- [ ] README updated with 2–3 headline insights

---

## 🧪 Requirements

See `requirements.txt`.

---

## 📝 License

MIT — feel free to use, remix, and learn from this project. Add attribution if you fork.

---

## 🙋 Contact

Questions or suggestions? Open an issue or connect on LinkedIn.
