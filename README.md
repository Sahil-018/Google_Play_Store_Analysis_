# Google_Play_Store_Analysis_
# 📱 Google Play Store — Exploratory Data Analysis (EDA)

## 📌 Overview

This project performs a comprehensive Exploratory Data Analysis (EDA) on the
Google Play Store dataset. The dataset contains 10,841 apps spread across 34
unique categories and 120 genres, capturing key attributes like ratings,
installs, size, pricing, content rating, and more.

The objective is to go beyond surface-level observations and extract
**concrete, business-relevant insights** that a developer or product team can
act on — such as which categories to target, how pricing affects perception,
and what drives installs.

---

## 📂 Dataset Details

| Property         | Value                          |
|-----------------|-------------------------------|
| Source           | Google Play Store (CSV)        |
| Total Records    | 10,841 apps                    |
| Total Features   | 13 columns                     |
| Categories       | 34 unique                      |
| Genres           | 120 unique                     |
| Time Range       | Apps last updated from 2010–2018 |

### 🗂️ Columns

| Column | Description |
|---|---|
| `App` | Name of the application |
| `Category` | App category (e.g., GAME, TOOLS, FAMILY) |
| `Rating` | Average user rating (out of 5) |
| `Reviews` | Total number of user reviews |
| `Size` | App size (MB or KB) |
| `Installs` | Install count bucket (e.g., 10,000+) |
| `Type` | Free or Paid |
| `Price` | Price in USD (0 for free apps) |
| `Content Rating` | Audience suitability (e.g., Everyone, Teen) |
| `Genres` | Sub-genre tags |
| `Last Updated` | Date of last update |
| `Current Ver` | Current app version |
| `Android Ver` | Minimum Android version required |

---

## 🔍 EDA Sections & What Was Analysed

### 1. 🗃️ Data Overview & Cleaning
- Loaded dataset: **10,841 rows × 13 columns**
- Identified and handled missing values:
  - `Rating`: 1,474 missing values → converted to numeric, NaNs dropped for analysis
  - `Type`: 1 missing
  - `Content Rating`: 1 missing
  - `Current Ver`: 8 missing
  - `Android Ver`: 3 missing
- Cleaned `Installs` column (removed `+` and `,`) for numeric operations
- Cleaned `Size` column (converted M/k suffixes to numeric MB)
- Cleaned `Price` column (stripped `$` symbol)
- Detected a data anomaly: one row had a rating of **19.0** (impossible on a 5-star scale) — treated as an outlier

---

### 2. 📊 Category Analysis
**Goal:** Understand how apps are distributed across categories and identify
which categories are most saturated.

**Top 10 Categories by App Count:**

| Category | App Count |
|---|---|
| FAMILY | 1,972 |
| GAME | 1,144 |
| TOOLS | 843 |
| MEDICAL | 463 |
| BUSINESS | 460 |
| PRODUCTIVITY | 424 |
| PERSONALIZATION | 392 |
| COMMUNICATION | 387 |
| SPORTS | 384 |
| LIFESTYLE | 382 |

📌 **Visualisation used:** Line chart — App distribution across all categories

---

### 3. ⭐ Rating Analysis
**Goal:** Understand how apps are rated overall and which categories
consistently earn higher ratings.

**Overall Rating Statistics:**

| Metric | Value |
|---|---|
| Count (non-null) | 9,367 |
| Mean | 4.19 |
| Std Dev | 0.54 |
| Min | 1.0 |
| 25th Percentile | 4.0 |
| Median (50%) | 4.3 |
| 75th Percentile | 4.5 |
| Max (valid) | 5.0 |

**Top Categories by Average Rating:**

| Category | Avg Rating |
|---|---|
| EVENTS | 4.44 |
| EDUCATION | 4.39 |
| ART_AND_DESIGN | 4.36 |
| BOOKS_AND_REFERENCE | 4.35 |
| PERSONALIZATION | 4.34 |
| PARENTING | 4.30 |
| GAME | 4.29 |
| BEAUTY | 4.28 |
| HEALTH_AND_FITNESS | 4.28 |

📌 **Visualisations used:**
- Histogram — rating distribution
- Horizontal bar chart (Seaborn) — average rating per category
- Interactive box plot (Plotly Express) — rating spread & outliers for top 10 categories

---

### 4. 📦 Size & Installs Analysis
**Goal:** Check whether app size influences how many users install it.

**Install Count Statistics:**

| Metric | Value |
|---|---|
| Mean | ~15.5 Million |
| Median | 100,000 |
| 75th Percentile | 5,000,000 |
| Max | 1,000,000,000 |

**Correlation between Size and Installs: r ≈ 0.015** (extremely weak)

> App size has virtually no linear relationship with the number of installs.
> A heavier app does not automatically attract more users.

📌 **Visualisation used:** Scatter plot — App Size vs Installs

---

### 5. 💰 Pricing Analysis
**Goal:** Understand the pricing landscape and the split between free and paid apps.

**Free vs Paid Split:**

| Type | Count |
|---|---|
| Free | 10,039 (92.6%) |
| Paid | 800 (7.4%) |

