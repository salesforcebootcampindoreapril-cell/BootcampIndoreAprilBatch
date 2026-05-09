# Week 3 - Security Model Implementation Guide

## ⚠️ Important Notice

**Week 3 security configuration requires MANUAL setup in the Salesforce UI.** Most security settings cannot be deployed via metadata files in a Developer Org without proper org connections. This document provides the complete implementation guide for manual configuration.

---

## What CAN Be Done via Metadata (Limited)

### ✅ Profiles (Partial)
- Can create profile metadata files
- **LIMITATION:** Profile permissions require the org to already have the objects/fields deployed
- Must be configured manually in Setup → Profiles after objects exist

### ❌ What CANNOT Be Done via Metadata

1. **Org-Wide Defaults (OWD)** - Must be configured manually in Setup → Sharing Settings
2. **Role Hierarchy** - Must be built manually in Setup → Roles  
3. **Users** - Cannot create users via metadata (requires UI or API)
4. **Permission Set Assignments** - Cannot assign via metadata
5. **Sharing Rules** - Must be configured manually in Setup → Sharing Settings
6. **Field-Level Security (FLS)** - Must be set in Profile/Permission Set UI

---

## Manual Implementation Steps

### Task 3.1 - Security Architecture Document

**Department Access Matrix:**

| Object | Sales | Delivery | Operations | Support |
|--------|-------|----------|------------|---------|
| **Client__c** | Read/Write | Read | Read/Write | Read |
| **Project__c** | Read | Read/Write | Read/Write | No Access |
| **Deliverable__c** | No Access | Read/Write | Read/Write | No Access |
| **Case** | Read | No Access | Read | Read/Write |
| **Resource__c** | No Access | Read | Read/Write | No Access |
| **Account** | Read/Write | Read | Read | Read |
| **Contact** | Read/Write | Read | Read | Read/Write |
| **Opportunity** | Read/Write | Read | Read | No Access |

**Reasoning:**
- Sales needs full access to Accounts, Contacts, Opportunities, and Clients to manage deals
- Delivery needs to manage Projects and Deliverables but only read Client info
- Operations needs broad read/write access to manage resources and oversee all projects
- Support needs access to Cases and Client information to resolve issues

---

### Task 3.2 - Configure Org-Wide Defaults

**Manual Steps:**
1. Navigate to: **Setup → Security → Sharing Settings**
2. Click **Edit** in the Organization-Wide Defaults section
3. Configure the following:

| Object | OWD Setting | Reasoning |
|--------|-------------|-----------|
| Account | Private | Sales teams should only see their own accounts |
| Contact | Controlled by Parent | Inherits from Account |
| Opportunity | Private | Competitive sales data must be protected |
| Case | Private | Support cases are team-specific |
| Project__c | Private | Project data is department-specific |
| Client__c | Public Read Only | All teams need to read client info |
| Deliverable__c | Controlled by Parent | Inherits from Project |
| Resource__c | Private | Resource data is sensitive |
| Project_Resource__c | Controlled by Parent | Inherits from parent relationships |

4. Click **Save**

---

### Task 3.3 - Build Role Hierarchy

**Manual Steps:**
1. Navigate to: **Setup → Roles**
2. Create roles in this order (top-down):

```
TechNova Solutions BV (CEO)
│
├── Sales Director
│   ├── Senior Sales Manager
│   └── Sales Executive
│
├── Delivery Director
│   ├── Senior Project Manager
│   └── Project Manager
│
├── Operations Manager
│   └── Operations Analyst
│
└── Support Manager
    ├── Senior Support Agent
    └── Support Agent
```

**For Each Role:**
- **Label:** [Role Name]
- **Description:** "Responsible for [department function] at TechNova Solutions"
- **Reports To:** [Parent Role]

**Example:**
- **Label:** Sales Director
- **Description:** "Responsible for client acquisition and sales strategy at TechNova Solutions"
- **Reports To:** TechNova Solutions BV (CEO)

---

### Task 3.4 - Create Custom Profiles

**Manual Steps:**

