# MABB-CLOTHING-COMPREHENSIVE SALES ANALYSIS

## Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data cleaning/preparation](#data-cleaning/-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results/-findings)
- [Recommendations](#recommendation)
- [Limitation](#limitation)
# Project Overview
A comprehensive analysis for a Global Clothing e-commerce company called MABB-Closing
looking at trends over the previous 4 years from 2019 to 2023 against the current year 2024
This analysis looks at the performance across sales, inventory and products alongside customer behaviour and website performance. 

# Data Source
'bigquery-public-data.thelook_ecommerce'

# Tools Used
- SQL was used to extract and join data sets [Download here](https://docs.google.com/document/d/1M6T3FmZ2ejxhKbyqnsGrMZkcTLUwXdby/edit?usp=drive_link&ouid=103341485764477469819&rtpof=true&sd=true)
- Python was used for data cleaning.[Download here](https://drive.google.com/file/d/1sSXPuhBpzFo4CFNGuLEoHneGdtniMLB4/view?usp=drive_link)
- All data visualisations were created on Tableau.[Download here](https://drive.google.com/file/d/10wdG-EhZP4AsPnCEoqr97Gy_ijC62Gco/view?usp=drive_link)

# Data cleaning/preparation
In the innitial data preparation phase, the following tasks were performed:
1. Data Loading and inspection.
2. Handeling missing value.
3. Data cleaning and formatting.

# Exploratory Data Analysis 
- What is the most misited parts of the website?
- Where the website traffic is coming from?
- What-if analysis.
- What are the sales performance?
- what are the product performance?
- What is the Demographic composition?
- What is the inventory status?

# Data Analysis 
```sql
SELECT 
    DISTINCT(users.id),
    CONCAT(users.first_name, ' ', users.last_name) AS full_name,
    users.gender,
    users.state,
    users.postal_code,
    users.city,
    users.country,
    users.age,
    orders.order_id,
    inventory_items.product_name,
    products.id AS product_id,
    products.brand,
    orders.num_of_item,
    products.cost,
    order_items.sale_price,
    products.retail_price,
    inventory_items.product_category,
    order_items.created_at,
    orders.status
  
FROM 
    `bigquery-public-data.thelook_ecommerce.users` as users
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.orders` as orders 
ON 
    users.id = orders.user_id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.order_items` as order_items
ON 
    orders.order_id = order_items.order_id
LEFT JOIN 
    `bigquery-public-data.thelook_ecommerce.products` as products
ON 
    order_items.product_id = products.id

LEFT JOIN
    `bigquery-public-data.thelook_ecommerce.inventory_items` as inventory_items
ON
    products.id = inventory_items.product_id
WHERE orders.status IN ('Complete', 'Shipped');
```


# Results/Findings
The Analysis are summarised as follows:
1. Traffic source was from Emails.
2. The Most Visited Website was Products.
3. Most purchases was done by China.
4. The problematic Distribution centers were Los Angelis CA and Charleston SC.

# Recommendations
- Segment Your Audience.Use your email platform to categorize users into specific groups (e.g., new subscribers, loyal customers, abandoned cart users). Send tailored messages to each segment.
- Focus on stocking Distribution centers Los Angelis CA and Charles SC.
- focus on expanding and promoting products category A.
- Implement a customer segmentation strategy to target high customers effectively.

# Limitation
Null Values had to be removed and be replaced with zeros because they would have affected the accuracy of the conclution of the anlysis.



