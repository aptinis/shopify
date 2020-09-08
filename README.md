# Shopify Data Science Challenge

## Question 1:

- 5000 orders totalling $15,725,640 and 43936 total items placed between 2017-03-01 and 2017-03-30
- The largest order was $704,000.00 and had 2000 items.
- 78% of total sales were from only 3 users (user_id = 607, 878, 834)
- Average Order Value $3145.13, with an average of 8.79 items per order

### a. 
The average order value of $3145.13 is unexpectedly high given that it's only sneakers being sold is likely due to 2 stores in particular.
- Shop 42 has an average order value of $235101.49 with an average of 667.90 items per order. At shop 42 a single customer purchased 34,000 pairs of shoes at $352, in 17 separate orders.
- Shop 78 has an average order value of $49213.04 with an average of 1.91 items. At shop 78 there were a total 46 orders and each pair of shoes cost $25,725.
- The mean is affected by these extreme order totals (caused by the large number of items per order with shop 42 and the expensive shoes sold by shop 78). The data is highly variable with a large standard deviation and variance. These large measures of dispersion suggest the mean does not represent the data well.

### b. 
A better metric to report the central tendency of this data would be the median. The median is more robust to extreme values and better represents the dataset.

### c.
The median of the amount per order is $284.00.

## Question 2:

### a.
    SELECT COUNT(Orders.ShipperID) AS NumOrders
    FROM Orders
    WHERE ShipperID=3;

| NumOrders |
| --------- |
| 68 |

### b.
    SELECT LastName, MAX(NumOrders)
    FROM (
    SELECT LastName, COUNT(ord.OrderID) as NumOrders
    FROM [Orders] as ord INNER JOIN Employees as em
    ON ord.EmployeeID = em.EmployeeID
    GROUP BY em.EmployeeID);

LastName | MAX(NumOrders)
---------| ---------------
Peacock  | 40

### c. 
    SELECT ProductName, MAX(count)
    FROM (
    SELECT ProductName, COUNT(ProductName) as count
    FROM [Orders] as ord INNER JOIN OrderDetails as ordet
    ON ord.OrderID = ordet.OrderID
    INNER JOIN Customers cus
    ON ord.CustomerID = cus.CustomerID
    INNER JOIN Products prod
    ON ordet.ProductID = prod.ProductID
    WHERE Country = 'Germany'
    GROUP BY prod.ProductName);

ProductName	| MAX(count)
------------|-----------
Gorgonzola Telino	| 5
