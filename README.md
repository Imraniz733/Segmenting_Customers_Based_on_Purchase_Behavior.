# Segmenting_Customers_Based_on_Purchase_Behavior.

## Table of Contents
- [Introduction](#Introduction)
- [Data Description](#Data-Description)
- [Data Cleaning And Processing](#Data_Clening_And_Processing)
- [Exploratory Data Analysis(EDA)](#Exploratory_Data_Analysis)

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
