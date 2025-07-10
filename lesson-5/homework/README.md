
# Lesson 5 - Data Modeling Basics (README)

## 1. What is a primary key in a table?
A **primary key** is a column (or combination of columns) that uniquely identifies each row in a table. It ensures that there are no duplicate values and every row is distinct. Example: `CustomerID` in the Customer table.

---

## 2. Name the two types of table relationships in Power BI.
- **One-to-Many (1:*)**: A single value in one table can relate to multiple rows in another table.
- **Many-to-Many (*:*)**: Both tables can have multiple instances of the same value in the related column.

---

## 3. How do you create a relationship between two tables in Power BI?
- Open **Model view**.
- Drag a column from one table to the matching column in another.
- Or go to: Home → Manage Relationships → New → Select tables and columns to connect.

---

## 4. What is a "star schema"?
A **star schema** is a data modeling structure where a central **fact table** is connected to multiple **dimension tables**. It looks like a star with the fact table at the center and dimension tables around it. This design is simple and optimized for querying.

---

## 5. Which table is typically the fact table in a sales dataset?
In a sales dataset, the **Sales** table is typically the **fact table** because it contains measurable events like `OrderID`, `CustomerID`, `ProductID`, `Quantity`, and `OrderDate`.

---

## 6. Link Sales.csv to Customers.csv using CustomerID (one-to-many).
Create a relationship:
- `Customer[CustomerID]` (one side)
- `Sales[CustomerID]` (many side)
- This ensures that each customer can have multiple sales entries.

---

## 7. Why is ProductID in Sales.csv a foreign key?
`ProductID` in the Sales table is a **foreign key** because it references the **primary key** in the Products table. It connects each sale to a specific product.

---

## 8. Fix a relationship error where ProductID has mismatched data types.
- Open **Power Query**
- Set the **data type** of `ProductID` in both `Sales` and `Products` tables to **Whole Number**
- Apply the changes and recreate the relationship.

---

## 9. Explain why a star schema improves performance.
- Simplifies relationships and queries  
- Reduces join complexity  
- Improves data compression  
- Enhances performance in DAX calculations and report visuals

---

## 10. Add a new column TotalSales in Sales (Quantity * Price from Products).
In the `Sales` table, use the following DAX formula:
```dax
TotalSales = Sales[Quantity] * RELATED(Products[Price])
```
This uses the `RELATED()` function to bring the price from the Products table.

---

## 11. Optimize a model with circular relationships—how would you resolve it?
- Remove one of the circular relationships  
- Replace with DAX functions like `LOOKUPVALUE`, `TREATAS`  
- Or create a bridge table to break the loop  
- Keep only one active path between any two tables

---

## 12. Create a role-playing dimension for OrderDate and ShipDate.
- Create one `Date` table  
- Link `Date[Date]` to `Sales[OrderDate]` (active)  
- Also link to `Sales[ShipDate]` (inactive)  
- Use `USERELATIONSHIP` in measures when needed

---

## 13. Handle a many-to-many relationship between Customers and Products.
- Create a **Bridge Table** (CustomerProduct) that lists CustomerID and ProductID  
- Connect it with `Customer` and `Product` tables via one-to-many relationships  
- Use it for analysis like which customer bought which product

---

## 14. Use bidirectional filtering sparingly—when is it appropriate?
Use **bidirectional filtering** when:
- You need filters to flow in both directions (e.g., reporting on Many-to-Many relationships)
- For specific use cases like row-level security or bridge tables  
Avoid it in large models to prevent performance issues.

---

## 15. Write DAX to enforce referential integrity if a CustomerID is deleted.
To detect orphan records:
```dax
CheckCustomer = IF(ISBLANK(RELATED(Customer[Name])), "Missing Customer", "OK")
```
Or count broken links:
```dax
BrokenLinks = CALCULATE(COUNTROWS(Sales), ISBLANK(RELATED(Customer[Name])))
```
