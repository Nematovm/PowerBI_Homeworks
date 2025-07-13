# 📊 Project 1: Basic Sales Dashboard

## 📝 Prerequisites
- ✅ Download the dataset: **Retail_Sales_Data.xlsx**
- ✅ Install Power BI Desktop

---

## 📂 Step 1: Import Data

1. Open **Power BI Desktop**.
2. Click on **"Get Data" → "Excel"**.
3. Select the file **Retail_Sales_Data.xlsx**.
4. Load the table into Power BI.

---

## 📈 Step 2: Table Visual — Region & Sales

- Go to **Report** view.
- Insert a **Table** visual.
- Drag **Region** and **Sales** fields into the Values section.

✅ **Expected Output**:

| Region | Sales |
|--------|-------|
| North  | 1200  |
| South  | 125   |
| East   | 80    |

---

## 🎛️ Step 3: Add a Slicer for Product

- Insert a **Slicer** visual.
- Drag the **Product** field into the slicer.

✅ Now, you can filter the visuals by selecting a product.

---

## 🌑 Step 4: Apply Dark Mode Theme

- Go to **View → Themes → Dark**.
- Select the built-in **"Dark"** theme.

✅ The dashboard will now have a dark background and light text.

---

## ❓ What is the "Data" and "Model" View in Power BI?

- **Data View**: Allows you to see and clean table data, add calculated columns, and inspect rows.
- **Model View**: Lets you define relationships between tables, create star schemas, and manage model structure.

---

## 📊 Step 5: Create Dashboard Visuals

### a) Bar Chart: Sales by Region
- Insert a **Clustered Bar Chart**.
- Axis: `Region`
- Value: `Sales`

### b) Line Chart: Sales over Date
- Insert a **Line Chart**.
- Axis: `Date`
- Value: `Sales`

### c) Card Visual: Total Profit
- Insert a **Card**.
- Drag `Profit` into the **Field** well.
- Aggregation: **Sum**

---

## 🔍 Step 6: Drill-through from Region → Detailed Sales

1. Create a **new page** and rename it to `Region Details`.
2. Add `Region` to the **Drill-through** filters section.
3. Add visuals like table/chart on that page (Product, Sales, Profit).

Now, on the main page, **right-click on a region**, select **Drill through → Region Details**.

---

## 🎨 Step 7: Conditional Formatting for High-Profit Regions

1. Select the **Table** visual with Region and Profit.
2. Click on **Profit column → Conditional Formatting → Background color**.
3. Set rules:
   - Green for profit > 200
   - Yellow for profit > 100
   - Red otherwise

✅ Helps highlight high-performing regions visually.

---

## ☁️ Step 8: Publish to Power BI Service

1. Click **Home → Publish**.
2. Sign in to Power BI account.
3. Select the desired workspace.

---

## 👥 Step 9: Share Report (Simulated)

In Power BI Service:

1. Go to the workspace where report is published.
2. Click **"Share"**.
3. Enter your colleague’s email.
4. Grant them **View access**.

✅ Simulates real-world collaboration.

---

## ➕ Step 10: Add "Sales Growth %" Using Quick Measure

1. Right-click on the table → **New Quick Measure**.
2. Choose: `Calculation → Percent difference from previous value`.
3. Base value: **Sales**
4. Time: **Date**

✅ No DAX needed — Power BI creates the DAX for you.

---

## ⚡ Step 11: Optimize Dataset

- Go to **Data View**.
- Remove unused columns (like `OrderID` if not needed).
- Ensure data types are correct (e.g., `Date` is in date format).

✅ Helps improve performance & refresh speed.

---

## 🛠️ Step 12: Troubleshooting – Slicers Not Working?

- Check if visuals are **filtered by the same field** used in the slicer.
- Select slicer → Format → **Edit Interactions**.
- Ensure slicer affects all relevant visuals (not set to "None").

---

## 🖼️ Step 13: Embed into PowerPoint

1. In Power BI Service → Open report.
2. Click **File → Embed Report → PowerPoint**.
3. Download the `.pptx` or copy the embed link.
4. Paste into PowerPoint using **Insert → Online Video** or embed code.

---

## 🕐 Step 14: Scheduled Refresh Setup

1. Go to **Power BI Service → Workspace → Dataset Settings**.
2. Expand **Scheduled Refresh**.
3. Turn it ON, set frequency (e.g., daily).
4. Enter credentials if needed (gateway, etc.).

✅ Keeps data updated without manual refresh.

---

## ✅ Sample Data Preview

| OrderID | Date       | Product  | Region | Sales | Profit |
|---------|------------|----------|--------|-------|--------|
| 2001    | 1/1/2023   | Laptop   | North  | 1200  | 300    |
| 2002    | 1/5/2023   | Mouse    | South  | 125   | 25     |
| 2003    | 1/10/2023  | Keyboard | East   | 80    | 15     |

---

Happy Dashboarding! 🎉  
*Created by Muhammadali, Lesson 7*
