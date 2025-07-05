# Lesson 4: Data Transformation with Power Query (Part 2)

## 📌 Theory Questions

### 1. What is the difference between "Merge" and "Append" in Power Query?

* **Merge** combines two tables **horizontally** (column‑wise) based on matching keys, like SQL JOINs (Inner, Left Outer, etc.).
* **Append** combines two tables **vertically** (row‑wise) by stacking rows; schemas must be identical or similar.

---

### 2. How do you split a "Full Name" column into "First Name" and "Last Name"?

1. Select **Full Name**.
2. `Transform ▸ Split Column ▸ By Delimiter`.
3. Choose delimiter **Space** (` `).
4. Rename new columns to **First Name** and **Last Name**.

---

### 3. What is "Pivot Columns" used for?

Turns distinct values in one column into multiple column headers, aggregating a value column. Example: pivot **Product** to show total **Quantity** per product.

---

### 4. How do you undo a step in Power Query?

In **Applied Steps**, click the **❌** next to the step you want to remove.

---

### 5. What is the purpose of "Reference" vs. "Duplicate" in queries?

| Duplicate                                | Reference                                                |
| ---------------------------------------- | -------------------------------------------------------- |
| Creates an independent copy of the query | Creates a linked view that depends on the original query |
| Later edits do **not** affect the source | Reflects changes made to the source                      |
| Heavier (copies all data)                | Lighter, reuses existing steps                           |

---

## ⚙️ Practical Tasks

### 6. Merge **Orders.csv** and **Customers.xlsx** on `CustID` (Inner Join)

1. Load both tables into Power Query.
2. Select **Orders** ▸ `Home ▸ Merge Queries ▸ Merge as New`.
3. Choose **Customers** and select `CustID` in both.
4. Set **Join kind** = **Inner**.
5. Expand merged column to include **Name** and **Email**.

---

### 7. Pivot the **Product** column to show total **Quantity** per product

1. In the merged table, select **Product**.
2. `Transform ▸ Pivot Column`.
3. **Values column** = `Quantity`; **Aggregation** = **Sum**.

---

### 8. Append two tables (Orders\_Jan + Orders\_Feb)

1. Load **Orders\_Jan.csv** and **Orders\_Feb.csv**.
2. `Home ▸ Append Queries ▸ Append as New`.
3. Select the two tables and confirm.

---

### 9. Use **Fill Down** to replace nulls in the **Email** column

1. Select **Email** column.
2. `Transform ▸ Fill ▸ Down`.

---

### 10. Extract the domain from the **Email** column

```m
Text.AfterDelimiter([Email], "@")
```

---

### 11. M‑code to merge queries dynamically based on a parameter

```m
let
    JoinType = "Inner",          // parameter
    Orders   = Orders,            // existing query
    Customers = Customers,        // existing query
    Merged = Table.NestedJoin(
        Orders, {"CustID"},
        Customers, {"CustID"},
        "MergedColumn",
        Record.Field(JoinKind, JoinType)
    )
in
    Merged
```

---

### 12. Unpivot sales columns (e.g., "Jan\_Sales", "Feb\_Sales")

1. Select all monthly sales columns.
2. `Transform ▸ Unpivot Columns`.
3. Rename result columns to **Month** and **Sales**.

---

### 13. Handle errors in a custom column (e.g., division by zero)

```m
try [Column1] / [Column2] otherwise 0
```

---

### 14. Create a function to clean phone numbers

1. `Home ▸ New Source ▸ Blank Query` ▸ **Advanced Editor**.
2. Paste:

```m
(phone as text) =>
let
    Cleaned = Text.Remove(phone, {"-", "(", ")", " "})
in
    Cleaned
```

3. Invoke with `CleanPhone([PhoneNumber])`.

---

### 15. Optimize a query with 10+ steps

* **Filter early**, then sort/group.
* Combine repetitive steps via **Custom Column** instead of multiple `Add Column` actions.
* Remove unused columns early ("Reduce the shape").
* Use **Reference** instead of **Duplicate** when possible.
* Delete intermediary queries that are no longer needed.
