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



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
df = pd.read_csv(r"C:\2025\BA  - 2025\Project and Workshop\BI_Coffee Sales\archive\Project.csv")
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>transaction_id</th>
      <th>transaction_date</th>
      <th>transaction_time</th>
      <th>store_id</th>
      <th>store_location</th>
      <th>product_id</th>
      <th>transaction_qty</th>
      <th>unit_price</th>
      <th>Total_Bill</th>
      <th>product_category</th>
      <th>product_type</th>
      <th>product_detail</th>
      <th>Size</th>
      <th>Month Name</th>
      <th>Day Name</th>
      <th>Hour</th>
      <th>Month</th>
      <th>Day of Week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>114301</td>
      <td>01-06-2023</td>
      <td>11:33:29</td>
      <td>3</td>
      <td>Astoria</td>
      <td>45</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>Large</td>
      <td>June</td>
      <td>Thursday</td>
      <td>11</td>
      <td>6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>115405</td>
      <td>02-06-2023</td>
      <td>11:18:24</td>
      <td>3</td>
      <td>Astoria</td>
      <td>45</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>Large</td>
      <td>June</td>
      <td>Friday</td>
      <td>11</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>115478</td>
      <td>02-06-2023</td>
      <td>12:02:45</td>
      <td>3</td>
      <td>Astoria</td>
      <td>45</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>Large</td>
      <td>June</td>
      <td>Friday</td>
      <td>12</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>116288</td>
      <td>02-06-2023</td>
      <td>19:39:47</td>
      <td>3</td>
      <td>Astoria</td>
      <td>45</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>Large</td>
      <td>June</td>
      <td>Friday</td>
      <td>19</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>116714</td>
      <td>03-06-2023</td>
      <td>12:24:57</td>
      <td>3</td>
      <td>Astoria</td>
      <td>45</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>Large</td>
      <td>June</td>
      <td>Saturday</td>
      <td>12</td>
      <td>6</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# checking for nulls
df.isnull().sum()
```




    transaction_id      0
    transaction_date    0
    transaction_time    0
    store_id            0
    store_location      0
    product_id          0
    transaction_qty     0
    unit_price          0
    Total_Bill          0
    product_category    0
    product_type        0
    product_detail      0
    Size                0
    Month Name          0
    Day Name            0
    Hour                0
    Month               0
    Day of Week         0
    dtype: int64




```python
# dropping "product_id" and "store_id"
df.drop(columns = ["store_id", "product_id"], inplace = True)
```


```python
# rename columns
df.rename(columns = {'transaction_id': 'id',
                     'transaction_date': 'date',
                     'transaction_time': 'time',
                     'transaction_qty': 'quantity',
                     'store_location': 'location',
                     'product_category': 'category',
                     'product_type': 'product',
                     'product_detail': 'detail'}, inplace = True)
```


```python
# check duplicated rows
df.duplicated().any()
```




    np.False_




```python
# Find duplicated rows based on the 'id' column
duplicates = df[df.duplicated(subset='id', keep=False)]
duplicates
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>date</th>
      <th>time</th>
      <th>location</th>
      <th>quantity</th>
      <th>unit_price</th>
      <th>Total_Bill</th>
      <th>category</th>
      <th>product</th>
      <th>detail</th>
      <th>Size</th>
      <th>Month Name</th>
      <th>Day Name</th>
      <th>Hour</th>
      <th>Month</th>
      <th>Day of Week</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# summary
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 149116 entries, 0 to 149115
    Data columns (total 16 columns):
     #   Column       Non-Null Count   Dtype  
    ---  ------       --------------   -----  
     0   id           149116 non-null  int64  
     1   date         149116 non-null  object 
     2   time         149116 non-null  object 
     3   location     149116 non-null  object 
     4   quantity     149116 non-null  int64  
     5   unit_price   149116 non-null  float64
     6   Total_Bill   149116 non-null  float64
     7   category     149116 non-null  object 
     8   product      149116 non-null  object 
     9   detail       149116 non-null  object 
     10  Size         149116 non-null  object 
     11  Month Name   149116 non-null  object 
     12  Day Name     149116 non-null  object 
     13  Hour         149116 non-null  int64  
     14  Month        149116 non-null  int64  
     15  Day of Week  149116 non-null  int64  
    dtypes: float64(2), int64(5), object(9)
    memory usage: 18.2+ MB
    


```python
# converting date to datetime
df['date'] = pd.to_datetime(df['date'], dayfirst=True)
```


```python
# sales
df['sales'] = df['quantity'] * df['unit_price']
```


```python
# extract the month as a full name
df['month'] = df['date'].dt.strftime('%B')
```


