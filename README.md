Question 1: Given some sample data, write a program to answer the following: click here to access the required data set
On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

a.Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.
  There were outliers in the data with 5 digit values from stores 42 and 78. Therefore all the 5 digit values should be removed. To calculate the new average I removed all the outliers from the order value column got the sum of all remaining values. I then divided the sum by 4937 records that were then present.   

b.What metric would you report for this dataset?
I would report it as Average Small Order Value

c. What is its value?
I got a value of 302.58

Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.
a.How many orders were shipped by Speedy Express in total?
54
SELECT COUNT(*) as ShipmentOrderd FROM [Orders] where ShipperID=1;

b. What is the last name of the employee with the most orders?

Peacock
SELECT LastName, MAX(NetOrders) FROM
(Select *, COUNT(DISTINCT OrderID) as NetOrders FROM
(SELECT o.OrderID, e.EmployeeID, e.LastName, e.FirstName
FROM Orders o Inner Join Employees e
ON o.EmployeeID = e.EmployeeID)
GROUP BY EmployeeID
ORDER BY COUNT(DISTINCT OrderID) DESC)
 
 c.  What product was ordered the most by customers in Germany?
 SELECT ProductName, MaxOrders FROM
(SELECT ProductID, MAX(NetOrders) as MaxOrders FROM
(Select , Count(DISTINCT OrderID) AS NetOrders from
(SELECT
From Orders o Inner Join OrderDetails od
On o.OrderID = od.OrderID
Where CustomerID IN
(Select CustomerID From
Customers Where Country = 'Germany'))
Group by ProductID
Order by COUNT(DISTINCT OrderID) DESC)) t1 Inner Join Products p
WHERE t1.ProductID = p.ProductID

