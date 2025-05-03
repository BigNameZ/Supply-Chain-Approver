# 🚀 StockPilot - Inventory Management System with Approval Workflows

_End-to-end inventory and approval solution powered by Power Platform: Power Apps, Power Automate, and Power BI._

---

## 🌟 Key Features

- **🛒 Smart Order Submission**  
  User-friendly Power Apps interface with a shopping cart experience  
- **✅ Automated Approvals**  
  Email notifications with one-click approve/reject for managers  
- **📊 Real-Time Analytics**  
  Power BI dashboards auto-refresh from SharePoint data  
- **🔄 Inventory Sync**  
  Stock levels update instantly upon order approval  
- **🔐 Role-Based Access**  
  Tailored views for staff and managers with secure access via Azure AD  

---

## 🛠️ Technical Stack

| Component  | Technology              | Key Benefit              |
|------------|--------------------------|---------------------------|
| Frontend   | Power Apps Canvas App    | Mobile-friendly UI       |
| Backend    | SharePoint Lists         | No-code, scalable storage|
| Workflows  | Power Automate           | Streamlined approvals    |
| Analytics  | Power BI                 | Real-time, visual insights|
| Auth       | Azure AD                 | Enterprise-grade security|

---

## ✉️ Power Automate Workflows

### 📩 1. New Order Notification

- **Trigger**: On item creation in `PendingApprovals` list  
- **Recipient**: `jbigname@gmail.com`  
- **Email Template**:



ACTION REQUIRED: New Order Approval

Customer: {CustomerName}
Order ID: {Title}
Items:

{Product1} x {Qty}

{Product2} x {Qty}

Expires: {AddHours(TriggerTime, 24)}


---

### 🧾 2. Approval Processing Flow

- **Trigger**: When status changes to "Approved"  
- **Actions**:
- Decrease stock in `Inventory`
- Log approval in `ApprovedOrders`
- Send confirmation to requester
- Trigger Power BI dataset refresh  

---

## 📊 Power BI Integration

- **Dashboards**:
- *Inventory Health*: Live stock levels vs. thresholds  
- *Reorder Suggestions*: Based on low-stock indicators  
- *Approval Metrics*:  
  - Average time to approve  
  - Department-wise rejection rates  

- **Power Query Sample**:
```powerquery
Source = SharePoint.Tables("yourdomain.sharepoint.com", [ApiVersion=15]),
Inventory = Source{[Name="Inventory"]}[Data]

⚙️ Setup Guide
1. SharePoint Lists

| List               | Key Columns                | Purpose              |
| ------------------ | -------------------------- | -------------------- |
| `Inventory`        | ProductID, StockQty, Price | Tracks current stock |
| `PendingApprovals` | ProductsJSON, Status       | Approval queue       |
| `ApprovedOrders`   | ApprovedBy, ApprovalDate   | Order history log    |


3. Configure Power Automate
Import from /flows folder:

NewOrderNotification.zip

OrderApprovalProcessor.zip


