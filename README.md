#### Employee-Data-Analysis-SQL-Portfolio




### Table of Contents

- [Introduction](introduction)

- [Objective and Scope](objective-and-scope)

- [SQL Queries and Analysis](sql-queries-and-analysis)

  [Order Management Involvement](order-managemnt-involvement)

  [Employee Performance in Order Handling](employee-performance-in-order-handling)

  [Top Revenue Generating Employees](top-revenue-generating-employees)

  [Regional Trends in Employee Performance](regional-trends-in-employee-performance)

  [Average Employee Tenure](average-employee-tenure)

- [Challenges Encountered](challenges-encountered)

- [Insights and Conclusions](insights-and-conclusions)

## Introduction
In today’s competitive business landscape, a company’s success largely depends on its people. Understanding the contributions and performance of employees in areas like order management and revenue generation is essential for effective workforce planning and strategy. This portfolio showcases SQL queries designed to extract key employee performance metrics and drive meaningful insights for better decision-making.

## Objective and Scope
The purpose of this portfolio is to present a structured approach to analyzing employee data through SQL. By examining metrics such as order management involvement, individual performance in order handling, revenue generation, regional trends, and tenure, this portfolio provides a comprehensive view of workforce impact. This analysis can benefit recruiters, HR professionals, and business leaders seeking data-backed strategies for workforce management.

## SQL Queries and Analysis

- Order Management Involvement

Query:

SELECT COUNT(DISTINCT SalespersonID) AS employees_involved
FROM orders;

Description: This query counts the unique employees involved in managing orders. It reveals insights into team engagement and resource allocation, indicating how many employees contribute to order management.

Results: Through this analysis, we identified that 19 employees actively contribute to order management, emphasizing cross-functional team engagement.

![Employee involved in managing order](https://github.com/user-attachments/assets/2afe224b-4909-4821-ac8c-8fbb26fc79ed)




- Employee Performance in Order Handling

Query:

SELECT e.EmployeeID, e.First, COUNT(o.OrderID) AS total_orders_handled
FROM employees e
JOIN orders o ON e.EmployeeID = o.SalesPersonID
GROUP BY e.EmployeeID, e.First
ORDER BY total_orders_handled DESC;


![Employees performance in order handling](https://github.com/user-attachments/assets/0f0f7af5-1c09-4d63-954f-cad47abcfc43)


Description: This query ranks employees based on the total number of orders they handle. It provides insight into individual workload and efficiency, allowing managers to recognize high performers and address any disparities in workload distribution.

Results: Employee performance varies, with [Rita] handling the highest number of orders [137], indicating high productivity and possible prioritization in customer management.

- Top Revenue Generating Employees

Query:

SELECT e.EmployeeID, e.Last, SUM(o.Quantity * p.SuggestedRetail) AS total_revenue
FROM employees e
JOIN orders o ON e.EmployeeID = o.SalespersonID
JOIN Products p ON o.ProductID = p.ProductID
GROUP BY e.EmployeeID, e.Last
ORDER BY total_revenue DESC
LIMIT 5;

![Top revenue generating employees](https://github.com/user-attachments/assets/750875bd-5f21-42a1-8408-97256a59da0e)



Description: This query identifies the top revenue-generating employees by calculating total revenue from the orders they processed. It highlights key contributors to the company’s financial success and can guide reward and recognition programs.

Results: The top 5 employees generate significant revenue, with [Short] leading at 6143182.76, underscoring high sales impact and the potential for targeted recognition or reward programs.

- Regional Trends in Employee Performance

Query:

SELECT  s.RegionName,  e.First,  e.Last, COUNT(o.OrderID) AS total_orders, SUM(o.Quantity * p.SuggestedRetail) AS total_sales 
FROM  states s  -- Start with states to ensure all regions are included
LEFT JOIN  building_states bs ON s.StateAbbr = bs.StateAbbr  -- Join with building_states to get the Building
LEFT JOIN  employees e ON bs.Building = e.Building  -- Join with employees to get employee details
LEFT JOIN orders o ON e.EmployeeID = o.SalesPersonID  -- Join with orders for order details
LEFT JOIN products p ON o.ProductID = p.ProductID  -- Join with products to get product details
GROUP BY s.RegionName, e.First, e.Last 
ORDER BY s.RegionName, total_orders DESC 
LIMIT 0, 1000;

![Regional Trends](https://github.com/user-attachments/assets/e67ee192-5537-494e-b387-5767f90334de)



Description: This query analyzes regional trends in employee performance by counting total orders and sales per employee in each region. By using a LEFT JOIN on the states table, the query ensures that all regions are included, even those with no orders. This analysis helps identify which regions have the highest activity and may indicate a need for targeted resource allocation or marketing efforts.

Results: Our analysis shows that [Top State] consistently has higher performance metrics, suggesting either a greater customer base or more active engagement from employees in this region.

- Average Employee Tenure

Query:

SELECT AVG(TIMESTAMPDIFF(YEAR, hire_date, CURDATE())) AS avg_tenure_years FROM employees;

![Average Employee Tenure](https://github.com/user-attachments/assets/1fe40ce9-ef38-4196-aa86-90e98ad2225f)


Description: This query calculates the average tenure of employees, an important metric for workforce stability and experience levels within the company. 
Understanding tenure helps assess the balance between experienced and newer employees, which can influence company culture and innovation.

Results: The average tenure is approximately X years, indicating a mix of both experienced and relatively new employees, which can be valuable for diversity in ideas and approaches.

 
 ## Challenges Encountered
 
Throughout the analysis, I faced several challenges, including:

Data Integrity Issues: Some tables had missing or inconsistent data, leading to unexpected results. I had to perform data cleaning and validation before running analyses.

Complex Joins: The need to join multiple tables (e.g., states, employees, orders, products) complicated the queries. I had to carefully consider join types (INNER vs. LEFT) to ensure that I included all relevant data while avoiding duplicates.

Query Performance: The initial versions of my queries were slow due to large data volumes. I optimized them by filtering data earlier in the query and ensuring proper indexing on frequently joined columns.

Interpreting Results: After executing the queries, some results were not aligned with expectations. I had to iterate on my queries, adjusting grouping and aggregation techniques to accurately reflect the intended metrics.

## Insights and Conclusions

From this analysis, several valuable insights emerge:

- Order Management Involvement: The company benefits from a diverse team in order management, fostering collaboration across departments.

- Employee Performance in Order Handling: Employees like [Rita] play a crucial role in customer interactions, possibly indicating an area for resource optimization.

- Top Revenue Generators: Recognizing top revenue contributors enables targeted rewards, fostering a culture of appreciation and motivation.

- Regional Trends: Regional differences suggest a tailored approach in different states may enhance performance further.

- Average Tenure: The tenure data underscores a balanced team composition, which is ideal for innovation and growth.

These findings can guide strategic decisions in resource allocation, employee recognition, and region-specific strategies.
