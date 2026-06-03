---
title: Datasets best practices
description: This article describes best practices for creating and managing datasets in an analysis.
url: https://docs.tealium.com/server-side/insights/datasets-best-practices/
---
The following best practices help ensure efficient dataset performance and data quality in Tealium Insights.

## Optimize dataset structure

Optimizing the structure of your dataset can significantly improve query performance and improve load times.

### Use multiple smaller datasets

Instead of using one large dataset for a dashboard, break it down into multiple smaller datasets. Using smaller datasets reduces the data loaded at once, making queries faster and the dashboard more responsive.

### Reduce the number of columns

When [creating a dataset](), all columns are loaded into SPICE (Super-fast Parallel In-memory Calculation Engine) by default. Including more columns than is necessary can slow down query performance, especially with large datasets. 

For example, in a dataset with 20 million rows:
* 1 column takes approximately `2.63` minutes to load.
* 4 columns take approximately `4.61` minutes to load.
* 150 columns take approximately `19.49` minutes to load.

In the dataset view, include only the columns needed for analysis or dashboards, and remove any columns that aren’t needed. This reduces load times and improves responsiveness.

![](/images/server-side/data-insights/include-and-exclude-columns-in-datasets.png)

## Use date columns to filter rows

For large datasets, using date columns to filter rows can significantly improve database performance.
* For event data, filter by the `event - time` column.
* For visits/visitors data, filter by the `updated` column.

Filtering by these date columns allows Insights to take advantage of sorting optimizations, making it faster to retrieve data.

## Aggregate and process data using SQL

### Use custom SQL

Instead of loading entire tables or schemas, use the **custom SQL** option to pre-aggregate or filter data before loading into SPICE. This reduces dataset size and improves performance.

For example, to count event types by day, use a SQL query like this:

```sql
SELECT 
    COUNT(*) AS count, 
    TRUNC(&#34;event - time&#34;) AS &#34;period&#34;, 
    &#34;event - udo - tealium_event&#34; 
FROM ${db_schema}.events_view__all_events__all_events 
GROUP BY &#34;period&#34;, &#34;event - udo - tealium_event&#34;;
```

Adapt this approach for other aggregations or analyses you need to perform, as it reduces the data processed in SPICE.

### Avoid using `SELECT *` in queries

Using `SELECT *` queries can slow down performance and make queries harder to read. Instead, select only the columns you need.

Avoid selecting all columns:
```sql
SELECT * FROM employees;
```

Select only the columns you need:
```sql
SELECT employee_id, first_name, last_name
FROM employees;
```

If you’re exploring a new table and need to see all columns, use a `LIMIT` clause to reduce the number of rows displayed:

```sql
SELECT * FROM employees
LIMIT 10;
```

### Avoid subqueries

While subqueries offer flexible query organization, they can slow down performance. When possible, use joins or temporary tables instead.

Avoid using a subquery: 
```sql
SELECT employee_id, first_name, last_name
FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE name = &#39;Sales&#39;);
```

Use a join to query data from two tables:
```sql
SELECT e.employee_id, e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE d.name = &#39;Sales&#39;;
```

## Configure incremental refreshes

To maintain dataset accuracy and reduce refresh times, configure an incremental refresh when creating a refresh schedule. Incremental refreshes are ideal for large, frequently updated datasets because it processes only new or updated data, unlike full refreshes, which reload the entire dataset. For best results, we recommend a 2-day window size, though you can adjust this based on your requirements.

![](/images/server-side/data-insights/configure-incremental-refresh.png)