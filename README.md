# 📈 Google Stock Analysis 2004–2025

> **An interactive single-page Power BI dashboard analyzing 21 years of Google (GOOG) stock data — covering price trends, volume patterns, annual returns, and volatility from IPO to present.**

---

## 📊 Dashboard Preview

![Google Stock Analysis Dashboard](https://github.com/rohithap0819/Google-Stock-Analysis-2004-2025/blob/main/Google%20stock%20analysis%20Dashobard%20image.png)

> A single-page dashboard with 5 KPI cards, 5 charts, and 2 interactive slicers — built entirely from the raw CSV using DAX calculated columns and measures.

---

## 🔢 Key Stats at a Glance

| Metric | Value |
|--------|-------|
| Analysis Period | 19 Aug 2004 → 19 Aug 2025 |
| Total Trading Days | 5,284 |
| Latest Close Price | $202.49 |
| All-Time High | $208.70 |
| All-Time Low | $2.39 |
| Total Return (IPO → 2025) | **+8,239%** |
| Avg Daily Price Range | $1.09 |
| Avg Daily Volume | 111M shares |
| Peak Single-Day Volume | 1.65B shares |

---

## 🖥️ Dashboard Components

### KPI Cards (left panel)

| Card | Value | DAX Measure |
|------|-------|-------------|
| Current Price | $202.49 | `LASTNONBLANK` on close |
| All-Time High | $208.70 | `MAX([high])` |
| All-Time Low | $2.39 | `MIN([low])` |
| Total Return % | 8,239% | `DIVIDE(MAX-MIN, MIN)` |
| Avg Daily Range | $1.09 | `AVERAGEX([high]-[low])` |

### Charts

| # | Chart Title | Visual Type | Key Insight |
|---|-------------|-------------|-------------|
| 1 | Closing price over time (2004–2025) | Area / Line chart | Exponential growth — flat 2004–2015, explosive post-2020 |
| 2 | Yearly avg closing price | Column chart | Consistent YoY growth with dips in 2008 and 2022 |
| 3 | Yearly avg volume (declining trend) | Column + trend line | Volume fell from 364M (2004) to 24M (2025) — 93% drop |
| 4 | Annual return % | Bar chart (green/red) | 15 positive years, 5 negative — worst: 2008 (−56%), best: 2005 (+110%) |
| 5 | Volume vs daily price change | Scatter chart | Higher volume correlates with larger daily price swings |

### Slicers

| Slicer | Type |
|--------|------|
| Year | Dropdown |
| Date range | Between slider |

---

## 📁 Repository Structure

```
Google-Stock-Analysis-2004-2025/
│
├── GOOG_2004-08-19_2025-08-20.csv    ← Raw stock data (5,284 rows)
├── Google Stock Anlysis.pbix          ← Power BI dashboard file
├── dashboard_preview.png              ← Dashboard screenshot 
├── README.md
└── LICENSE
```

---

## 🗂️ Dataset Overview

**Source:** Kaggle — Google (GOOG) historical daily prices  
**Period:** 19 August 2004 – 19 August 2025  
**Rows:** 5,284 trading days · **Columns:** 7

| Column | Description | Type |
|--------|-------------|------|
| `date` | Trading date | Date |
| `open` | Opening price ($) | Float |
| `high` | Intraday high ($) | Float |
| `low` | Intraday low ($) | Float |
| `close` | Closing price ($) | Float |
| `adj_close` | Dividend/split-adjusted close | Float |
| `volume` | Shares traded | Integer |

---

## 🔑 DAX Measures & Calculated Columns

```dax
-- ── Calculated Columns (create before building any visuals) ──
Year           = YEAR('GOOG'[date])
Month Num      = MONTH('GOOG'[date])
Month Name     = FORMAT('GOOG'[date], "MMM")
Quarter        = "Q" & QUARTER('GOOG'[date])
Daily Range    = 'GOOG'[high] - 'GOOG'[low]
Daily Return % = DIVIDE('GOOG'[close] - 'GOOG'[open], 'GOOG'[open]) * 100
Price Change   = 'GOOG'[close] - 'GOOG'[open]

-- ── KPI Measures ──
Current Price    = CALCULATE(LASTNONBLANKVALUE('GOOG'[date], 'GOOG'[close]))
All Time High    = MAX('GOOG'[high])
All Time Low     = MIN('GOOG'[low])
Avg Daily Range  = AVERAGEX('GOOG', 'GOOG'[high] - 'GOOG'[low])
Total Return %   = DIVIDE(MAX('GOOG'[close]) - MIN('GOOG'[close]), MIN('GOOG'[close]))
Avg Daily Volume = AVERAGE('GOOG'[volume])
Trading Days     = COUNTROWS('GOOG')

-- ── Annual Return ──
Annual Return % = 
DIVIDE(
    LASTNONBLANKVALUE('GOOG'[date], 'GOOG'[close]) - 
    FIRSTNONBLANKVALUE('GOOG'[date], 'GOOG'[open]),
    FIRSTNONBLANKVALUE('GOOG'[date], 'GOOG'[open])
) * 100
```

---

## 💡 Key Insights

### 1. +8,239% total return over 21 years
Google's stock grew from ~$2.50 at IPO (August 2004) to $202.49 by August 2025. An investor who put $1,000 at IPO would have ~$82,390 today — without accounting for any dividends.

### 2. Volume has declined 93% since IPO
Average daily trading volume fell from **364M shares** in 2004 to just **24M shares** in 2025. This reflects Google's evolution from a speculative growth stock to a stable blue-chip holding — institutions hold and rarely trade.

### 3. 2022 was the worst year since 2008
Google lost **−38.6%** in 2022 — its second-worst year on record after the 2008 financial crisis (−55.6%). Both were macro-driven selloffs, not company-specific events.

### 4. Positive years dominate — 15 out of 21
GOOG posted positive annual returns in **15 of 21 years** (71.4%). The only negative years were 2008, 2010, 2014, 2018, and 2022 — all correlated with broader market downturns.

### 5. High volume = high volatility
The scatter chart confirms that days with the highest trading volume have significantly wider High−Low daily ranges — indicating that institutional activity and news events amplify intraday price swings.

### 6. Growth accelerated massively post-2020
From IPO (2004) to 2015: stock went from ~$2.50 to ~$30 (12× in 11 years).  
From 2015 to 2025: stock went from ~$30 to $202 (6.7× in 10 years, with far larger absolute dollar moves per day).

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard development & visualization |
| **DAX** | Calculated columns and KPI measures |
| **Power Query** | Date parsing and data type formatting |
| **Yahoo Finance** | Source of raw historical stock data |

---

## 🚀 How to Use

1. **Clone or download** this repository
   ```bash
   git clone https://github.com/rohithap0819/Google-Stock-Analysis-2004-2025.git
   ```

2. **Open the dashboard**  
   Open `Google Stock Anlysis.pbix` in **Power BI Desktop** (free download from Microsoft)

3. **Interact with slicers**
   - Use the **Year dropdown** to filter to any specific year or range of years
   - Use the **Date range slider** to zoom into any custom time window (e.g. 2020–2022 crash and recovery)

4. **Explore the charts**
   - The closing price area chart auto-scales when you apply filters
   - The annual return chart turns **green** for positive years and **red** for negative years automatically via conditional formatting
   - The scatter chart reveals the volume–volatility relationship interactively

5. **Use the raw CSV**  
   The file `GOOG_2004-08-19_2025-08-20.csv` can be loaded directly into Python (pandas), Excel, Tableau, or any analytics tool for further analysis.

---

## 📌 Assumptions & Limitations

- All prices are in **USD** sourced from Yahoo Finance historical data
- The `adj_close` column accounts for stock splits and dividends; the raw `close` column does not — both are included for comparison purposes
- Google executed a **20-for-1 stock split in July 2022** — prices in this dataset are already adjusted to post-split equivalents across the full history
- Volume data represents shares traded during regular market hours only; pre-market and after-hours volume is excluded
- The dataset ends on **19 August 2025** — any subsequent price movements are not reflected
- Past performance does not indicate future results — this is an educational analysis only

---

## 👤 Author

**Rohith A P**  
Data Analytics Enthusiast  
[GitHub Profile](https://github.com/rohithap0819)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## ⭐ Support

If you found this useful, give the repo a **star** ⭐ and feel free to **fork** it to build your own stock analysis on top of this template!

---
