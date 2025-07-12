# Lesson 6: Creating Basic Visualizations & Adding Interactivity to Visuals

## Questions and Answers

### 1. Name three types of visuals you can create in Power BI.
- Bar Chart
- Line Chart
- Pie Chart

### 2. How do you add a slicer to a report?
- Go to the Visualizations pane, click the Slicer icon, then drag a field (e.g., Quarter) into the slicer’s Field well.

### 3. What is the difference between a bar chart and a column chart?
- A bar chart displays horizontal bars, whereas a column chart displays vertical bars. Both are used to compare values across categories.

### 4. How do you change the color of a visual background?
- Select the visual, go to the Format pane, expand the “General” section, and change the background color option.

### 5. What does "drill-down" mean in a visual?
- Drill-down allows users to explore data at more detailed levels within a hierarchy (e.g., from Region → Product → Quarter).

## Tasks

### 6. Create a bar chart showing SalesAmount by Region.
- Visual: Bar Chart
- Axis: Region
- Values: SalesAmount

### 7. Add a slicer for Quarter to filter all visuals on the page.
- Visual: Slicer
- Field: Quarter

### 8. Format the bar chart to show data labels.
- Select the bar chart → Format pane → Data labels → On

### 9. Use a line chart to show SalesAmount trends over Quarter.
- Visual: Line Chart
- Axis: Quarter
- Values: SalesAmount

### 10. Add a tooltip to display Product details when hovering over bars.
- Drag the Product field into the Tooltips well of the bar chart.

### 11. Sync slicers across multiple report pages.
- Use the View tab → Sync slicers → Enable for desired slicers and pages.

### 12. Create a custom visual with dynamic measure selection (e.g., Sales vs. Profit).
- Create a disconnected table with measure names.
- Use a measure with SWITCH() to return values based on selection.

### 13. Implement a hierarchy for Region > Product > Quarter drill-down.
- In the Data pane, drag Product into Region, then drag Quarter into Product to form a hierarchy.
- Use this hierarchy in a visual and enable drill mode.

### 14. Use bookmarks to toggle between two visuals in the same space.
- Create both visuals, use Selection pane to show/hide, then add bookmarks to toggle visibility.

### 15. Optimize a slow-rendering report with 10+ visuals.
- Reduce unnecessary visuals, use aggregations, disable interactions where not needed, and consider using bookmarks instead of separate visuals.

---

📁 Dataset used: `Sales_Interactive.xlsx`