#### Profile 1: TechNova Sales User
1. Setup → Profiles → Clone "Standard User"
2. **Name:** TechNova Sales User
3. **Permissions to REMOVE:**
   - Manage Dashboards
   - Modify All Data
4. **Object Permissions:**
   - Account: Read, Create, Edit
   - Contact: Read, Create, Edit
   - Opportunity: Read, Create, Edit, Delete
   - Client__c: Read, Create, Edit
   - Project__c: Read only
   - Case: Read only

#### Profile 2: TechNova Delivery User
1. Clone "Standard User"
2. **Name:** TechNova Delivery User
3. **Permissions to REMOVE:**
   - Manage Leads
   - Edit Opportunities
4. **Object Permissions:**
   - Project__c: Read, Create, Edit, Delete
   - Deliverable__c: Read, Create, Edit, Delete
   - Resource__c: Read
   - Client__c: Read only

#### Profile 3: TechNova Operations User
1. Clone "Standard User"
2. **Name:** TechNova Operations User
3. **Permissions to ADD:**
   - View All Data
   - Manage Reports
4. **Object Permissions:**
   - All custom objects: Full access
   - Resource__c: Read, Create, Edit, Delete

#### Profile 4: TechNova Support User
1. Clone "Standard User"
2. **Name:** TechNova Support User
3. **Permissions to REMOVE:**
   - Edit Opportunities
   - Manage Campaigns
4. **Object Permissions:**
   - Case: Read, Create, Edit, Delete
   - Client__c: Read only
   - Account: Read
   - Contact: Read, Edit

---

### Task 3.5 - Create Test Users

**Manual Steps:**
1. Navigate to: **Setup → Users → New User**
2. Create these 8 users:

| Full Name | Email | Username | Profile | Role |
|-----------|-------|----------|---------|------|
| Alice van Berg | alice@technova.nl | alice.technova.test@bootcamp.nl | TechNova Sales User | Sales Executive |
| Bob de Vries | bob@technova.nl | bob.technova.test@bootcamp.nl | TechNova Sales User | Senior Sales Manager |
| Clara Smit | clara@technova.nl | clara.technova.test@bootcamp.nl | TechNova Delivery User | Project Manager |
| David Bakker | david@technova.nl | david.technova.test@bootcamp.nl | TechNova Delivery User | Senior Project Manager |
| Eva Jansen | eva@technova.nl | eva.technova.test@bootcamp.nl | TechNova Operations User | Operations Analyst |
| Frank Visser | frank@technova.nl | frank.technova.test@bootcamp.nl | TechNova Operations User | Operations Manager |
| Grace Meijer | grace@technova.nl | grace.technova.test@bootcamp.nl | TechNova Support User | Support Agent |
| Hans Mulder | hans@technova.nl | hans.technova.test@bootcamp.nl | TechNova Support User | Senior Support Agent |

**For Each User:**
- Set **User License:** Salesforce
- Set **Active:** Checked
- Set **Generate new password and notify user immediately:** Unchecked

---

### Task 3.6 - Create Permission Sets

#### Permission Set 1: Project Dashboard Viewer

**Manual Steps:**
1. Setup → Permission Sets → New
2. **Label:** Project Dashboard Viewer
3. **API Name:** Project_Dashboard_Viewer
4. **License:** None
5. **Object Settings:**
   - Project__c: Read
   - Deliverable__c: Read
6. **Tab Settings:**
   - Project__c: Default On
7. **Assignments:**
   - Assign to: Alice van Berg, Bob de Vries

#### Permission Set 2: Client Data Manager

**Manual Steps:**
1. Setup → Permission Sets → New
2. **Label:** Client Data Manager
3. **API Name:** Client_Data_Manager
4. **License:** None
5. **Object Settings:**
   - Client__c: Read, Create, Edit, Delete
6. **Field Permissions:**
   - Client__c.Annual_Revenue__c: Read, Edit
   - Client__c.Client_Tier__c: Read, Edit
7. **Assignments:**
   - Assign to: Eva Jansen

