# Coffee_Shop_Sales_Analysis
The data source can be found on kaggle website at [this link](https://www.kaggle.com/datasets/divu2001/coffee-shop-sales-analysis/data/). The main objective of this project is to evaluate the sales of three coffee shop locations using Power BI.

[Preview_Dashboard](https://github.com/David-Tu-Nguyen/Power-BI-Projects/blob/main/Coffee-Shop-Sales-Analysis/Coffee%20Sales%20Dashboard%20DB.pdf)

## Main objective

- **Revenue Analysis:** Calculate total sales,...
- **Visitor Trends:** Identify peak hours.
- **Store Performance:** Compare sales performance across store locations.
- **Product Insights:** Identify top-selling items.
- **Category Contribution:** Analyze category-wise sales distribution and contributions to total revenue.
- **Visualize Trends:** Enable visualization-ready data for further exploration.

The questions we will answer through this analysis are the following :
- What is the number of orders?
- Which store location has the highest sales?
- What are the best-selling product types?
- What is the trend of total sales over the months covered in the data?
- What are the peak hours for sales?
- How do sales vary across days of the week?
- Are there any notable correlations between unit price and?
...

## Data dictionary
- Number of Rows: 149116
- Number of Columns: 18
  
Column Name | Data Type | Description
| ------------- |:-------------:| :-------------:|
Transaction_ID | Integer | Unique identifier for each transaction.
Transaction_Date | DateTime | Date and time when the transaction occurred.
Product_Name | Varchar | Name of the product sold (e.g., Espresso, Latte).
Product_Category | Varchar | Category of the product (e.g., Hot Beverage, Cold Beverage, Pastry).
Quantity_Sold | Integer | Number of units sold in the transaction.
Unit_Price | Float | Price per unit of the product.
Total_Sales | Float | Total revenue from the transaction (Quantity_Sold × Unit_Price).
Payment_Method | Varchar | Mode of payment used (e.g., Cash, Credit Card, Mobile Payment).
Customer_Age_Group | Varchar | Age group of the customer (e.g., 18-24, 25-34).
Customer_Gender | Varchar | Gender of the customer (e.g., Male, Female).
Store_Location | Varchar | Location of the store where the transaction took place.
Day_of_Week | Varchar | Day of the week when the transaction occurred (e.g., Monday, Tuesday).
Time_of_Day | Varchar | Time period of the day (e.g., Morning, Afternoon, Evening).
Season | Varchar | Season during which the transaction occurred (e.g., Winter, Summer).

## Methodology and tools used
Tables
| Step  | Used Tools |
| ------------- |:-------------:|
|First Exploratory Data Analysis & Joining Tables     |     |
|Data Cleaning, Advanced Exploratory Data Analysis & First Visualizations  | Python |
|Advanced Data Visualizations & Dashboard    |      |
