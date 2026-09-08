# retail-customer-segmentation-rfm

A customer segmentation analysis of ~4,000 customers from a UK-based 
online retailer, using RFM (Recency, Frequency, Monetary) methodology 
to identify revenue concentration and inform retention strategy.

## Tools Used
- SQL (SQLite) — data cleaning, transaction-level querying
- Python (pandas) — RFM scoring, customer segmentation logic
- Google Sheets — pivot tables and visualization

## Business Problem
This project analyzes ~4,000 customers from a UK-based online retailer using RFM (Recency, Frequency, Monetary) segmentation to identify which customers drive revenue and where the business faces risk from over-reliance on a small customer base. Understanding this concentration is critical for prioritizing retention spend and avoiding blind investment across an undifferentiated customer list.

## Method
Using SQL (SQLite), I cleaned and queried ~400K raw transaction records, calculating Recency, Frequency, and Monetary values for each customer. In Python (pandas), I applied quartile-based scoring to each dimension and classified customers into five segments: Best Customers, At Risk, Lost/Churned, New/Promising, and Regular. I then aggregated revenue and customer counts by segment to quantify the business impact of each group.

## Key Findings & Recommendation
The analysis reveals significant revenue concentration: Best Customers make up only 20.2% of the customer base but generate 72.5% of total revenue, while Lost/Churned customers represent 31.9% of the base but contribute just 3.9% of revenue. This concentration means the business's financial health is highly dependent on retaining a relatively small group of high-value customers. I'd recommend prioritizing a dedicated retention program (loyalty tiers, early product access, personalized outreach) for the Best Customers segment, since losing even a small fraction of this group would have an outsized revenue impact. Separately, given the low revenue contribution from Lost/Churned customers, re-engagement spend should be modest and tightly measured (e.g., a single low-cost win-back email campaign) rather than a major investment, since the data suggests limited return from reactivating this group at scale.

## Files
- `rfm_analysis.ipynb` — full notebook (SQL queries, Python segmentation logic)
- `rfm_results.csv` — final customer-level RFM scores and segment labels
