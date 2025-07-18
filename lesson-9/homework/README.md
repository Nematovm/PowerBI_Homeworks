
# DAX Concepts and Examples – README

This document explains key DAX concepts and provides answers with practical examples.

---

### 1. What is row context? Give an example in a calculated column.

**Row context** refers to the current row being evaluated in a calculated column. DAX applies the formula on a row-by-row basis.

**Example:**
```DAX
TotalPrice = Sales[Quantity] * Sales[UnitPrice]
```

---

### 2. Write a measure that finds total sales

**Measure:**
```DAX
Total Sales = SUM(Sales[SalesAmount])
```

---

### 3. Use RELATED to fetch the Name from the Customers table into the Sales table.

**Calculated Column:**
```DAX
CustomerName = RELATED(Customers[Name])
```

---

### 4. What does `CALCULATE(SUM(Sales[Quantity]), Sales[Category] = "Electronics")` return?

This returns the **total quantity sold**, but only for rows in the `Sales` table where the category is `"Electronics"`.

---

### 5. Explain the difference between VAR and RETURN in DAX.

- `VAR` is used to define temporary variables to store values or expressions.
- `RETURN` specifies the final result of the expression using those variables.

**Example:**
```DAX
Example = 
VAR Discount = 0.1
RETURN Sales[Amount] * (1 - Discount)
```

---

### 6. Create a calculated column in Sales called TotalPrice using row context (`Quantity * UnitPrice`).

**Calculated Column:**
```DAX
TotalPrice = Sales[Quantity] * Sales[UnitPrice]
```

---

### 7. Write a measure `Electronics Sales` using CALCULATE to sum sales only for the "Electronics" category.

**Measure:**
```DAX
Electronics Sales = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    Sales[Category] = "Electronics"
)
```

---

### 8. Use `ALL(Sales[Category])` in a measure to show total sales ignoring category filters.

**Measure:**
```DAX
Total Sales All Categories = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    ALL(Sales[Category])
)
```

---

### 9. Fix this error: A calculated column in Sales uses `RELATED(Customers[Region])` but returns blanks.

**Likely cause:** There is **no relationship** between `Sales` and `Customers`, or the foreign key (`CustomerID`) contains blanks or invalid values.  
**Fix:** Ensure there is an active relationship and no missing keys.

---

### 10. Why does CALCULATE override existing filters?

`CALCULATE` creates a **new filter context**, replacing existing filters with the ones defined inside it. This allows precise control over how filters are applied to expressions.

---

### 11. Write a measure that returns average unit price of products

**Measure:**
```DAX
Average Unit Price = AVERAGE(Products[UnitPrice])
```

---

### 12. Use VAR to store a temporary table of high-quantity sales (Quantity > 2), then count rows.

**Measure:**
```DAX
High Quantity Count = 
VAR HighQtySales = 
    FILTER(Sales, Sales[Quantity] > 2)
RETURN
    COUNTROWS(HighQtySales)
```

---

### 13. Write a measure `% of Category Sales` that shows each sale's contribution to its category total.

**Measure:**
```DAX
% of Category Sales = 
DIVIDE(
    Sales[SalesAmount],
    CALCULATE(
        SUM(Sales[SalesAmount]),
        ALLEXCEPT(Sales, Sales[Category])
    )
)
```

---

### 14. Simulate a "remove filters" button using ALL in a measure.

**Measure:**
```DAX
Total Sales No Filter = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    ALL(Sales)
)
```

This measure ignores any filters applied to the Sales table.

---

### 15. Troubleshoot: A CALCULATE measure ignores a slicer. What’s the likely cause?

The likely cause is that `CALCULATE` uses a **filter function (like ALL or REMOVEFILTERS)** that **removes** or **replaces** the slicer's filter context. Check if functions like `ALL`, `REMOVEFILTERS`, or `ALLEXCEPT` are overriding slicer behavior.

---
