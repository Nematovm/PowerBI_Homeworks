# 📘 Lesson 11: Date and Time Functions & Financial Functions

## 📌 Topic
Working with date and time functions in DAX, and deriving calendar attributes such as fiscal quarters.

---

## 📂 Prerequisites
Please make sure to download and connect the `Lesson 10.xlsx` file containing the following dataset:

| SaleID | ProductID | Amount | Region | SaleDate   |
|--------|-----------|--------|--------|------------|
| 1      | P1        | 1200   | North  | 1/5/2023   |
| 2      | P2        | 800    | South  | 1/10/2023  |
| 3      | P1        | 1500   | North  | 1/15/2023  |
| 4      | P2        | 600    | East   | 1/20/2023  |

---

## 🧠 Task Description

Create a DAX-calculated table in Power BI with the following criteria:

### 🎯 Table Requirements:
- The table must include **the previous 7 days**, **today**, and **the next 7 days** (total of 15 days).
- It should contain **7 columns**:
  1. `Date`
  2. Name of the day in English (e.g., Friday)
  3. Name of the day in **Uzbek** (e.g., Juma)
  4. `Year`
  5. `Month Name`
  6. `Day Number`
  7. **Fiscal Quarter**, assuming the fiscal year starts in **October**

---

## 🧮 DAX Solution

```DAX
DateContextTable =
VAR TodayDate = TODAY()
VAR StartDate = TodayDate - 7
VAR EndDate = TodayDate + 7
RETURN
ADDCOLUMNS (
    CALENDAR(StartDate, EndDate),
    "Day Name (EN)", FORMAT([Date], "dddd"),
    "Day Name (UZ)", FORMAT([Date], "dddd", "UZ-uz"),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Day Number", DAY([Date]),
    "Fiscal Quarter",
        SWITCH (
            TRUE(),
            MONTH([Date]) IN {10, 11, 12}, "Q1",
            MONTH([Date]) IN {1, 2, 3}, "Q2",
            MONTH([Date]) IN {4, 5, 6}, "Q3",
            MONTH([Date]) IN {7, 8, 9}, "Q4"
        )
)