```python
# extract the day and year
df['day'] = df['date'].dt.day
df['year'] = df['date'].dt.year
```


```python
# get the weekday name
df['weekday'] = df['date'].dt.day_name()
```


```python
# extracting the hour from time
df['hour'] = pd.to_datetime(df['time'], format='%H:%M:%S').dt.hour
```


```python
# defining the time of the day
def get_time_of_day(hour):
    if hour < 12:
        return 'Morning'
    elif 12 <= hour < 18:
        return 'Afternoon'
    else:
        return 'Evening'
```


```python
df['time_of_day'] = df['hour'].apply(get_time_of_day)
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>date</th>
      <th>time</th>
      <th>location</th>
      <th>quantity</th>
      <th>unit_price</th>
      <th>Total_Bill</th>
      <th>category</th>
      <th>product</th>
      <th>detail</th>
      <th>...</th>
      <th>Hour</th>
      <th>Month</th>
      <th>Day of Week</th>
      <th>sales</th>
      <th>month</th>
      <th>day</th>
      <th>year</th>
      <th>weekday</th>
      <th>hour</th>
      <th>time_of_day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>114301</td>
      <td>2023-06-01</td>
      <td>11:33:29</td>
      <td>Astoria</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>...</td>
      <td>11</td>
      <td>6</td>
      <td>3</td>
      <td>3.0</td>
      <td>June</td>
      <td>1</td>
      <td>2023</td>
      <td>Thursday</td>
      <td>11</td>
      <td>Morning</td>
    </tr>
    <tr>
      <th>1</th>
      <td>115405</td>
      <td>2023-06-02</td>
      <td>11:18:24</td>
      <td>Astoria</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>...</td>
      <td>11</td>
      <td>6</td>
      <td>4</td>
      <td>3.0</td>
      <td>June</td>
      <td>2</td>
      <td>2023</td>
      <td>Friday</td>
      <td>11</td>
      <td>Morning</td>
    </tr>
    <tr>
      <th>2</th>
      <td>115478</td>
      <td>2023-06-02</td>
      <td>12:02:45</td>
      <td>Astoria</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>...</td>
      <td>12</td>
      <td>6</td>
      <td>4</td>
      <td>3.0</td>
      <td>June</td>
      <td>2</td>
      <td>2023</td>
      <td>Friday</td>
      <td>12</td>
      <td>Afternoon</td>
    </tr>
    <tr>
      <th>3</th>
      <td>116288</td>
      <td>2023-06-02</td>
      <td>19:39:47</td>
      <td>Astoria</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>...</td>
      <td>19</td>
      <td>6</td>
      <td>4</td>
      <td>3.0</td>
      <td>June</td>
      <td>2</td>
      <td>2023</td>
      <td>Friday</td>
      <td>19</td>
      <td>Evening</td>
    </tr>
    <tr>
      <th>4</th>
      <td>116714</td>
      <td>2023-06-03</td>
      <td>12:24:57</td>
      <td>Astoria</td>
      <td>1</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>Tea</td>
      <td>Brewed herbal tea</td>
      <td>Peppermint</td>
      <td>...</td>
      <td>12</td>
      <td>6</td>
      <td>5</td>
      <td>3.0</td>
      <td>June</td>
      <td>3</td>
      <td>2023</td>
      <td>Saturday</td>
      <td>12</td>
      <td>Afternoon</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>




```python
df.to_csv('cleaned_coffee_sales_dataset.csv')
```

## EDA & Metrics


```python
palette = sns.set_palette(sns.color_palette("RdBu"))
```

### 0.1 Total Revenue


```python
total_revenue = df['sales'].sum()
(f'Total Revenue: ${total_revenue:,.2f}')
```




    'Total Revenue: $698,812.33'



### 0.2 Total Orders


```python
total_orders = df['id'].nunique()
(f'Total Order: {total_orders:,.2f}')
```




    'Total Order: 149,116.00'



### 0.3 Average Order Value (AOV)


```python
aov = total_revenue/total_orders
(f'Average Order Value (AOV): {aov:,.2f}')
```




    'Average Order Value (AOV): 4.69'



### 0.4 Peak Sales Location & Revenue


```python
peak_sales_location = df.groupby('location')['sales'].sum().idxmax()
(f'Peak Sales Location: {peak_sales_location}')
```




    "Peak Sales Location: Hell's Kitchen"




```python
peak_sales_location_revenue = df.groupby('location')['sales'].sum().max()
(f'Peak Sales Location: ${peak_sales_location_revenue:,.2f}')
```




    'Peak Sales Location: $236,511.17'



### 0.5 Sales by Month


```python
# Sum of sales for each month
revenue = df.groupby('month')['sales'].sum().reset_index()
revenue
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>month</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>April</td>
      <td>118941.08</td>
    </tr>
    <tr>
      <th>1</th>
      <td>February</td>
      <td>76145.19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>January</td>
      <td>81677.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>June</td>
      <td>166485.88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>March</td>
      <td>98834.68</td>
    </tr>
    <tr>
      <th>5</th>
      <td>May</td>
      <td>156727.76</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(10, 8))
