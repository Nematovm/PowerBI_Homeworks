# Lesson 19: Publishing and Sharing in Power BI

## 1. What is the difference between Power BI Desktop and Power BI Online Service?
- **Power BI Desktop**: Free application installed on your computer, used to create, transform, and model data, build reports, and develop measures with DAX.
- **Power BI Online Service**: Cloud-based platform (app.powerbi.com) used to publish, share, collaborate, refresh data, and manage dashboards.

## 2. How do you publish a Power BI report from Desktop to the Online Service?
- Click **Publish** in Power BI Desktop → Sign in → Choose a workspace → The report is uploaded to Power BI Online Service.

## 3. What is a workspace in Power BI? What are the types of workspaces available?
- A **workspace** is a collaborative environment in the Power BI Service where reports, datasets, and dashboards are stored.
- Types:
  - **My Workspace**: Personal, only for you.
  - **Shared Workspace (App Workspace)**: Collaborative, allows multiple users to work together.

## 4. What is the difference between a workspace and an app in Power BI?
- **Workspace**: Development and collaboration area.
- **App**: A packaged, read-only version of reports/dashboards shared with end users.

## 5. Explain the different Power BI license types and their limitations.
- **Free**: Limited to personal use in "My Workspace", no sharing.
- **Pro**: Required for sharing, collaboration, and advanced features.
- **Premium Per User (PPU)**: Higher data limits, AI features, paginated reports.
- **Premium Capacity**: Enterprise-level, dedicated capacity, allows free users to view shared content.

## 6. How can you share a report with someone who doesn’t have a Pro license?
- Place the report in a **Premium Capacity Workspace**, then free users can view without Pro.

## 7. What is a semantic model (dataset) in Power BI, and where is it stored in the service?
- A **semantic model (dataset)** is the structured data model behind reports (tables, measures, relationships).
- Stored in the **Power BI Service cloud workspace**.

## 8. How does Scheduled Refresh work in Power BI Online Service?
- Allows datasets to refresh automatically from connected sources on a schedule (daily, multiple times per day). Requires a gateway for on-premises data.

## 9. What is the difference between a dataset and a dataflow in Power BI?
- **Dataset**: A model created in Desktop and published, used directly in reports.
- **Dataflow**: ETL process stored in the cloud (Power Query Online), reusable across multiple datasets.

## 10. When and why would you use a dataflow instead of a dataset?
- Use a **dataflow** when multiple reports need the same cleaned/transformed data. Promotes consistency and reduces redundancy.

## 11. What are dashboards in Power BI Online? How are they different from reports?
- **Dashboard**: A one-page canvas that aggregates visuals from multiple reports and datasets.
- **Report**: Multi-page, interactive visuals connected to a single dataset.

## 12. How do you pin a visual to a dashboard from a report?
- In a report → Hover on visual → Click **Pin** → Choose dashboard.

## 13. What is the mobile view in Power BI and why is it useful?
- A layout optimized for mobile devices, ensuring visuals fit small screens for better user experience.

## 14. What is a paginated report in Power BI and when would you use it?
- Pixel-perfect, paginated (long, printable) report format, suitable for invoices, financial statements, official documents.

## 15. Can you export reports from Power BI Service to PDF or PowerPoint? How?
- Yes. In the service → Open report → File → Export to PDF or PowerPoint.

## 16. What does “Live Connection” mean in Power BI Service, and how does it work?
- Live Connection: Reports directly query a data source (e.g., Analysis Services) in real-time without importing data.

## 17. Explain Row-Level Security (RLS) and how it’s applied in Power BI Online.
- RLS restricts data access for specific users based on roles. Applied in Desktop, published to Service, then roles are assigned to users.

## 18. How can you test RLS roles in Power BI Service?
- In the Service → Dataset settings → Security → "Test as role".

## 19. What are Apps in Power BI and how do you publish one?
- An **App** is a packaged collection of dashboards and reports shared with users.
- Published from a workspace → Click **Publish App** → Configure settings → Share with audience.

## 20. What are some key benefits of using the Power BI Online Service in enterprise environments?
- Centralized sharing & collaboration
- Scheduled refresh & data governance
- Row-level security for sensitive data
- Mobile access & optimized views
- Scalability with Premium capacity
