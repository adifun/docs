Total number of rows in `processor_transactions`: 378142

## processor_transactions with Diverse Values

| Column Name | Sample Value | Distribution |
|-------------|--------------|--------------|
| ID | 190121853 | 378142 unique values |
| MERCHANT_ID | 280772 | 123 unique values |
| CARD_TOKEN | 543459u2mIzF8476 | 298603 unique values |
| CC_LAST_FOUR | 8476 | 10000 unique values |
| TOTAL_AMOUNT | 99.86 | 12885 unique values |
| SETTLED_AT | 2023-02-15T17:45:00Z | 45733 unique values |
| CREATED_AT | 2023-02-18T09:39:18.464Z | 371674 unique values |
| UPDATED_AT | 2023-02-18T09:39:18.464Z | 371674 unique values |

## processor_transactions for Non-Diverse or Empty Columns

| Column Name | Sample Value | Note |
|-------------|--------------|------|
| CURRENCY_CODE | USD | All values are the same |



---------------------------------------------------
Total number of rows in `customer_retention`: 123

## customer_retention with Diverse Values

| Column Name | Sample Value | Distribution |
|-------------|--------------|--------------|
| 2023-01_total_customers | 141.0 | 85 unique values |
| 2023-01_new_customers | 141.0 | 85 unique values |
| 2023-01_total_revenue | 4811.2300000000005 | 122 unique values |
| 2023-02_total_customers | 1106.0 | 117 unique values |
| 2023-02_new_customers | 1079.0 | 116 unique values |
| 2023-02_returning_customers | 27.0 | 43 unique values |
| 2023-02_retention_rate_percentage | 2.4412296564195297 | 118 unique values |
| 2023-02_total_revenue | 39083.310000000005 | 122 unique values |
| 2023-02_returning_customer_revenue | 1198.4899999999998 | 122 unique values |
| 2023-03_total_customers | 1195.0 | 113 unique values |
| 2023-03_new_customers | 1045.0 | 115 unique values |
| 2023-03_returning_customers | 150.0 | 91 unique values |
| 2023-03_retention_rate_percentage | 12.552301255230125 | 119 unique values |
| 2023-03_median_order_frequency | 1.0 | 2 unique values |
| 2023-03_total_revenue | 37731.52 | 120 unique values |
| 2023-03_returning_customer_revenue | 4959.19 | 119 unique values |

## customer_retention for Non-Diverse or Empty Columns

| Column Name | Sample Value | Note |
|-------------|--------------|------|
| 2023-01_returning_customers | 0.0 | All values are the same |
| 2023-01_retention_rate_percentage | 0.0 | All values are the same |
| 2023-01_median_order_frequency | 1.0 | All values are the same |
| 2023-01_returning_customer_revenue | 0.0 | All values are the same |
| 2023-02_median_order_frequency | 1.0 | All values are the same |



# Customer Retention and Revenue Analysis Documentation

## Methodology

### Time-Based Grouping of Transactions
Transactions are grouped by specific time intervals, allowing for analysis over defined periods. This step is crucial for tracking customer engagement and revenue trends.

```python
df['TIME_PERIOD'] = df['SETTLED_AT'].dt.strftime('%Y-%m')  # For monthly grouping
```

### Customer Retention Metrics Calculation
Metrics such as the total number of customers, new customers, and returning customers are calculated for each time period. These figures shed light on customer acquisition and retention efforts.

```python
new_customers = period_customers - seen_customers
returning_customers = period_customers & seen_customers
```

### Revenue Analysis
Analysis includes total revenue and the revenue from returning customers, highlighting the value of customer loyalty.

```python
total_revenue = period_data['TOTAL_AMOUNT'].sum()
returning_customer_revenue = period_data[period_data['CARD_TOKEN'].isin(returning_customers)]['TOTAL_AMOUNT'].sum()
```

### Merchant-Specific Insights
The analysis is further refined by merchant, offering insights into customer retention and revenue at a granular level. This approach facilitates targeted strategic decisions.

```python
final_df = pd.concat([final_df, sample_df], ignore_index=False, sort=False)
```

## Key Considerations

### Data Integrity
Accurate and comprehensive data is critical for reliable insights. Data quality directly influences the interpretation of customer behaviors and revenue trends.

### Unique Customer Identification
The methodology assumes each `CARD_TOKEN` uniquely identifies a customer. This assumption may not account for shared payment methods or customers using multiple payment methods.

### External Influences
Customer behavior and revenue performance are influenced by external market and seasonal trends. Recognizing these factors is essential for accurate analysis.
