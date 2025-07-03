# Lesson 3: Data Transformation with Power Query (Part 1)

**Prerequisites:**  
Downloaded files:
- `Customer_Orders.txt`  
- `Orders.txt`

---

## Answers

1. **What is the purpose of the "Applied Steps" pane in Power Query?**  
   It shows the list of transformation steps applied to the query in sequence. You can edit or remove steps from there.

2. **How do you remove duplicate rows in Power Query?**  
   Select the relevant columns → Right-click → *Remove Duplicates*.

3. **What does the "Filter" icon do in Power Query?**  
   It allows you to filter data by specific values or conditions in a column.

4. **How would you rename a column from "CustID" to "CustomerID"?**  
   Right-click on the column name → *Rename* → Enter "CustomerID".

5. **What happens if you click "Close & Apply" in Power Query?**  
   The transformed data is loaded into Power BI’s data model.

6. **Remove all rows where Quantity is less than 2.**  
   Select the Quantity column → Filter Rows → Choose "is less than" → Enter 2 → Click OK → Remove the filtered rows.

7. **Split the OrderDate column into separate "Year," "Month," and "Day" columns.**  
   Use the *Date → Year*, *Month*, and *Day* extract options from the Transform tab.

8. **Replace all "Mouse" entries in the Product column with "Computer Mouse."**  
   Right-click on Product column → Replace Values → Replace "Mouse" with "Computer Mouse".

9. **Sort the table by OrderDate (newest first).**  
   Click on the *OrderDate* column → Sort Descending.

10. **How would you handle null values in the Price column?**  
    Several options:
    1. Replace nulls with 0: Right-click column → Replace Values → Replace null with 0
    2. Fill down: Right-click column → Fill → Down
    3. Remove rows: Right-click column → Remove Empty
    4. Use column statistics: Transform tab → Statistics → Insert Average/Median

11. **Write custom M-code to add a column calculating TotalSpent = Quantity * Price.**  
```m
Table.AddColumn(#"Previous Step Name", "TotalSpent", each [Quantity] * [Price], type number)
```

12. **Group the table by CustID to show total spending per customer.**  
   Use *Group By* → Group by CustID → Aggregation: Sum of TotalSpent.

13. **Fix inconsistent date formats (e.g., 01/10/2023 vs. 2023-01-10) in OrderDate.**  
   Change the data type of *OrderDate* column to *Date*. Power Query will standardize the format.

14. **Create a conditional column: Label orders as "High Value" if Price > 100.**  
   Use *Add Column → Conditional Column* → If [Price] > 100 then "High Value" else "Normal".

15. **Optimize the query to reduce refresh time (e.g., remove unused columns early).**  
   Remove unused columns as early as possible in the transformation steps (before heavy operations like merge, group, etc.).

---



