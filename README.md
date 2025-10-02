# Elevate-Labs---Task-6
# Used restaurant database

**Advanced SQL Techniques**:


## 🧠 Advanced SQL Techniques: Subqueries

This section demonstrates how subqueries are used in the `restaurant` database to perform complex queries and analysis.

### 🔹 Scalar vs. Correlated Subqueries

#### ✅ Scalar Subquery
Returns a single value, the same for all rows.

```sql
SELECT customerName,
       (SELECT COUNT(*) FROM orders) AS total_orders_in_system
FROM customer;
```

#### ✅ Correlated Subquery
Runs per row, referencing the outer query.

```sql
SELECT customerName,
       (SELECT COUNT(*) 
        FROM orders 
        WHERE orders.customerId = customer.customerId) AS order_count
FROM customer;
```

---

### 🔹 Subqueries with `IN`, `EXISTS`, and `=`

#### ✅ Using `IN`
Find customers who placed orders over ₹500.

```sql
SELECT customerName
FROM customer
WHERE customerId IN (
    SELECT customerId 
    FROM orders 
    WHERE total_amount > 500
);
```

#### ✅ Using `EXISTS`
Find customers who have placed any order.

```sql
SELECT customerName
FROM customer
WHERE EXISTS (
    SELECT 1 
    FROM orders 
    WHERE orders.customerId = customer.customerId
);
```

#### ✅ Using `=`
Find the customer who placed the highest-value order.

```sql
SELECT customerName
FROM customer
WHERE customerId = (
    SELECT customerId 
    FROM orders 
    ORDER BY total_amount DESC 
    LIMIT 1
);

