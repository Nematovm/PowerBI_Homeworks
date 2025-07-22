# Lesson 10: Advanced Filtering in DAX

## Prerequisites

Download and open the `Lesson 10.xlsx` file to follow along.

---

## Questions & Answers

### 1. What does `FILTER(Sales, Sales[Amount] > 1000)` return?

It returns a **table** containing only the rows from the `Sales` table where `Amount > 1000`. It does not return a value, but a filtered version of the table.

---

### 2. Write a measure `High Sales` that sums Amount where Amount > 1000 using `FILTER`:

```dax
High Sales = CALCULATE(SUM(Sales[Amount]), FILTER(Sales, Sales[Amount] > 1000))
```

---

### 3. How does `ALLEXCEPT(Sales, Sales[Region])` differ from `ALL(Sales)`?

* `ALL(Sales)` removes **all filters** from the `Sales` table.
* `ALLEXCEPT(Sales, Sales[Region])` removes all filters **except** those on `Sales[Region]`, keeping region-level context.

---

### 4. Use `SWITCH` to categorize Amount:

```dax
Amount Category =
SWITCH(
    TRUE(),
    Sales[Amount] > 500 && Sales[Amount] <= 1000, "Medium",
    Sales[Amount] > 1000, "High",
    "Low"
)
```

---

### 5. What is the purpose of `ALLSELECTED`?

`ALLSELECTED` keeps slicer and page-level filters but **ignores visual-level filters**, useful for calculating context-aware totals or percentages.

---

### 6. Write a measure `Regional Sales %`:

```dax
Regional Sales % =
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Sales, Sales[Region]))
)
```

---

### 7. Create a dynamic measure using `SWITCH` to toggle between `SUM`, `AVERAGE`, and `COUNT`:

```dax
Dynamic Amount Measure =
SWITCH(
    SELECTEDVALUE(MeasureSelector[MeasureType]),
    "Sum", SUM(Sales[Amount]),
    "Average", AVERAGE(Sales[Amount]),
    "Count", COUNT(Sales[Amount]),
    BLANK()
)
```

> Requires a disconnected table `MeasureSelector` with values: "Sum", "Average", "Count"

---

### 8. Use `FILTER` inside `CALCULATE` to exclude "Furniture" sales:

```dax
Sales Excl. Furniture =
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(Products, Products[Category] <> "Furniture")
)
```

---

### 9. Why might `ALLSELECTED` behave unexpectedly in a pivot table?

Because pivot tables can introduce **visual-level filters** for each cell/row, which `ALLSELECTED` ignores. This may cause inconsistent percentages if not handled carefully.

---

### 10. Write a measure that calculates total sales and ignores filters from region:

```dax
Total Sales (Ignore Region) =
CALCULATE(
    SUM(Sales[Amount]),
    ALL(Sales[Region])
)
```

---

### 11. Optimize this measure:

```dax
High Sales =
CALCULATE(SUM(Sales[Amount]), Sales[Amount] > 1000)
```

> This avoids using `FILTER` and improves performance.

---

### 12. Write a measure `Top 2 Products` using `TOPN` and `FILTER`:

```dax
Top 2 Products Sales =
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(
        Products,
        Products[ProductID] IN
            SELECTCOLUMNS(
                TOPN(2, SUMMARIZE(Products, Products[ProductID], "TotalSales", CALCULATE(SUM(Sales[Amount]))), [TotalSales], DESC),
                "ProductID", Products[ProductID]
            )
    )
)
```

---

### 13. Use `ALLSELECTED` with no parameters to respect slicers but ignore visual-level filters:

```dax
Sales % of Slicer Context =
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALLSELECTED())
)
```

---

### 14. Debug: A `SWITCH` measure returns incorrect values in matrix visuals:

> Cause: `SELECTEDVALUE()` returns blank when multiple values are in context.
> Fix:

```dax
Fixed SWITCH Measure =
IF(
    HASONEVALUE(Products[Category]),
    SWITCH(
        VALUES(Products[Category]),
        "Furniture", [MeasureA],
        "Electronics", [MeasureB],
        BLANK()
    ),
    [FallbackMeasure]
)
```

---

### 15. Simulate a "reset filters" button using `ALL`:

```dax
Total Sales (Reset Filters) =
CALCULATE(
    SUM(Sales[Amount]),
    ALL(Sales)
)
```
