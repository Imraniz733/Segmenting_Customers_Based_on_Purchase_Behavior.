# Segmenting_Customers_Based_on_Purchase_Behavior.

## Table of Contents
- [Introduction](#Introduction)
- [Data Description](#Data-Description)
- [Data Cleaning And Processing](#Data_Clening_And_Processing)
- [Exploratory Data Analysis(EDA)](#Exploratory_Data_Analysis)
- [Insights And Recommendations](#Insights_And_Recommendations) 

## Introduction
In the modern retail industry, understanding customer behavior is crucial for tailoring personalized marketing strategies and improving overall customer experience. This project uses purchase behavior data from an online retail platform to focus on customer segmentation. By segmenting customers based on their purchasing patterns, we aim to uncover valuable insights that can inform targeted marketing campaigns, promotions, and product recommendations.

## Data Description
The dataset used in this project contains records of customer transactions from an online retail platform. The data includes details on individual customer purchases, which allows us to analyze and segment customers based on their purchase behavior. Below is a description of the key columns in the dataset:

**Columns**
**CustomerID:** A unique identifier for each customer. This is used to track individual customers across transactions.

**InvoiceNo:** A unique identifier for each transaction or order. This allows us to track multiple items purchased in a single transaction.

**StockCode:** A unique code is assigned to each product purchased. This column helps identify the specific products purchased by customers.

**Description:** The name or description of the product. This column provides information about the items that customers are purchasing.

**Quantity:** The quantity of each product purchased. This helps determine the volume of products customers are buying.

**InvoiceDate:** The date and time when the transaction took place. This column is useful for calculating Recency and identifying the frequency of customer purchases.

**UnitPrice:** The price per unit of the product. This helps calculate the Monetary value by multiplying this column by the quantity purchased.

**Country:** The customer's country. This is useful if analyzing purchasing behavior across regions.

## Data Cleaning And Processing
- The dataset contains missing values in the CustomerID column for 135,080 rows, accounting for approximately 25% of the total dataset. Additionally, 1,454 rows have missing values in the Description column. To address this, we flagged the CustomerID column using a new indicator, CustomerID_flag, where 1 represents present IDs and 0 represents missing IDs. Missing CustomerID values were replaced with "Unknown". For the Description column, the 1,454 rows with missing values also had zero values for CustomerID, Quantity, and UnitPrice. Consequently, these rows were removed from the dataset.
-  Upon checking for duplicate entries, we identified 5,268 duplicate records. However, upon further investigation, we observed that these records shared the same InvoiceNo, InvoiceDate, CustomerID, and Country, indicating that multiple items were purchased simultaneously at the same location. The apparent duplication is due to variations in the Description and Quantity fields, representing different items within the same transaction. To validate this observation, we downloaded the duplicate entries dataset and reviewed it in a CSV file.
- There are instances of negative quantities in the dataset, which represent discounts, damaged goods, stock loss, and item returns. We have flagged these entries and retained them as they are, since the negative quantities are necessary for accurately calculating TotalPrice, where they appropriately reduce the total count. 
- The dataset contains a total of 1,061 records with zero values in the UnitPrice column. To address this, we examined the Description and StockCode of the products and applied an imputation technique by taking the average UnitPrice of similar non-missing entries. Additionally, we identified two entries with the largest negative Quantity of -11,062, labeled as "bad debt" in the Description field. These entries were considered outliers and were subsequently removed from the dataset. 

## Exploratory Data Analysis
**1. Top 10 Products by Revenue:** 
We have listed the top 10 products by total revenue, where Dotcom Postage shows the highest revenue of 206,828.93, while Chilli Lights records the lowest revenue among the top products at 53,788.38.

**2. Top 10 Products by Quantity:** 
We have listed the top 10 products by Quantity, where world war 2 gliders asstd designs shows the highest quantity of 53847, while pack of 60 pink paisley cake cases records the lowest quantity among the top products at 24573.

**3. Sales by Country:**
| Country               | Total Sales (in USD) |
|-----------------------|----------------------|
| United Kingdom        | 7,802,160.84         |
| Netherlands           | 285,557.43           |
| Eire                  | 264,114.80           |
| Germany               | 222,086.18           |
| France                | 197,783.45           |
| Australia             | 138,208.68           |
| Switzerland           | 56,394.24            |
| Spain                 | 54,829.69            |
| Belgium               | 40,910.96            |
| Sweden                | 36,595.91            |
| Japan                 | 35,340.62            |
| Norway                | 35,184.77            |
| Portugal             | 29,367.02            |
| Finland               | 22,326.74            |
| Channel Islands       | 20,086.29            |
| Denmark               | 18,768.14            |
| Italy                 | 16,890.51            |
| Cyprus                | 12,946.29            |
| Austria               | 10,154.32            |
| Hong Kong             | 10,117.04            |
| Singapore             | 9,120.39             |
| Israel                | 7,907.82             |
| Poland                | 7,213.14             |
| Unspecified           | 4,749.79             |
| Greece                | 4,710.52             |
| Iceland               | 4,310.00             |
| Canada                | 3,666.38             |
| Malta                 | 2,505.47             |
| United Arab Emirates  | 1,902.28             |
| USA                   | 1,730.92             |
| Lebanon               | 1,693.88             |
| Lithuania             | 1,661.06             |
| RSA                   | 1,381.86             |
| European Community    | 1,291.75             |
| Brazil                | 1,143.60             |
| Czech Republic        | 707.72               |
| Bahrain               | 548.40               |
| Saudi Arabia          | 131.17               |


**4. Sales Over Time:**

Sales Growth:
- From January (1, 2011) to November (11, 2011), there is a general upward trend in sales with fluctuations.
The sales start around 0.5 million in January and gradually increase, peaking in November at approximately 1.4 million.
- Fluctuations: There are noticeable fluctuations during the year. For example, after an initial increase from January to March, sales dip in April and then recover in subsequent months.
This indicates some seasonal variability in sales, possibly influenced by external factors such as demand, promotions, or holidays.
- Peak Sales in November: The highest sales occur in November 2011, reaching approximately 1.4 million. This could be attributed to:
- End-of-year promotions. Holiday season sales (e.g., Black Friday, Christmas preparations).
Sharp Decline in December: After peaking in November, sales experience a sharp decline in December, dropping back to around 0.5 million.

-This drop could be due to:
* Post-holiday season slowdown.
* Reduced demand after a period of high sales activity.
* Inventory depletion or fewer promotions.

**5. RFM Analysis:** 
RFM analysis was performed separately for customers and guest transactions. The following steps were followed:
- Recency: Calculated as the number of days since the last transaction.
- Frequency: Counted the number of unique invoices per customer.
- Monetary: Summed up the total transaction value for each customer.
- Assigned R, F, and M scores using quintiles and combined them to create an overall RFM score.
- Segmented customers into categories like:
- Champions (RFM Score >= 12)
- Loyal (RFM Score 9–11)
- Potential Loyalist (RFM Score 6–8)
- At Risk (RFM Score < 6)

## Customer Segment Distribution
The customers were segmented based on their RFM (Recency, Frequency, and Monetary) scores into four categories: **Champions**, **Potential Loyalists**, **Loyal**, and **At Risk**.

- **Champions**: 1278  
- **Potential Loyalists**: 1202  
- **Loyal**: 1006  
- **At Risk**: 886

## RFM Table for Customers

| **CustomerID** | **Recency** | **Frequency** | **Monetary** | **R** | **F** | **M** | **RFM_Score** | **Segment**  | **Type**     |
|----------------|-------------|---------------|--------------|-------|-------|-------|---------------|--------------|-------------|
| 12346.0        | 326         | 2             | 0.00         | 1     | 2     | 1     | 4             | At Risk      | Customers   |
| 12347.0        | 2           | 7             | 4310.00      | 5     | 4     | 5     | 14            | Champions    | Customers   |
| 12348.0        | 75          | 4             | 1797.24      | 2     | 3     | 4     | 9             | Loyal        | Customers   |
| 12349.0        | 19          | 1             | 1757.55      | 4     | 1     | 4     | 9             | Loyal        | Customers   |
| 12350.0        | 310         | 1             | 334.40       | 1     | 1     | 2     | 4             | At Risk      | Customers   |

---
## Guest Segments Distribution

The same segmentation was applied to guest transactions, resulting in the following distribution:

- **Loyal**: 869  
- **Potential Loyalists**: 686  
- **Champions**: 399  
- **At Risk**: 299  

## RFM Table for Guest Transactions

| **InvoiceNo**  | **Recency** | **Frequency** | **Monetary** | **R** | **F** | **M** | **RFM_Score** | **Segment**            | **Type**    |
|----------------|-------------|---------------|--------------|-------|-------|-------|---------------|------------------------|-------------|
| 536544         | 373         | 527           | 5521.14      | 1     | 5     | 5     | 11            | Loyal                  | Guest       |
| 536555         | 373         | 2             | 2.97         | 1     | 3     | 2     | 6             | Potential Loyalist     | Guest       |
| 536558         | 373         | 1             | 99.75        | 1     | 1     | 3     | 5             | At Risk                | Guest       |
| 536565         | 373         | 2             | 6.70         | 1     | 3     | 2     | 6             | Potential Loyalist     | Guest       |
| 536592         | 373         | 592           | 6915.65      | 1     | 5     | 5     | 11            | Loyal                  | Guest       |

---

**6. Top 10 Customers by Monetary Value:**
| **CustomerID** | **Monetary**       |
|----------------|--------------------:|
| 14646.0        | 280,384.905443     |
| 18102.0        | 256,438.490000     |
| 17450.0        | 187,482.170000     |
| 14911.0        | 133,276.032065     |
| 12415.0        | 124,825.082975     |
| 14156.0        | 113,384.140000     |
| 17511.0        | 88,125.380000      |
| 16684.0        | 65,892.080000      |
| 13694.0        | 62,653.100000      |
| 15311.0        | 59,419.340000      |

## Insights
1. The highest-spending customer contributed 280,385 in monetary value, with significant contributions from the top 10 customers.
2. The Champions segment has the highest number of customers (1278), followed by Potential Loyalists (1202).
3. Many high-value transactions are from guest users, indicating potential for conversion into loyal customers.

## Recommendations
1. Focus on re-engaging At Risk customers through personalized offers and loyalty programs.
2. Encourage guest users to create accounts by offering signup bonuses and exclusive deals.
3. Nurture Potential Loyalists with targeted campaigns to boost spending and convert them into Champions.