month_order = ['January', 'February', 'March', 'April', 'May', 'June']
sns.barplot(data = revenue, x = 'month', y = 'sales', hue = 'month', order = month_order, errorbar = None)
plt.title('Sales by Month', fontsize = 18)
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()
```


    
![png](https://i.imgur.com/Q0eA4tg.png)
    


### 0.6 Sales by Location


```python
# Sum of sales for each location
location_revenue = df.groupby('location')['sales'].sum().reset_index()
location_revenue
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>location</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Astoria</td>
      <td>232243.91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hell's Kitchen</td>
      <td>236511.17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lower Manhattan</td>
      <td>230057.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(10, 8))
sns.barplot(data = location_revenue, x = 'location', y = 'sales', hue = 'location', errorbar = None)
plt.title('Sales by Location', fontsize = 18)
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()
```


    
![png](https://i.imgur.com/5rNv8Nw.png)
    


### 0.7 Top 10 Popular Product by Revenue


```python
product_revenue = df.groupby('product')['sales'].sum().reset_index()
product_revenue
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Barista Espresso</td>
      <td>91406.20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Biscotti</td>
      <td>19793.53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Black tea</td>
      <td>2711.85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Brewed Black tea</td>
      <td>47932.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brewed Chai tea</td>
      <td>77081.95</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Brewed Green tea</td>
      <td>23852.50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Brewed herbal tea</td>
      <td>47539.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chai tea</td>
      <td>4301.25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Clothing</td>
      <td>6163.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Drinking Chocolate</td>
      <td>2728.04</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Drip coffee</td>
      <td>31984.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Espresso Beans</td>
      <td>5560.25</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Gourmet Beans</td>
      <td>6798.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Gourmet brewed coffee</td>
      <td>70034.60</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Green beans</td>
      <td>1340.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Green tea</td>
      <td>1470.75</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Herbal tea</td>
      <td>2729.75</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Hot chocolate</td>
      <td>72416.00</td>
    </tr>
    <tr>
      <th>18</th>
      <td>House blend Beans</td>
      <td>3294.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Housewares</td>
      <td>7444.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Organic Beans</td>
      <td>8509.50</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Organic Chocolate</td>
      <td>1679.60</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Organic brewed coffee</td>
      <td>37746.50</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Pastry</td>
      <td>25655.99</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Premium Beans</td>
      <td>14583.50</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Premium brewed coffee</td>
      <td>38781.15</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Regular syrup</td>
      <td>6084.80</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Scone</td>
      <td>36866.12</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sugar free syrup</td>
      <td>2324.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (10, 8))
ax = sns.barplot(x = 'product', y = 'sales', hue='product', palette='RdBu', data = product_revenue.sort_values('sales', ascending = False)[0:10])
# x-axis rotation
plt.xticks(rotation=90)
plt.title('Top 10 Popular Products by Revenue', fontsize = 18)
plt.xlabel('Products')
plt.ylabel('Sales')
plt.show()
```


    
![png](https://i.imgur.com/wO2vAqU.png)
    


### 0.8 Average Order Value (AOV) by Product Category


```python
category_aov = df.groupby('category')['sales'].mean().reset_index()
category_aov
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>category</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bakery</td>
      <td>3.610969</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Branded</td>
      <td>18.215529</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Coffee</td>
      <td>4.621207</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Coffee beans</td>
      <td>22.866657</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Drinking Chocolate</td>
      <td>6.314615</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Flavours</td>
      <td>1.238409</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Loose Tea</td>
      <td>9.267438</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Packaged Chocolate</td>
      <td>9.050595</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Tea</td>
      <td>4.321458</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (10, 8))
sns.barplot(x = 'sales', y = 'category', hue = 'category', palette='RdBu', data = category_aov.sort_values('sales', ascending = False))
plt.title('Average Order Value by Category', fontsize = 18)
plt.xlabel('Sales')
plt.ylabel('Category')
plt.show()
```


    
![png](https://i.imgur.com/5evyRCD.png)
    


### 0.9 Popular Category


```python
# count of category
category_count = df['category'].value_counts().reset_index()
category_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>category</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Coffee</td>
      <td>58416</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tea</td>
      <td>45449</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bakery</td>
      <td>22796</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Drinking Chocolate</td>
      <td>11468</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Flavours</td>
      <td>6790</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Coffee beans</td>
      <td>1753</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Loose Tea</td>
      <td>1210</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Branded</td>
      <td>747</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Packaged Chocolate</td>
      <td>487</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (10, 8))
