# Customer Segmentation using RFM Analysis

Segmenting 4,371 customers from a UK online retailer based on how recently, how often, and how much they've spent — to identify high-value customers and who's at risk of churning.

## Cleaning
- Dropped all null values from the CustomerID column, since a transaction can't be assigned in RFM if the customer isn't known. Filled "Unknown" in Description where null, since it isn't used in the RFM calculation.
- Checked duplicate records and initially suspected they were related to returns — investigation showed they were exact repeated line items (same InvoiceNo, product, quantity, and price), a data entry issue, not returns. These exact duplicates were removed.
- Cancelled orders (InvoiceNo starting with 'C') were kept rather than dropped, since their negative Quantity values naturally reduce a customer's Monetary total — giving a more accurate picture of their true net spend.
- Removed records with UnitPrice = 0, which aren't real transactions — likely promotions, samples, or giveaways that would have distorted Frequency counts.

## The Method: RFM
Every customer is scored 1-5 on Recency (days since last purchase), Frequency (number of orders), and Monetary (total spend), then grouped into segments — Champions, Loyal Customers, At Risk, Lost, and a couple in between.

## What I Found
- Champions and Lost customers together make up nearly 50% of the customer base — a healthy amount of high-value engagement, but also a large group needing win-back attention. Champions (~26%) show low Recency, high Frequency, and high Monetary value — the profile of an engaged, valuable customer. Lost customers (~24%) show the opposite across all three metrics.
- Loyal Customers hold the second-highest total Monetary value after Champions, showing this segment, while not top-tier, still contributes meaningfully to overall revenue.
- The UK drives the highest total Monetary value overall — expected, since this is a UK-based retailer. Interestingly, the Netherlands has the highest average Monetary value per transaction, backed by a real sample of 2,367 transactions, not just a few high spenders.

## Dashboard
Built an interactive Power BI dashboard to explore segments by revenue, count, and behavior.

![Dashboard](images/RFM_Segmentation_Dashboard.png)

## Project Structure
```
├── RFM_Customer_Segmentation.ipynb
├── rfm_segments.csv
├── RFM_Segmentation_Report.pbix
└── README.md
```

## Conclusion
RFM turned a raw set of transactions into a clear picture of who actually matters to the business, and who's worth a second look. A simple framework, but a genuinely useful one.
