# Lesson 13 - Time-Based Calculations in Power BI

**Dataset:** Chocolate Sales.csv  
**Path:** `C:\Users\MaabLLC\Desktop\maab\_files\PowerBI\_Homeworks\Chocolate Sales.csv`

## Prerequisites
- Load the CSV file into Power BI.
- Disable *Auto Date/Time* for new files:  
  File > Options and Settings > Options > Data Load > *Time Intelligence* > Uncheck "Auto Date/Time."
- Create a proper Date table using:
```DAX
Date = 
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Quarter", QUARTER([Date]),
    "YearMonth", FORMAT([Date], "YYYY-MM")
)
```
- Create a relationship between the `Date` table and the `Sales Date` column from the `Chocolate Sales` table.

---

## Basic Level (1–5)

```DAX
1. Total Sales Amount (All-Time)
Total Sales = SUM('Chocolate Sales'[Sales Amount])

2. Total Sales for Current Year
Total Sales This Year = 
CALCULATE([Total Sales], YEAR('Date'[Date]) = YEAR(TODAY()))

3. Total Sales for Last Year
Total Sales Last Year = 
CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))

4. Total Sales for Current Month
Total Sales This Month = 
CALCULATE([Total Sales], MONTH('Date'[Date]) = MONTH(TODAY()) && YEAR('Date'[Date]) = YEAR(TODAY()))

5. Total Sales for Current Quarter
Total Sales This Quarter = 
CALCULATE([Total Sales], QUARTER('Date'[Date]) = QUARTER(TODAY()) && YEAR('Date'[Date]) = YEAR(TODAY()))
```

---

## Intermediate (6–10)

```DAX
6. Sales Growth % Compared to Last Year (%YoY)
YoY Growth % = 
DIVIDE(
    [Total Sales This Year] - [Total Sales Last Year],
    [Total Sales Last Year]
)

7. Sales Last Month
Sales Last Month = 
CALCULATE([Total Sales], PREVIOUSMONTH('Date'[Date]))

8. Running Total of Sales
Running Total Sales = 
CALCULATE(
    [Total Sales],
    FILTER(ALLSELECTED('Date'[Date]),
        'Date'[Date] <= MAX('Date'[Date])
    )
)

9. Sales Last 3 Months
Sales Last 3 Months = 
CALCULATE(
    [Total Sales],
    DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -3, MONTH)
)

10. Month with Highest Sales in Last 12 Months
Max Sales Month = 
CALCULATE(
    MAX('Chocolate Sales'[Sales Amount]),
    DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -12, MONTH)
)
```

---

## Advanced (11–15)

```DAX
11. Compare Q1 Sales of Each Year
Q1 Sales = 
CALCULATE(
    [Total Sales],
    'Date'[Quarter] = 1
)

12. YoY Difference for December Only
YoY December = 
VAR CurrentYearDec = 
    CALCULATE([Total Sales], MONTH('Date'[Date]) = 12, YEAR('Date'[Date]) = YEAR(TODAY()))
VAR LastYearDec = 
    CALCULATE([Total Sales], MONTH('Date'[Date]) = 12, YEAR('Date'[Date]) = YEAR(TODAY()) - 1)
RETURN
    CurrentYearDec - LastYearDec

13. Last 12 Months Sales
Sales Last 12 Months = 
CALCULATE(
    [Total Sales],
    DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -12, MONTH)
)

14. Sales Difference Between Current and Previous Quarter
Quarter Diff = 
VAR CurrentQ = CALCULATE([Total Sales], DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -3, MONTH))
VAR PrevQ = CALCULATE([Total Sales], DATESINPERIOD('Date'[Date], MAX('Date'[Date]) - 90, -3, MONTH))
RETURN
    CurrentQ - PrevQ

15. Highlight Months Where Sales > 110% of Last Year
Sales Exceeded 110% = 
VAR CurrentMonth = [Total Sales]
VAR LastYearMonth = 
    CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
RETURN
    IF(CurrentMonth > 1.1 * LastYearMonth, 1, 0)
```

---

✅ Use matrix visuals or bar charts to validate the calculations across time periods.
📌 All measures must reference the `Date` table for accurate time-based filtering.