---

### Task 3.7 - Configure Sharing Rules

#### Rule 1: Sales Team Project Visibility

**Manual Steps:**
1. Setup → Sharing Settings → Project__c Sharing Rules
2. Click **New**
3. **Label:** Sales Team Project Visibility
4. **Rule Type:** Based on record owner
5. **Share records owned by:**
   - Role: Senior Project Manager
6. **Share with:**
   - Role and Subordinates: Sales Director
7. **Access Level:** Read Only
8. Click **Save**

#### Rule 2: Support Team Client Access

**Manual Steps:**
1. Setup → Sharing Settings → Client__c Sharing Rules
2. Click **New**
3. **Label:** Support Team Client Access
4. **Rule Type:** Based on criteria
5. **Criteria:**
   - Field: Is_Active__c
   - Operator: equals
   - Value: True
6. **Share with:**
   - Role and Subordinates: Support Manager
7. **Access Level:** Read Only
8. Click **Save**

---

### Task 3.8 - Configure Field-Level Security

**Manual Steps:**

For each Profile, navigate to: Setup → Profiles → [Profile Name] → Object Settings

#### TechNova Sales User:
- Client__c.Annual_Revenue__c: **Hidden**
- Client__c.Client_Tier__c: **Visible**
- Project__c.Budget__c: **Hidden**
- Project__c.Actual_Cost__c: **Hidden**

#### TechNova Delivery User:
- Client__c.Annual_Revenue__c: **Hidden**
- Client__c.Client_Tier__c: **Hidden**
- Project__c.Budget__c: **Visible**
- Project__c.Actual_Cost__c: **Visible**

#### TechNova Operations User:
- Client__c.Annual_Revenue__c: **Visible + Editable**
- Client__c.Client_Tier__c: **Visible + Editable**
- Project__c.Budget__c: **Visible + Editable**
- Project__c.Actual_Cost__c: **Visible + Editable**

#### TechNova Support User:
- Client__c.Annual_Revenue__c: **Hidden**
- Client__c.Client_Tier__c: **Hidden**
- Project__c.Budget__c: **Hidden**
- Project__c.Actual_Cost__c: **Hidden**

---

### Task 3.9 - Test & Validate Security Model

**Manual Steps:**
1. Navigate to: Setup → Users
2. Find a test user (e.g., Alice van Berg)
3. Click **Login** next to their name
4. Document:
   - Which tabs are visible
   - Which objects can be accessed
   - Which fields are visible/hidden
   - Create/Edit/Delete capabilities

**Create a validation table:**

| User | Tabs Visible | Can Access | Can Create | Can Edit | Can Delete | Fields Hidden |
|------|-------------|------------|-----------|----------|-----------|---------------|
| Alice (Sales) | Accounts, Contacts, Opportunities, Clients, Projects | Clients, Projects (Read only) | Clients, Opportunities | Clients, Opportunities | Opportunities | Annual Revenue, Budget, Actual Cost |
| Clara (Delivery) | Projects, Deliverables, Resources | Projects, Deliverables | Projects, Deliverables | Projects, Deliverables | Projects, Deliverables | Annual Revenue, Client Tier |
| Grace (Support) | Cases, Clients | Cases, Clients (Read only) | Cases | Cases, Contacts | Cases | Annual Revenue, Client Tier, Budget, Actual Cost |

---

## Week 3 Completion Checklist

- [ ] Security Architecture Document created
- [ ] OWD configured for 6+ objects
- [ ] Role Hierarchy built (10 roles)
- [ ] 4 Custom Profiles created and configured
- [ ] 8 Test Users created
- [ ] 2 Permission Sets created and assigned
- [ ] 2 Sharing Rules configured
- [ ] FLS applied on 4 fields across profiles
- [ ] Security validation testing completed

---

## Next Steps

After completing Week 3 manual configuration:
1. Test the security model with "Login As" feature
2. Verify users can only access appropriate data
3. Document any issues in Security Validation Report
4. Proceed to Week 4 (Automation/Flows)