sns.barplot(data = category_count, x = 'count', y = 'category', hue = 'category', palette='RdBu')
plt.title('Popular Category', fontsize = 18)
plt.xlabel('Count of Category')
plt.ylabel('Category')
plt.show()
```


    
![png](https://i.imgur.com/8Cy9HUl.png)
    


### 0.10 Peak Hour


```python
order_per_hour = df.groupby('hour')['id'].count().reset_index()
order_per_hour
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hour</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>4594</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>13428</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>17654</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>17764</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>18545</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>9766</td>
    </tr>
    <tr>
      <th>6</th>
      <td>12</td>
      <td>8708</td>
    </tr>
    <tr>
      <th>7</th>
      <td>13</td>
      <td>8714</td>
    </tr>
    <tr>
      <th>8</th>
      <td>14</td>
      <td>8933</td>
    </tr>
    <tr>
      <th>9</th>
      <td>15</td>
      <td>8979</td>
    </tr>
    <tr>
      <th>10</th>
      <td>16</td>
      <td>9093</td>
    </tr>
    <tr>
      <th>11</th>
      <td>17</td>
      <td>8745</td>
    </tr>
    <tr>
      <th>12</th>
      <td>18</td>
      <td>7498</td>
    </tr>
    <tr>
      <th>13</th>
      <td>19</td>
      <td>6092</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20</td>
      <td>603</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename columns
order_per_hour.rename(columns = {'id':'count_of_orders'}, inplace = True)
```


```python
plt.figure(figsize = (10, 8))
sns.lineplot(x = 'hour', y = 'count_of_orders', data = order_per_hour, marker='o')
plt.xlabel('Hour')
plt.ylabel('Count of Orders')
plt.title('Peak Hour', fontsize = 18)
# Set the x-axis limits to the min and max values of 'hour'
plt.xticks(range(order_per_hour['hour'].min(), order_per_hour['hour'].max() + 1))
plt.show()
```


    
![png](https://i.imgur.com/qa3FzLg.png)
    


### 0.11 Peak Day


```python
plt.figure(figsize = (10, 8))
weekdays_order = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
ax = sns.countplot(x = 'weekday', data = df, hue = 'weekday', palette='RdBu', order = weekdays_order)

# Add count values inside the bars
for p in ax.patches:
    ax.annotate(f'{p.get_height()}', 
                (p.get_x() + p.get_width() / 2., p.get_height()),   # x and y position of the text
                ha = 'center', va = 'center', 
                xytext = (0, 7), textcoords='offset points')  

plt.xlabel('Weekday')
plt.ylabel('Count of Orders')
plt.title('Peak Day', fontsize = 18)
plt.show()
```


    
![png](https://i.imgur.com/QomPLQI.png)
    


### 0.12 Distribution of orders across different coffee types


```python
coffee_type = df[df['category'] == 'Coffee'][['product']]
coffee_type
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Gourmet brewed coffee</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Drip coffee</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Drip coffee</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Gourmet brewed coffee</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Barista Espresso</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>149103</th>
      <td>Organic brewed coffee</td>
    </tr>
    <tr>
      <th>149104</th>
      <td>Premium brewed coffee</td>
    </tr>
    <tr>
      <th>149105</th>
      <td>Drip coffee</td>
    </tr>
    <tr>
      <th>149106</th>
      <td>Gourmet brewed coffee</td>
    </tr>
    <tr>
      <th>149114</th>
      <td>Barista Espresso</td>
    </tr>
  </tbody>
</table>
<p>58416 rows × 1 columns</p>
</div>




```python
coffee_type_count = coffee_type['product'].value_counts().reset_index()
coffee_type_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Gourmet brewed coffee</td>
      <td>16912</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Barista Espresso</td>
      <td>16403</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Organic brewed coffee</td>
      <td>8489</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Drip coffee</td>
      <td>8477</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Premium brewed coffee</td>
      <td>8135</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (10, 8))
sns.barplot(data = coffee_type_count, x = 'count', y = 'product', hue = 'product' )
plt.title('Order Distribution by Coffee Type', fontsize = 18)
plt.xlabel('Count of Orders')
plt.ylabel('Coffee Types')
plt.show()
```


    
![png](https://i.imgur.com/X9R80pt.png)
    



```python

```
