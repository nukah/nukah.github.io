---
title: "Database column type overflow case"
date: 2023-03-18T15:00:00+04:00
tags: ['interview', 'engineering', 'case', 'database']
---

# Database interview questions
Here is the list of tasks which can be used to verify knowledge of working with various databases.

<!--more-->
## Database query performance case

- Create a multi-column table and insert multiple rows.
- Create indexes on several columns which are used in the query.
- Create a query that shows fast performance when executed with EXPLAIN, but the actual query execution results in a long wait.
- Explain why the query, which appears to perform fast when EXPLAIN is run, actually performs slowly, and what might explain this difference in performance.

## Query composition #1
Write a query that selects the top 10 best-selling products over the last 3 months from the orders table.

### Input data:
Orders table with columns: order_id, customer_id, product_id, order_date, order_quantity.

### Table schema:

```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    order_date TIMESTAMP NOT NULL,
    order_quantity INTEGER NOT NULL
);
```

### Sample data:
```sql
INSERT INTO orders (customer_id, product_id, order_date, order_quantity) VALUES
(1, 1, '2022-01-01', 5),
(1, 2, '2022-01-01', 3),
(2, 1, '2022-02-01', 2),
(2, 2, '2022-02-01', 1),
(2, 3, '2022-02-01', 4),
(3, 1, '2022-03-01', 1),
(3, 3, '2022-03-01', 6),
(4, 2, '2022-04-01', 3),
(4, 3, '2022-04-01', 2);
```

### Expected output:

- product_id
- total_quantity (sum of order_quantity for this product over the last 3 months)

## Query composition #2

### Task
Write a query to select customers who have not placed orders in over 6 months.

### Input data:
Orders table with columns: order_id, customer_id, product_id, order_date, order_quantity.

### Table schema:

```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    order_date TIMESTAMP NOT NULL,
    order_quantity INTEGER NOT NULL
);
```
### Sample data:

```sql
INSERT INTO orders (customer_id, product_id, order_date, order_quantity) VALUES
(1, 1, '2022-01-01', 5),
(1, 2, '2022-01-01', 3),
(2, 1, '2022-02-01', 2),
(2, 2, '2022-02-01', 1),
(2, 3, '2022-02-01', 4),
(3, 1, '2022-03-01', 1),
(3, 3, '2022-03-01', 6),
(4, 2, '2022-04-01', 3),
(4, 3, '2022-04-01', 2);
```

### Expected output:
- customer_id

## Optimising a query using partitions

There is an SQL query that runs rather slowly on a large amount of data. The query has to be optimized using table partitions.

### Input data:
```sql
SELECT COUNT(*), date_trunc('day', created_at)
FROM my_table
WHERE created_at BETWEEN '2022-01-01' AND '2022-02-01'
GROUP BY date_trunc('day', created_at)
ORDER BY date_trunc('day', created_at);
```

### Test data:
- Table "my_table" with 1 billion records.
- The "created_at" column is of data type timestamp with time zone.
- Partitioning the table by "created_at" column by month range.
- Indexes on the "created_at" column.