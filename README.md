# 🛒 Blinkit Grocery Sales Analysis (Power BI & SQL)
![Power BI](https://img.shields.io/badge/Tool-PowerBI-yellow)
![SQL](https://img.shields.io/badge/Database-SQL-blue)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview
This project focuses on analyzing Blinkit's sales performance, customer satisfaction, and inventory distribution to uncover meaningful insights and optimization opportunities. The analysis is built using **SQL for data preparation** and **Power BI for visualization**.

The dashboard provides a clear view of key business metrics and trends across products, outlets, fat content categories, and locations.

---

## 🎯 Business Objective
To conduct a comprehensive analysis of Blinkit's sales performance, customer satisfaction, and inventory distribution in order to identify key insights and opportunities for optimization using various KPIs and visualizations in Power BI.

---

## 📊 Key KPIs
- Total Sales  
- Average Sales  
- Number of Items Sold  
- Average Rating  

---

## 📋 Granular Requirements
- Total Sales by Fat Content  
- Total Sales by Item Type  
- Fat Content by Outlet for Total Sales  
- Total Sales by Outlet Establishment Year  
- Percentage of Sales by Outlet Size  
- Sales by Outlet Location  
- All Metrics by Outlet Type  

---

## 🗂 Dataset

**Source File:**  
BlinkIT Grocery Data.csv  

**Contains Information About:**
- Items  
- Fat Content  
- Item Type  
- Outlet Size, Type, Location  
- Ratings  
- Sales  

---

## 🧹 Data Cleaning (SQL)

Standardizing `Item_Fat_Content` to remove inconsistencies such as **LF**, **low fat**, and **reg**.

```sql
UPDATE blinkit_data
SET Item_Fat_Content =
    CASE
        WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
        WHEN Item_Fat_Content = 'reg' THEN 'Regular'
        ELSE Item_Fat_Content
    END;
```

## ✅ Check Results

```sql
SELECT DISTINCT Item_Fat_Content
FROM blinkit_data;
```
## 📈 KPI SQL Queries
### 🔹 Total Sales
```sql
SELECT CAST(SUM(Total_Sales) / 1000000.0 AS DECIMAL(10,2)) AS Total_Sales_Million
FROM blinkit_data;
```
### 🔹 Average Sales
```sql
SELECT CAST(AVG(Total_Sales) AS INT) AS Avg_Sales
FROM blinkit_data;
```

### 🔹 Number of Items
```sql
SELECT COUNT(*) AS No_of_Orders
FROM blinkit_data;
```
### 🔹 Average Rating
```sql
SELECT CAST(AVG(Rating) AS DECIMAL(10,1)) AS Avg_Rating
FROM blinkit_data;
```
## 📊 Analytical Queries
### 🔹 Total Sales by Fat Content
```sql
SELECT Item_Fat_Content,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Fat_Content;
```
### 🔹 Total Sales by Item Type
```sql
SELECT Item_Type,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Type
ORDER BY Total_Sales DESC;
```
### 🔹 Fat Content by Outlet (Pivot)
```sql
SELECT Outlet_Location_Type,
       ISNULL([Low Fat],0) AS Low_Fat,
       ISNULL([Regular],0) AS Regular
FROM
(
    SELECT Outlet_Location_Type,
           Item_Fat_Content,
           CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
    FROM blinkit_data
    GROUP BY Outlet_Location_Type, Item_Fat_Content
) s
PIVOT
(
    SUM(Total_Sales)
    FOR Item_Fat_Content IN ([Low Fat],[Regular])
) p;
```
### 🔹 Total Sales by Outlet Establishment Year
```sql
SELECT Outlet_Establishment_Year,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Establishment_Year
ORDER BY Outlet_Establishment_Year;
```
### 🔹 Percentage of Sales by Outlet Size
```sql
SELECT Outlet_Size,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
       CAST((SUM(Total_Sales) * 100.0 /
       SUM(SUM(Total_Sales)) OVER()) AS DECIMAL(10,2)) AS Sales_Percentage
FROM blinkit_data
GROUP BY Outlet_Size;
```
### 🔹 Sales by Outlet Location
```sql
SELECT Outlet_Location_Type,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Location_Type;
```
### 🔹 All Metrics by Outlet Type
```sql
SELECT Outlet_Type,
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
       CAST(AVG(Total_Sales) AS DECIMAL(10,0)) AS Avg_Sales,
       COUNT(*) AS No_Of_Items,
       CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating,
       CAST(AVG(Item_Visibility) AS DECIMAL(10,2)) AS Item_Visibility
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;
```
## 📊 Power BI Dashboard Features
- KPI Cards (Total Sales, Avg Sales, Items, Rating)

- Donut Chart: Sales by Fat Content

- Bar Charts: Sales by Item Type & Location

- Matrix: All Metrics by Outlet Type

- Custom designed cards using shapes and icons

## 🛠 Tools & Technologies
- Power BI

- SQL Server / MySQL

- Microsoft Excel

- PowerPoint

# 📁 Project Files
- blinkit.pbix

- BlinkIT Grocery Data.csv

- Blinkit Analysis.pptx

- Query Doc (1).docx

## 🚀 Key Insights
- Low Fat products contribute more to overall sales

- Medium outlet size generates highest revenue

- Certain outlet types dominate total sales


---

## 📸 Dashboard Screenshots

![Dashboard](Images/dashboard.png)


---

## 👤 Author

**Name:** Upendra Dhawalkar   

📧 Email: upendradhawalkar18@gmail.com  
🔗 LinkedIn: https://www.linkedin.com/in/upendradhawalkar  

---





