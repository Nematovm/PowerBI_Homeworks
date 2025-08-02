# Power BI Project: Movies Analyses Dashboard with DAX

## Dataset
All data is provided in **Movies.xlsx**.

---

## Data Preparation
- Loaded `Movies.xlsx` into Power BI Desktop.
- Removed or imputed missing values in `Budget` and `Box Office` columns (replaced with 0 or median).
- Ensured appropriate data types for all columns.
- Created a **DATE table** using `Release Date` column with:
  - `CALENDARAUTO()`
  - `ADDCOLUMNS()` and `FILTER()`
- Built a relationship between the Movies and Date table.

---

## DAX Measures and Calculated Columns

### Calculated Columns
- **Profit** = `Movies[Box Office] - Movies[Budget]`
- **Run Time Category** =
  ````
  Run Time Category = 
  SWITCH(TRUE(),
    Movies[Run Time] < 90, "Short",
    Movies[Run Time] >= 90 && Movies[Run Time] < 120, "Medium",
    Movies[Run Time] >= 120, "Long"
  )
  ````

### Measures
- **Total Box Office** = `SUM(Movies[Box Office])`
- **Average Budget** = `AVERAGE(Movies[Budget])`
- **Average Margin** = `AVERAGE(Movies[Box Office] - Movies[Budget])`
- **Total Movies with Oscars** =
  ````
  Total Movies with Oscars = 
  COUNTROWS(FILTER(Movies, Movies[Oscar Wins] > 0))
  ````
- **Top Genre by Box Office** =
  ````
  Top Genre by Box Office = 
  CALCULATE(
    MAX(Movies[Genre]),
    TOPN(1, SUMMARIZE(Movies, Movies[Genre], "TotalBoxOffice", SUM(Movies[Box Office])), [TotalBoxOffice])
  )
  ````
- **YoY Box Office Growth** =
  ````
  YoY Box Office Growth = 
  DIVIDE(
    [Total Box Office] - CALCULATE([Total Box Office], DATEADD('Date'[Date], -1, YEAR)),
    CALCULATE([Total Box Office], DATEADD('Date'[Date], -1, YEAR))
  )
  ````
- **Average Nominations per Director** =
  ````
  Average Nominations per Director = 
  AVERAGEX(VALUES(Movies[Director]), CALCULATE(AVERAGE(Movies[Nominations])))
  ````

---

## Dashboard Pages

### Page 1: Overview Dashboard
- **Card Visuals**:
  - Total Box Office
  - Profit Margin
  - Movies with Oscars
- **Bar Chart**:
  - Total Box Office by Genre (stacked by Certificate)
- **Line Chart**:
  - Box Office trend by Release Year
- **Slicer**:
  - Filter by Country and Release Date (range)
- **KPI**:
  - YoY Box Office Growth (Target: > 0%)

### Page 2: Director Analysis
- **Treemap**:
  - Budget by Director (Size = Budget, Color = Oscar Wins)
- **Table**:
  - Director | Total Nominations | Total Oscars | Avg Nominations per Director
- **Slicer**:
  - Filter by Genre
- **Donut Chart**:
  - Run Time Category distribution for selected Director

### Page 3: Genre and Country Insights
- **Matrix**:
  - Genre vs Country with Total Box Office
  - Conditional Formatting: Color scale for Box Office
- **Pie Chart**:
  - Share of Box Office by Certificate
- **Word Cloud**:
  - Genre (Custom Visual from marketplace)
- **Slicer**:
  - Filter by Run Time Category

---

## Author
Generated for Power BI Lesson 15