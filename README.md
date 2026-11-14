# Retail Customer Segmentation (RFM)

A customer segmentation analysis of 4,372 customers from a UK-based online retailer, using RFM (Recency, Frequency, Monetary) methodology to identify revenue concentration and inform retention strategy.

**Interactive dashboard:** 
https://public.tableau.com/app/profile/ritz.s7687/viz/CustomerSegmentationRFM_17946346690550/RFMDashboard?publish=yes

## Tools Used
- **SQL (SQLite):** data cleaning, transaction-level querying, RFM calculation
- **Python (pandas):** quartile-based RFM scoring and segmentation logic
- **Google Sheets:** pivot tables for first-pass visualization
- **Tableau Public:** interactive dashboard (segment shares, segment profiles, customer scatter)

## Business Problem
Which customers drive revenue, and where is the business exposed to over-reliance on a small group? Understanding this concentration is critical for prioritizing retention spend and avoiding blind investment across an undifferentiated customer list.

## Dataset
https://www.kaggle.com/datasets/ulrikthygepedersen/online-retail-dataset: about 540K transactions from a UK-based online retailer, covering roughly one year. Prices are in pounds sterling.

## Method
1. **Cleaning (SQL and pandas):** converted dates, removed cancellations and negative quantities, and kept about 400K transaction rows.
2. **RFM calculation (SQL):** per customer, Recency (days since last purchase, measured from the last date in the data), Frequency (distinct invoices), and Monetary (sum of quantity times unit price).
3. **Scoring and segmentation (pandas):** quartile scores for each dimension (Frequency has three levels because many customers tie at one order), combined with rules into five segments: Best Customers, Regular, At Risk, Lost/Churned, and New/Promising.
4. **Dashboard (Tableau Public):** segment shares of customers and revenue, a segment profile table, and a log-scale scatter of orders against spend.

## Key Findings
- **Revenue is concentrated.** Best Customers are 20.2% of customers and generate 67.7% of revenue (£5.6M of £8.3M). Lost/Churned customers are 31.9% of customers and generate 4.5%.

| Segment | Customers | % of customers | % of revenue | Avg orders | Avg spend (£) | Days since last order |
|---|---|---|---|---|---|---|
| Best Customers | 884 | 20.2% | 67.7% | 15 | 6,360 | 14 |
| Regular | 1,065 | 24.4% | 16.2% | 3 | 1,259 | 60 |
| At Risk | 416 | 9.5% | 9.2% | 6 | 1,841 | 109 |
| Lost/Churned | 1,396 | 31.9% | 4.5% | 1 | 270 | 190 |
| New/Promising | 611 | 14.0% | 2.3% | 2 | 317 | 23 |

- **At Risk customers were once valuable.** They averaged 6 orders and £1,841 in spend, but their last order was about 109 days ago, compared with 14 days for Best Customers.
- **Lost/Churned customers are mostly one-time buyers** (about 1 order and £270 on average, last seen about 190 days ago).

## Recommendation
- **Protect the Best Customers.** The business depends heavily on this group, so losing even a small fraction would have an outsized revenue impact. A retention program (loyalty tiers, early access, personalized outreach) is justified.
- **Test win-back on At Risk, not Lost/Churned.** At Risk customers have a history of repeat purchases, so a low-cost win-back campaign (for example, one targeted email) is more likely to pay back. Lost/Churned customers contribute little revenue, so keep any outreach to them modest and measured.

## Data note
The segmentation table contained one row with no CustomerID (all anonymous invoices grouped together as a single fake "customer"). It was assigned to Best Customers and carried about £1.45M of spend. It is excluded from the dashboard and from the figures above. An earlier version of this analysis, which included it, reported Best Customers at 72.5% of revenue. A planned fix is to drop missing CustomerIDs in the cleaning step and rerun the segmentation.

## Limitations
- About one year of data, so seasonality and longer-term behavior are not captured.
- Segment thresholds are judgment calls, and quartile cutoffs depend on the data.
- Frequency has only three score levels because of ties.
- Segments are descriptive, not predictive. Nothing here forecasts who will buy again.
- Customers with zero or negative total spend are not shown on the log-scale scatter.

## Files
- `Retail.ipynb`: full notebook (SQL queries, Python segmentation logic)
- `rfm_results.csv`: customer-level RFM scores and segment labels
- `dashboard.png`: screenshot of the Tableau dashboard
