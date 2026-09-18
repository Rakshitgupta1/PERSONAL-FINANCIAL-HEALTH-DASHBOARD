# PERSONAL-FINANCIAL-HEALTH-DASHBOARD

An Excel-based automation tool that turns raw bank transaction data into a single, defensible **Financial Health Score (0–100)** — built with Power Query, VBA, and a custom-designed scoring model.

## The Problem

Most people can see *how much* they spent in a month, but not whether that spending pattern is actually healthy. A single ratio (like savings rate) doesn't capture the full picture — someone could be saving well but carrying dangerous debt, or have a comfortable income but no emergency cushion at all.

This project answers that by combining four independent factors into one composite score:

| Factor | What it measures | Full marks at |
|---|---|---|
| Savings Rate | Income saved vs. spent | 20%+ savings rate |
| Debt-to-Income | Debt burden relative to income | 0% debt |
| Emergency Fund Coverage | Months of expenses covered by savings | 6+ months |
| Expense Volatility | Month-to-month spending stability | Low variation |

Each factor is scored 0–25 and summed into a final 0–100 Health Score.

## How It Works

**1. Data Ingestion (Power Query)**
Raw bank/card statement CSVs are dropped into a `/Statements` folder. Power Query automatically detects new files, cleans the data, and standardizes column types — no manual data entry required.

**2. Categorization (Power Query)**
Every transaction is auto-categorized (Food, Transport, Housing, etc.) using a fully transparent, auditable keyword-matching table (`Category_Rules` sheet) — not a black-box classifier. This was a deliberate design choice: every categorization decision can be traced and explained.

**3. Scoring Engine (Excel formulas)**
The `Health_Score_Engine` sheet computes each of the four sub-scores using custom-weighted formulas, then sums them into the final score per month.

**4. Automation (VBA)**
Three one-click macros handle the full workflow:
- **Refresh Data** — refreshes all Power Query connections and recalculates scores
- **Import New Statement** — prompts for a new CSV and drops it into the watched folder
- **Export Report** — generates a clean PDF snapshot of the dashboard

**5. Dashboard (Excel charts + PivotTables)**
- Current Health Score + month-over-month change indicator
- Score Component Breakdown (which factor is driving the score)
- Income vs. Expenses trend
- Category spend totals and category spend trend over time
- Debt-to-Income and Emergency Fund Coverage KPI cards

## Tech Stack

- **Power Query (M)** — data ingestion, cleaning, categorization
- **Excel formulas** — scoring engine (SUMIFS, custom weighting logic)
- **VBA** — workflow automation (refresh, import, export)
- **PivotTables & Charts** — dashboard visualization

## Try It Yourself

1. Clone this repo
2. Open `Financial_Health_Dashboard.xlsm` (enable macros and content when prompted)
3. Sample statement data is already loaded in `/Statements` — click **Refresh Data** to see it flow through the pipeline
4. Try **Import New Statement** with the extra sample file in `/sample-data/` to see a new month get categorized and scored automatically

> Note: all data in this repo is synthetic/dummy data generated for demonstration purposes — no real financial information is included.

## Why This Approach

Most personal finance templates apply someone else's pre-built ratios. This project's scoring bands (20% savings rate, 6-month emergency fund, etc.) are my own weighting decisions, and the keyword-based categorization was chosen deliberately over a fuzzy/ML approach for full transparency and auditability — every score and category can be explained and defended, not just computed.

## Author

Built by [Your Name] — Economics Honours student, CFA Level 1 / FRM Part 1 candidate.
