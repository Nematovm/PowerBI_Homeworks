# Lesson 8: Introduction to DAX Basics & Calculated Columns vs. Measures

## What does DAX stand for?
**DAX** stands for **Data Analysis Expressions**.

## Write a DAX formula to sum the Sales column.
```dax
Total Sales = SUM(Sales[Sales])
```

## What is the difference between a calculated column and a measure?
- **Calculated Column**: Computed row by row and stored in the table. It uses **row context**.
- **Measure**: Calculated at query time based on the filter context, not stored in the table.

## Use the DIVIDE function to calculate Profit Margin (Profit/Sales).
```dax
Profit Margin = DIVIDE(Sales[Profit], Sales[Sales])
```

## What does COUNTROWS() do in DAX?
Returns the number of rows in a table.

## Create a measure: Total Profit that subtracts total cost from total sales
```dax
Total Profit = SUM(Sales[Sales]) - SUM(Sales[Cost])
```

## Write a measure to calculate Average Sales per Product.
```dax
Average Sales per Product = AVERAGEX(VALUES(Sales[Product]), Sales[Sales])
```

## Use IF() to tag products as "High Profit" if Profit > 1000.
```dax
Profit Category = IF(Sales[Profit] > 1000, "High Profit", "Low Profit")
```

## What is a circular dependency error in a calculated column?
Occurs when a calculated column refers to itself or causes an indirect loop, making it impossible to calculate values in order.

## Explain row context vs. filter context.
- **Row context**: Exists in calculated columns or iterators; evaluates expressions row-by-row.
- **Filter context**: Comes from slicers, filters, or CALCULATE; applies filters to evaluate expressions.

## Write a measure to calculate YTD Sales using TOTALYTD().
```dax
YTD Sales = TOTALYTD(SUM(Sales[Sales]), Sales[Date])
```

## Create a dynamic measure that switches between Sales, Profit, and Margin.
```dax
Selected Metric =
SWITCH(
    SELECTEDVALUE(Metrics[Metric]),
    "Sales", SUM(Sales[Sales]),
    "Profit", SUM(Sales[Profit]),
    "Margin", DIVIDE(SUM(Sales[Profit]), SUM(Sales[Sales]))
)
```

## Optimize a slow DAX measure using variables (VAR).
```dax
Optimized Profit Margin =
VAR TotalProfit = SUM(Sales[Profit])
VAR TotalSales = SUM(Sales[Sales])
RETURN DIVIDE(TotalProfit, TotalSales)
```

## Use CALCULATE() to override a filter
```dax
Sales for 2024 = CALCULATE(SUM(Sales[Sales]), Sales[Year] = 2024)
```

## Write a measure that returns the highest sales amount
```dax
Max Sales = MAX(Sales[Sales])
```