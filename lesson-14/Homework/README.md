# 📘 Lesson 14: DAX Optimization

## 🧾 Prerequisites

- Download the `Chocolate Sales.csv` file and load into Power BI.
- Disable Auto DateTime:
  - Go to: `File` → `Options and Settings` → `Options` → `Current File` → `Data Load`
  - Uncheck: **Auto Date/Time for new files**
- Create a `Date` table using the following DAX:

```DAX
Date = 
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMM"),
    "MonthNo", MONTH([Date]),
    "YearMonth", FORMAT([Date], "YYYY-MM")
)
```

---

## ✅ Tasks and Solutions

### 1. Use variable to calculate % Growth in Sales Compared to Last Year

```DAX
%Growth YoY = 
VAR CurrentSales = SUM('Chocolate Sales'[SalesAmount])
VAR LastYearSales = CALCULATE(SUM('Chocolate Sales'[SalesAmount]), SAMEPERIODLASTYEAR('Date'[Date]))
RETURN DIVIDE(CurrentSales - LastYearSales, LastYearSales)
```

---

### 2. Use variable to calculate the difference between Sales Amount of current month and previous month

```DAX
SalesDiff MoM = 
VAR CurrMonth = SUM('Chocolate Sales'[SalesAmount])
VAR PrevMonth = CALCULATE(SUM('Chocolate Sales'[SalesAmount]), PREVIOUSMONTH('Date'[Date]))
RETURN CurrMonth - PrevMonth
```

---

### 3. Calculate total boxes shipped and average monthly boxes in one measure using VAR

```DAX
TotalAndAvgBoxes = 
VAR TotalBoxes = SUM('Chocolate Sales'[Boxes])
VAR AvgMonthlyBoxes = AVERAGEX(VALUES('Date'[YearMonth]), CALCULATE(SUM('Chocolate Sales'[Boxes])))
RETURN TotalBoxes + AvgMonthlyBoxes
```

---

### 4. Calculate total boxes shipped and average monthly boxes in one measure using VAR and return average monthly boxes only

```DAX
AvgMonthlyBoxes = 
VAR TotalBoxes = SUM('Chocolate Sales'[Boxes])
VAR AvgMonthly = AVERAGEX(VALUES('Date'[YearMonth]), CALCULATE(SUM('Chocolate Sales'[Boxes])))
RETURN AvgMonthly
```

---

### 5. Calculate growth percentage from last month

```DAX
%Growth MoM = 
VAR ThisMonth = SUM('Chocolate Sales'[SalesAmount])
VAR LastMonth = CALCULATE(SUM('Chocolate Sales'[SalesAmount]), PREVIOUSMONTH('Date'[Date]))
RETURN DIVIDE(ThisMonth - LastMonth, LastMonth)
```

---

### 6. Create a moving average of sales over the last 3 months

```DAX
3M Moving Avg Sales = 
CALCULATE(
    AVERAGEX(
        DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -3, MONTH),
        CALCULATE(SUM('Chocolate Sales'[SalesAmount]))
    )
)
```

---

### 7. Use Card to show a Dynamic Message Based on Sales Rank and YoY Performance

```DAX
Sales Message = 
VAR Product = SELECTEDVALUE('Chocolate Sales'[Product])
VAR Rank = RANKX(ALL('Chocolate Sales'[Product]), CALCULATE(SUM('Chocolate Sales'[SalesAmount])))
VAR SalesCurr = CALCULATE(SUM('Chocolate Sales'[SalesAmount]))
VAR SalesPrev = CALCULATE(SUM('Chocolate Sales'[SalesAmount]), SAMEPERIODLASTYEAR('Date'[Date]))
VAR Growth = DIVIDE(SalesCurr - SalesPrev, SalesPrev)

RETURN
SWITCH(
    TRUE(),
    Rank <= 3 && Growth > 0.1, "Top Performer - Sales up by " & FORMAT(Growth, "0.0%"),
    Growth > -0.05 && Growth < 0.1, "Consistent Performer",
    "Needs Improvement"
)
```

---

### 8. List Top 5 tips to optimize DAX query manually and explain why

1. **Use Variables (`VAR`)**  
   Reduces repeated calculations, improves performance and readability.

2. **Minimize `FILTER` in iterators**  
   Use `CALCULATE` with proper filter context to avoid performance hits.

3. **Avoid Complex Calculations in Visuals**  
   Define explicit measures outside visuals.

4. **Use Aggregation on Columns, not Expressions**  
   Aggregating expressions is slower than using a measure or column directly.

5. **Reduce Column Cardinality**  
   Lower unique values help compression and improve engine speed.

---

### 9. Benefits of Using DAX Optimization Tools

| Tool | Benefits |
|------|----------|
| **DAX Studio** | Analyze query plans, find bottlenecks, inspect storage engine vs formula engine. |
| **Performance Analyzer** | Profile visual-level query duration to optimize dashboards. |
| **Tabular Editor** | Easily manage measures, KPIs, and metadata, and write optimized DAX in bulk. |

---

### 10. Create a flag (Yes/No) if a product is in the top 5 by total sales

```DAX
Top 5 Product Flag = 
VAR ProductRank = RANKX(
    ALL('Chocolate Sales'[Product]),
    CALCULATE(SUM('Chocolate Sales'[SalesAmount]))
)
RETURN IF(ProductRank <= 5, "Yes", "No")
```

---

### 🏁 End of Lesson

You have now explored DAX optimization techniques, time intelligence, ranking logic, and measure performance tuning for real-world Power BI dashboards.
