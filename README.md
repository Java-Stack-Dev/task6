# Task 6 – Sales Trend Analysis Using Aggregations

## Objective
Analyze monthly revenue and order volume from an online sales dataset using SQL queries and aggregation functions.

## Dataset Description

The dataset consists of a table named `Transactions` with the following columns:

- `Transaction_ID` – Unique ID for each transaction
- `order_date` – Date of purchase
- `Product_Category` – Category of the product sold
- `Product_Name` – Name of the product
- `Units_Sold` – Number of units sold
- `Unit_Price` – Price per unit
- `Total_Revenue` – Total revenue from the transaction
- `Region` – Sales region
- `Payment_Method` – Mode of payment

## Tools Used
- Oracle SQL / SQL*Plus
- PostgreSQL 
- GitHub

---

## Task Performed

1. **Created a table** `Transactions` and inserted data into it.

  ```CREATE TABLE Transactions (
    Transaction_ID INT PRIMARY KEY,
    order_date DATE,
    Product_Category VARCHAR(100),
    Product_Name VARCHAR(100),
    Units_Sold INT,
    Unit_Price DECIMAL(10, 2),
    Total_Revenue DECIMAL(10, 2),
    Region VARCHAR(100),
    Payment_Method VARCHAR(100)```
);
2. Wrote SQL query to:
   - Extract year and month from `order_date`
   - Calculate `SUM(Total_Revenue)` as `monthly_revenue`
   - Count unique `Transaction_ID`s for `monthly_order_volume`
   - Group results by year and month
   - Sort the output in descending order of year and month


## SQL Query Used

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS order_year,
    EXTRACT(MONTH FROM order_date) AS order_month,
    SUM(Total_Revenue) AS monthly_revenue,
    COUNT(DISTINCT Transaction_ID) AS monthly_order_volume
FROM
    Transactions
GROUP BY
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY
    order_year DESC,
    order_month DESC;


SELECT * FROM (
        SELECT
           EXTRACT(YEAR FROM order_date) AS order_year,
            EXTRACT(MONTH FROM order_date) AS order_month,
            SUM(Total_Revenue) AS monthly_revenue
      FROM
           Transactions
       GROUP BY
            EXTRACT(YEAR FROM order_date), EXTRACT(MONTH FROM order_date)
       ORDER BY
           monthly_revenue DESC
  )
  WHERE ROWNUM <= 3;