**Paid App Price Statistics:**

| Metric | Price (USD) |
|---|---|
| Min | $0.99 |
| 25th Percentile | $1.49 |
| Median | $2.99 |
| 75th Percentile | $4.99 |
| Max | $400.00 |
| Mean | $13.92 |

**Most Common Price Points:**
`$0.99` (148 apps) → `$2.99` (129 apps) → `$1.99` (73 apps) → `$4.99` (72 apps)

📌 **Visualisations used:**
- Price distribution chart
- Estimated revenue by price tier (Plotly interactive bar chart)

---

### 6. 📈 Installs vs Rating Relationship
**Goal:** Check whether more downloads correlate with better ratings.

| Install Bucket | Avg Rating |
|---|---|
| < 1K | 4.20 |
| 1K – 100K | 4.07 |
| 100K – 1M | 4.21 |
| 1M+ | 4.31 |

> Apps with 1M+ installs have the highest average rating (4.31), suggesting
> that quality-driven apps attract more users — not the other way around.

---

### 7. 👥 Content Rating Distribution

| Content Rating | App Count |
|---|---|
| Everyone | 8,714 |
| Teen | 1,208 |
| Mature 17+ | 499 |
| Everyone 10+ | 414 |
| Adults only 18+ | 3 |
| Unrated | 2 |

> Over **80% of all apps on the Play Store** are rated for Everyone —
> a clear signal that the platform's primary audience skews family-friendly.

---

### 8. 🏆 Most Reviewed Apps (Top 10)

| App | Category | Reviews | Rating |
|---|---|---|---|
| Facebook | SOCIAL | 78,158,306 | 4.1 |
| WhatsApp Messenger | COMMUNICATION | 69,119,316 | 4.4 |
| Instagram | SOCIAL | 66,577,446 | 4.5 |
| Messenger | COMMUNICATION | 56,646,578 | 4.0 |

---

## 💡 Key Insights & Business Recommendations

### 1. 🎯 Target Less Saturated, Well-Rated Categories
FAMILY (1,972 apps) and GAME (1,144 apps) are extremely crowded. Categories
like EVENTS, EDUCATION, and ART_AND_DESIGN have far fewer apps but
consistently high average ratings (4.35–4.44), meaning less competition and
more satisfied users.

**Action:** Enter a category where you can realistically reach or beat the
median rating with a quality product, rather than fighting for visibility in
an over-saturated space.

---

### 2. 🏗️ App Size Does Not Drive Installs (r ≈ 0.015)
There is virtually no correlation between how large an app is and how many
people install it. Heavy apps do not get more downloads — quality and
reputation do.

**Action:** Focus development resources on UX, stability, and update
frequency rather than feature-bloating the app to appear more "complete."

---

### 3. ⭐ Quality Drives Scale — Not the Other Way Around
Apps with 1M+ installs average a 4.31 rating vs. 4.07 for apps in the 1K–100K
range. High-quality apps earn good ratings, and good ratings attract more
installs — it's a compounding effect.

**Action:** Prioritize the early user experience and act fast on negative
reviews. Your first 1,000 reviews set the trajectory.

---

### 4. 💵 Free with In-App Purchases Dominates
92.6% of apps are free. Among paid apps, the most popular price points are
$0.99, $2.99, and $1.99. Only a handful of niche apps (mostly in MEDICAL and
BUSINESS) command prices above $50.

**Action:** For most categories, a free-with-ads or freemium model is the
most viable path. Paid pricing above $4.99 needs a very specific,
professional user base to justify it.

---

### 5. 📊 Benchmark Within Your Category, Not Across All Apps
Each category has its own rating distribution. A 4.1 rating in SOCIAL might
be competitive, while the same rating in EDUCATION is below the median.

**Action:** Before launch, check the box plot for your target category —
aim to be at or above the median, and study the top-rated apps in that
specific space.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.12 | Core programming language |
| Pandas | Data loading, cleaning, transformation |
| NumPy | Numerical operations |
| Matplotlib | Static charts and plots |
| Seaborn | Statistical visualisations (bar charts, histograms) |
| Plotly Express | Interactive charts (box plots, bar charts) |

---

## 📊 Visualisations Produced

- Rating distribution — Histogram
- Average rating by category — Horizontal bar chart (Seaborn)
- App count per category — Line chart (Matplotlib)
- App size vs installs — Scatter plot
- Avg rating by install bucket — Interactive bar chart (Plotly)
- Rating distribution by category (Top 10) — Interactive box plot (Plotly)

---

## 🚀 How to Run

```bash
git clone https://github.com/Sahil-018/<repo-name>
cd <repo-name>
pip install pandas numpy matplotlib seaborn plotly
jupyter notebook GooglePlayStore.ipynb
```

> Dataset required: `googleplaystore.csv` — place it in the same directory
> as the notebook before running.

---

## 👤 Author

**Sahil Kale**
📍 Pune, Maharashtra, India
🔗 [LinkedIn](https://linkedin.com/in/sahil-kale01) | [GitHub](https://github.com/Sahil-018)
