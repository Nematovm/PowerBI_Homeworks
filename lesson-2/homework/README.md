
# Lesson 2 – Importing Data into Power BI

## Theory Answers

**1. List three data sources Power BI can connect to.**  
→ SQL Server, Excel, Web

**2. What is the first step to import data into Power BI Desktop?**  
→ Click on "Get Data" and select your data source.

**3. How do you refresh imported data in Power BI?**  
→ Click the "Refresh" button in the Home tab.

**4. What file formats can Power BI import directly? (Name two.)**  
→ Excel (.xlsx), CSV (.csv)

**5. What does the "Navigator" window show after selecting a data source?**  
→ It displays the available tables or sheets to load or transform.

**6. Import Sales_Data.csv and load only the "Product" and "Price" columns.**  
→ In Navigator, select only "Product" and "Price" before loading.

**7. How would you change OrderDate to a date format during import?**  
→ Use Power Query to change the column type to "Date".

**8. What is the difference between "Load" and "Transform Data" in the import dialog?**  
→ "Load" imports data directly; "Transform Data" opens Power Query to clean or shape data.

**9. Why might you see an error when connecting to a SQL database? (Name one reason.)**  
→ Incorrect credentials or firewall blocking the connection.

**10. How do you replace a data source after importing it?**  
→ Go to "Data source settings" and click "Change Source".

**11. Write the M-code to import only rows where Quantity > 1.**  
```m
= Table.SelectRows(Sales_Data, each [Quantity] > 1)
```

**12. How would you change the data source if Sales_Data.csv changed?**  
→ Use "Data source settings" to browse and select the updated CSV file.

**13. Troubleshoot: Your CSV import fails due to a "mixed data type" error—how do you fix it?**  
→ Set the column data type to "Text" first, then convert appropriately.

**14. Connect to a live SQL database with parameters (e.g., filter by year).**  
→ Use a parameter in Power Query, then apply it in the SQL query or filtering.

**15. How would you automate data imports using Power BI and Power Automate?**  
→ Set up a scheduled refresh with Power Automate or Power BI Service workflows.

---

## Practical Steps

- Imported: `Sales_Data.csv`
- Loaded columns: `Product`, `Price`
- Converted `OrderDate` column to `Date` type
- Used M-code to filter `Quantity > 1`
- Visualized Total Sales, Average Price, and Order Count
- Added a Product Slicer for interactivity

---

## Visuals Included

- **Bar Chart** – Total Sales by Product  
- **Line Chart** – Sales Trend by Order Date  
- **Card** – Total Orders  
- **Card** – Average Price  
- **Slicer** – Product
