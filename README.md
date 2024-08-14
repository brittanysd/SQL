# Music Store Database Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Insights](#insights)

### Project Overview

The purpose of this project is to analyze a music store's database in order to gain insights on sales, inventory, and trends.

### Data Source

Sales Data: The primary dataset used for this analysis is the chinook database  [here](https://github.com/lerocha/chinook-database).

### Tools

- Excel
- SQL Server

### Exploratory Data Analysis

- What is the average amount of sales across each 
company?
- What is the unit price of each genre?
- How many tracks are there in each genre?
- How many customers does each of the employees 
support?

### Data Analysis

```sql
SELECT
  c.company
 ,AVG(il.unitprice * il.quantity) total_sales
FROM invoice i
JOIN customer c
  ON c.customerid = i.customerid
JOIN invoiceline il
  ON i.invoiceid = il.invoicelineid
GROUP BY 1;

SELECT
  g.name
 ,MAX(t.unitprice) unit_price
FROM genre g
JOIN track t
  ON g.genreid = t.genreid
GROUP BY 1;

SELECT
  g.name genre_name
 ,COUNT(*) genre_total
FROM genre g
JOIN track t
  ON g.genreid = t.genreid
GROUP BY genre_name
ORDER BY 2 DESC;

SELECT
  e.firstname
 ,e.lastname
 ,COUNT(c.supportrepid) support_rep
FROM customer c
JOIN employee e
  ON e.employeeid = c.supportrepid
GROUP BY 2
        ,1;
```

### Insights

The anaysis results are summarizaed as follows:
1. The average amount of sales across each company is consistent. Each company sold the same amount of units.
2. Classical, Comedy, Sci Fi & Fantasy, Science Fiction, and TV Shows genres all have the highest price per unit at $1.99.
3. Majority the tracks purchased were from the Rock genre.
4. Jane Peacock has more customers while Steve Johnson has the least out of the support sales reps.

