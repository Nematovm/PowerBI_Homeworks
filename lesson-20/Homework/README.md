# Lesson 20  
**Topic:** Publishing and Sharing in Power BI  
**Prerequisites:** Written brief explanations for all questions  

---

### 1. How does Power BI handle large datasets in the Online Service, and what is the role of Premium Capacity in this?  
- Power BI Online handles large datasets using **Premium Capacity**, which provides more storage, higher refresh rates, and large model support (up to 400 GB).  
- Pro users are limited in dataset size (~1 GB), while Premium allows enterprise-scale BI.  

### 2. What are the differences between Import mode, DirectQuery, and Live Connection in Power BI Service?  
- **Import mode** – data is copied into Power BI, fast performance, limited size.  
- **DirectQuery** – queries the source system live, no data stored in Power BI, slower but real-time.  
- **Live Connection** – connects directly to Analysis Services or another Power BI dataset without storing data.  

### 3. Explain deployment pipelines in Power BI Online. What stages do they include?  
- Deployment pipelines streamline the release process of content.  
- Stages: **Development → Test → Production**.  
- Ensures version control and safe promotion of reports and datasets.  

### 4. How can Power BI Service integrate with Microsoft Teams or SharePoint for collaboration?  
- Power BI reports can be embedded directly in **Teams channels** or **SharePoint Online** pages.  
- Users can view, comment, and collaborate without leaving Teams/SharePoint.  

### 5. What is the XMLA endpoint in Premium and how does it benefit developers or enterprise BI teams?  
- XMLA endpoint allows external tools (SSMS, Excel, Python, etc.) to connect to datasets.  
- Benefits: advanced querying, automation, version control, enterprise BI integration.  

### 6. Describe how usage metrics and audit logs work in Power BI Service.  
- **Usage metrics** show how often reports/dashboards are viewed and by whom.  
- **Audit logs** (via Microsoft 365 compliance center) track actions like sharing, exports, or permission changes.  

### 7. How do you manage workspace access and permissions for different users?  
- By assigning roles: **Admin, Member, Contributor, Viewer**.  
- Admins control settings; Viewers only read content.  
- Permissions can also be managed via security groups.  

### 8. How can data governance be enforced in Power BI Service?  
- Through **sensitivity labels, RLS, audit logs, certified datasets, and governance policies**.  
- Premium environments allow more strict governance with XMLA endpoints.  

### 9. What are the limitations of Row-Level Security when using DirectQuery or Live Connection?  
- Performance issues due to query complexity.  
- RLS is processed at the data source, so restrictions depend on the source system.  
- Limited support for some complex models.  

### 10. Explain how you can refresh a dataset via Power Automate or REST API.  
- **Power Automate**: Create a flow that triggers dataset refresh on schedule or event.  
- **REST API**: Use `POST /groups/{groupId}/datasets/{datasetId}/refreshes` to programmatically refresh datasets.  

---
