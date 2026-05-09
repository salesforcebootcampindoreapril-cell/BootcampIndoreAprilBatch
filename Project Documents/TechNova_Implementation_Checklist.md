# TechNova Solutions - Salesforce Bootcamp Implementation Checklist

## Project Overview
Building a complete Salesforce CRM for TechNova Solutions - a fictional IT consulting company with 150 employees across 4 departments.

---

## WEEK 1: Salesforce Ecosystem & Org Fundamentals ☐

### Task 1.1 - Developer Org Registration & Setup ☐
- [ ] Sign up for free Salesforce Developer Org at developer.salesforce.com
- [ ] Verify email and complete initial login
- [ ] Update username format: firstname.technova@bootcamp.indr
- [ ] Document org credentials securely

### Task 1.2 - Configure TechNova Company Profile ☐
- [ ] Navigate to Setup → Company Settings → Company Information
- [ ] Company Name: TechNova Solutions BV
- [ ] Primary Contact: Your name
- [ ] Address: Indore, Madhya Pradesh, India
- [ ] Phone: +91 8712687126
- [ ] Default Currency: USD
- [ ] Language: English
- [ ] Locale: English (USA)
- [ ] Time Zone: IST (Asia/Kolkata +5:30)
- [ ] Fiscal Year Start: April

### Task 1.3 - Configure Business Hours ☐
- [ ] Navigate to Setup → Company Settings → Business Hours
- [ ] Create "TechNova Standard Hours"
- [ ] Monday to Friday: 08:00 – 18:00 CET
- [ ] Saturday & Sunday: Closed
- [ ] Set as Default Business Hours

### Task 1.4 - Build TechNova's Custom App ☐
- [ ] Navigate to Setup → App Manager → New Lightning App
- [ ] App Name: TechNova CRM
- [ ] Description: Internal CRM for TechNova Solutions BV
- [ ] App Branding Color: #0070D2
- [ ] Navigation Style: Standard Navigation
- [ ] Add Utility Items: History, Notes
- [ ] Add tabs: Home, Accounts, Contacts, Opportunities, Cases, Reports, Dashboards

### Task 1.5 - Create 3 Custom Object Tabs ☐
- [ ] Create Custom Object: Project (Label: Project | Plural: Projects)
- [ ] Create Custom Object: Client (Label: Client | Plural: Clients)
- [ ] Create Custom Object: Deliverable (Label: Deliverable | Plural: Deliverables)
- [ ] Create Custom Tab for Project (Icon: Briefcase)
- [ ] Create Custom Tab for Client (Icon: Building)
- [ ] Create Custom Tab for Deliverable (Icon: Checklist)
- [ ] Add all 3 tabs to TechNova CRM App

### Task 1.6 - Explore & Document Setup Navigation ☐
- [ ] Explore Setup menu for 20 minutes
- [ ] Create "TechNova Setup Exploration Notes" document
- [ ] Document 10 Setup sections with descriptions and relevance

---

## WEEK 2: Data Model, Objects & Relationships ☐

### Task 2.1 - Extend Project Object with Custom Fields ☐
- [ ] Project_Name__c (Text 80, Required)
- [ ] Project_Code__c (Text 20, Unique, External ID)
- [ ] Start_Date__c (Date, Required)
- [ ] End_Date__c (Date)
- [ ] Status__c (Picklist: Planning, Active, On Hold, Completed, Cancelled)
- [ ] Budget__c (Currency 16,2)
- [ ] Actual_Cost__c (Currency 16,2)
- [ ] Budget_Variance__c (Formula: Budget__c - Actual_Cost__c)
- [ ] Priority__c (Picklist: Low, Medium, High, Critical)
- [ ] Completion_Percentage__c (Percent 3,0)
- [ ] Project_Description__c (Long Text Area 5000)
- [ ] Is_Billable__c (Checkbox, Default: True)

### Task 2.2 - Extend Client Object with Custom Fields ☐
- [ ] Client_Name__c (Text 100, Required)
- [ ] Client_Code__c (Text 20, Unique)
- [ ] Industry__c (Picklist: Technology, Finance, Healthcare, Retail, Manufacturing, Other)
- [ ] Country__c (Picklist: Netherlands, Germany, Belgium, UK, France, Other)
- [ ] Annual_Revenue__c (Currency)
- [ ] Client_Tier__c (Picklist: Platinum, Gold, Silver, Bronze)
- [ ] Account_Manager__c (Lookup to User)
- [ ] Contract_Start__c (Date)
- [ ] Contract_End__c (Date)
- [ ] Is_Active__c (Checkbox, Default: True)
- [ ] Total_Projects__c (Roll-Up Summary - Count of Projects)
- [ ] Website__c (URL)

### Task 2.3 - Extend Deliverable Object & Build Relationships ☐
**Step A - Add Fields:**
- [ ] Deliverable_Name__c (Text 100, Required)
- [ ] Description__c (Long Text Area 2000)
- [ ] Due_Date__c (Date, Required)
- [ ] Status__c (Picklist: Not Started, In Progress, Under Review, Completed, Blocked)
- [ ] Assigned_To__c (Lookup to User)
- [ ] Estimated_Hours__c (Number 4,1)
- [ ] Actual_Hours__c (Number 4,1)
- [ ] Hours_Variance__c (Formula: Estimated_Hours__c - Actual_Hours__c)
- [ ] Completion_Notes__c (Long Text Area 2000)

**Step B - Build Relationships:**
- [ ] Client → Project (Master-Detail, Field Name: Client)
- [ ] Project → Deliverable (Master-Detail, Field Name: Project)
- [ ] Project → Account (Lookup, Field Name: Associated Account)

**Step C - Roll-Up Summary:**
- [ ] Verify Total_Projects__c on Client counts related Projects

### Task 2.4 - Create Resource Object ☐
- [ ] Create Resource object
- [ ] Name (Auto Number: RES-{0000})
- [ ] Employee__c (Lookup to User, Required)
- [ ] Role__c (Picklist: Project Manager, Developer, Designer, Analyst, Tester, Consultant)
- [ ] Daily_Rate__c (Currency)
- [ ] Availability__c (Percent)
- [ ] Skills__c (Text Area 500)
- [ ] Create Project Resource Junction Object
- [ ] Project (Master-Detail to Project)
- [ ] Resource (Master-Detail to Resource)
- [ ] Allocation % (Percent)
- [ ] Start Date (Date)
- [ ] End Date (Date)

### Task 2.5 - Configure Record Types ☐
- [ ] Create Record Type: Internal Project
- [ ] Create Record Type: Client Project
- [ ] Create Internal Project Layout (hide Budget/Billing fields)
- [ ] Create Client Project Layout (show all fields)

### Task 2.6 - Schema Builder Diagram ☐
- [ ] Open Schema Builder
- [ ] Add all custom objects: Project, Client, Deliverable, Resource, Project Resource
- [ ] Add standard objects: Account, Contact, User
- [ ] Arrange objects to show relationships clearly
- [ ] Take screenshot of complete diagram

---

## WEEK 3: Security Model & User Management ☐

### Task 3.1 - Design Security Architecture Document ☐
- [ ] Create Security Design Document (1-2 pages)
- [ ] Section A: Department Overview (Sales, Delivery, Operations, Support)
- [ ] Section B: Access Matrix for all objects
- [ ] Document reasoning for access decisions

### Task 3.2 - Configure Org-Wide Defaults ☐
- [ ] Account: Private
- [ ] Contact: Private
- [ ] Opportunity: Private
- [ ] Project__c: Private
- [ ] Client__c: Public Read Only
- [ ] Case: Private

### Task 3.3 - Build Role Hierarchy ☐
- [ ] CEO: TechNova Solutions BV
- [ ] Sales Director → Senior Sales Manager → Sales Executive
- [ ] Delivery Director → Senior Project Manager → Project Manager
- [ ] Operations Manager → Operations Analyst
- [ ] Support Manager → Senior Support Agent → Support Agent

### Task 3.4 - Create Custom Profiles ☐
- [ ] TechNova Sales User (clone Standard User)
- [ ] TechNova Delivery User (clone Standard User)
- [ ] TechNova Operations User (clone Standard User)
- [ ] TechNova Support User (clone Standard User)
- [ ] Configure Object Permissions per Access Matrix
- [ ] Configure Tab Visibility per profile

### Task 3.5 - Create Salesforce Users ☐
- [ ] Alice van Berg (alice.technova.test@bootcamp.nl, Sales User, Sales Executive)
- [ ] Bob de Vries (bob.technova.test@bootcamp.nl, Sales User, Senior Sales Manager)
- [ ] Clara Smit (clara.technova.test@bootcamp.nl, Delivery User, Project Manager)
- [ ] David Bakker (david.technova.test@bootcamp.nl, Delivery User, Senior Project Manager)
- [ ] Eva Jansen (eva.technova.test@bootcamp.nl, Operations User, Operations Analyst)
- [ ] Frank Visser (frank.technova.test@bootcamp.nl, Operations User, Operations Manager)
- [ ] Grace Meijer (grace.technova.test@bootcamp.nl, Support User, Support Agent)
- [ ] Hans Mulder (hans.technova.test@bootcamp.nl, Support User, Senior Support Agent)

### Task 3.6 - Create Permission Sets ☐
- [ ] Project Dashboard Viewer (Read Project & Deliverable, Project tab)
- [ ] Client Data Manager (Read/Write/Delete Client, edit Annual Revenue & Client Tier)
- [ ] Assign Project Dashboard Viewer to Alice & Bob
- [ ] Assign Client Data Manager to Eva

### Task 3.7 - Configure Sharing Rules ☐
- [ ] Sales Team Project Visibility (Share Senior PM projects with Sales Director)
- [ ] Support Team Client Access (Share Active Clients with Support Manager)

### Task 3.8 - Configure Field-Level Security ☐
- [ ] Client.Annual_Revenue__c (Hidden for Sales, Delivery, Support | Visible+Editable for Operations)
- [ ] Client.Client_Tier__c (Visible for Sales | Hidden for Delivery, Support | Visible+Editable for Operations)
- [ ] Project.Budget__c (Hidden for Sales, Support | Visible for Delivery | Visible+Editable for Operations)
- [ ] Project.Actual_Cost__c (Hidden for Sales, Support | Visible for Delivery | Visible+Editable for Operations)

### Task 3.9 - Test & Validate Security Model ☐
- [ ] Login as Alice van Berg (Sales Executive)
- [ ] Login as Clara Smit (Project Manager)
- [ ] Login as Grace Meijer (Support Agent)
- [ ] Document visible tabs, accessible objects, visible/hidden fields
- [ ] Create Security Validation Report

---

## WEEK 4: Automation Tools: Flow Builder ☐

### Task 4.1 - Flow 1: Auto-Assign Project Manager ☐
- [ ] Flow Type: Record-Triggered (After Save)
- [ ] Trigger: Project created
- [ ] Conditions: Record Type = Client Project, PM is NULL
- [ ] Get Records: User where Name = "David Bakker"
- [ ] Update Records: Set Project Manager
- [ ] Create Chatter post notification
- [ ] Activate flow

### Task 4.2 - Flow 2: Project Status Change Notification ☐
- [ ] Flow Type: Record-Triggered (Before + After Save)
- [ ] Trigger: Project updated
- [ ] Conditions: Status changed to Completed or Cancelled
- [ ] Before Save: Set End Date = Today
- [ ] Get Records: All Project Resources
- [ ] Loop through resources
- [ ] Send email to each resource
- [ ] Activate flow

### Task 4.3 - Flow 3: Client Onboarding Screen Flow ☐
- [ ] Flow Type: Screen Flow
- [ ] Screen 1: Basic Info (Name, Industry, Country, Website)
- [ ] Screen 2: Contract Details (Tier, Dates, Revenue)
- [ ] Screen 3: Confirmation summary
- [ ] Create Client record
- [ ] Set Is_Active = True
- [ ] Navigate to new record
- [ ] Create Quick Action button
- [ ] Activate flow

### Task 4.4 - Flow 4: Overdue Deliverable Escalation ☐
- [ ] Flow Type: Scheduled Flow
- [ ] Schedule: Every Monday 08:00 AM
- [ ] Get Records: Overdue deliverables (Due Date < TODAY, Status = In Progress or Not Started)
- [ ] Loop through deliverables
- [ ] Update Status = "Blocked"
- [ ] Get Project Manager
- [ ] Send escalation email
- [ ] Activate flow

### Task 4.5 - Flow 5: Budget Overspend Alert ☐
- [ ] Flow Type: Record-Triggered (After Save)
- [ ] Trigger: Project updated
- [ ] Conditions: Actual_Cost > Budget
- [ ] Decision: Budget_Variance < 0
- [ ] Update Status = "On Hold"
- [ ] Get User: Frank Visser
- [ ] Create Chatter post with @mention
- [ ] Activate flow

### Testing ☐
- [ ] Test each flow with documented scenarios
- [ ] Verify all 5 flows are Active

---

## WEEK 5: Reports, Dashboards & Data Management ☐

### Task 5.1 - Import Sample Data ☐
- [ ] Import 10 Client records (mix of tiers)
- [ ] Import 15 Project records (mix of statuses)
- [ ] Import 30 Deliverable records
- [ ] Import 5 Resource records

### Task 5.2 - Build 6 Reports ☐
- [ ] Report 1: Project Pipeline Summary (Summary by Status)
- [ ] Report 2: Overdue Deliverables (Tabular)
- [ ] Report 3: Client Portfolio by Tier (Summary)
- [ ] Report 4: Budget vs Actual by Project (Matrix with conditional highlighting)
- [ ] Report 5: Resource Allocation Overview (Summary)
- [ ] Report 6: Weekly Deliverable Completion Rate (Summary with Donut chart)
- [ ] Save all in "TechNova Reports" folder

### Task 5.3 - Build TechNova Leadership Dashboard ☐
- [ ] Create "TechNova Executive Overview" dashboard
- [ ] Running User: Frank Visser
- [ ] Component 1: Project Status Breakdown (Donut)
- [ ] Component 2: Budget vs Actual by Client (Grouped Bar)
- [ ] Component 3: Overdue Deliverables Count (Metric)
- [ ] Component 4: Client Tier Distribution (Funnel)
- [ ] Component 5: Total Active Budget (Metric)
- [ ] Component 6: Resource Allocation Heat (Stacked Bar)
- [ ] Component 7: Deliverable Completion Rate (Donut)
- [ ] Component 8: Top 5 Clients by Revenue (Bar)
- [ ] Arrange in specified layout

### Task 5.4 - Configure Duplicate Management ☐
- [ ] Client Duplicate Rule (Name + Website fuzzy match, Allow with Warning)
- [ ] Project Duplicate Rule (Project Code exact match, Block)

### Task 5.5 - Schedule Weekly Report Email ☐
- [ ] Schedule "Overdue Deliverables" report
- [ ] Every Monday 07:00 AM CET
- [ ] Recipients: Frank Visser, David Bakker
- [ ] Format: Excel

---

## WEEK 6: Lightning App Builder, AppExchange & Deployment ☐

### Task 6.1 - Redesign Project Record Page ☐
- [ ] Open Lightning App Builder for Project
- [ ] Left Column (70%): Dynamic Form with 3 tabs (Overview, Financials, Timeline)
- [ ] Add Related Lists: Deliverables, Project Resources
- [ ] Add Chatter Feed
- [ ] Right Column (30%): Highlights Panel, Activity Timeline, Report Chart
- [ ] Configure Dynamic Form rules (show Financials only for Client Projects)
- [ ] Apply conditional styling (Budget Variance red if < 0)

### Task 6.2 - Configure Dynamic Actions ☐
- [ ] Remove standard buttons
- [ ] Edit (always show)
- [ ] Delete (only Operations User)
- [ ] Mark as Complete (only if Status = Active)
- [ ] Escalate to Management (only if Priority = Critical)
- [ ] Clone (always show)
- [ ] Change Status (always show)
- [ ] Create Quick Action: Mark as Complete
- [ ] Create Quick Action: Change Status

### Task 6.3 - Redesign Client Record Page ☐
- [ ] Top Banner: Highlights Panel
- [ ] Left Column (60%): Dynamic Form (all Client fields)
- [ ] Add Related Lists: Projects, Contacts
- [ ] Right Column (40%): Report Chart (Clients by Tier)
- [ ] Add Activity Timeline
- [ ] Add Notes & Attachments
- [ ] Dynamic Form Rule: Show Annual Revenue only if Profile = Operations User
- [ ] Dynamic Form Rule: Show Contract fields only if Is_Active = True

### Task 6.4 - AppExchange Installation & Evaluation ☐
- [ ] Navigate to AppExchange
- [ ] Search and install "Salesforce Adoption Dashboards" (Free)
- [ ] Install for Admins Only
- [ ] Explore 3 dashboards/reports
- [ ] Identify which TechNova users benefit
- [ ] Write Evaluation Report (1 page) covering:
  - What does the package do?
  - Most valuable dashboards for TechNova
  - Limitations
  - Recommendation for production deployment
  - Security considerations

### Task 6.5 - Create and Document Change Set ☐
- [ ] Navigate to Setup → Outbound Change Sets
- [ ] Create "TechNova Week 6 Deployment" Change Set
- [ ] Add 10 components:
  - Project__c object
  - Client__c object
  - Deliverable__c object
  - TechNova CRM application
  - Auto Assign Project Manager flow
  - Client Onboarding Screen Flow
  - Project Record Page
  - Client Record Page
  - TechNova Sales User profile
  - TechNova Operations User profile
- [ ] Take screenshot of Change Set
- [ ] Write Deployment Notes document (half page):
  - What is being deployed
  - Target org prerequisites
  - Manual post-deployment steps
  - Rollback plan

---

## PROJECT COMPLETION SUMMARY

### Total Task Count
- **Week 1:** 6 major tasks with 25+ sub-tasks
- **Week 2:** 6 major tasks with 50+ sub-tasks
- **Week 3:** 9 major tasks with 45+ sub-tasks
- **Week 4:** 5 flows with full testing
- **Week 5:** 5 major tasks (reports, dashboards, data management)
- **Week 6:** 5 major tasks (UI/UX, AppExchange, deployment)

**GRAND TOTAL: 36 major tasks with 180+ actionable sub-tasks**

### Deliverables by Week

**Week 1 Deliverables:**
- Configured Salesforce Developer Org
- TechNova CRM Lightning App
- 3 Custom Objects with Tabs
- Setup Exploration Notes document

**Week 2 Deliverables:**
- Complete data model (5 custom objects)
- 50+ custom fields
- Master-Detail and Lookup relationships
- Roll-Up Summary fields
- 2 Record Types with page layouts
- Schema Builder diagram

**Week 3 Deliverables:**
- Security Architecture Document
- Configured OWD for 6 objects
- 10-role hierarchy
- 4 custom profiles
- 8 test users
- 2 permission sets
- 2 sharing rules
- Field-Level Security configuration
- Security Validation Report

**Week 4 Deliverables:**
- 5 production-ready Flows:
  1. Auto-Assign Project Manager
  2. Project Status Change Notification
  3. Client Onboarding Screen Flow
  4. Overdue Deliverable Escalation (Scheduled)
  5. Budget Overspend Alert
- Flow testing documentation

**Week 5 Deliverables:**
- Sample data (65+ records)
- 6 custom reports
- Executive Dashboard with 8 components
- 2 duplicate rules
- Scheduled weekly report email

**Week 6 Deliverables:**
- Redesigned Project Record Page (Dynamic Forms)
- Redesigned Client Record Page
- 2 Quick Actions
- Dynamic Actions configuration
- AppExchange package evaluation
- Change Set with 10 components
- Deployment Notes document

---

## SUCCESS CRITERIA

Your TechNova Salesforce org is complete when:

✅ **Functionality:** All 36 tasks completed across 6 weeks  
✅ **Data Model:** 5 custom objects with relationships working  
✅ **Security:** 4 profiles, 10 roles, sharing rules active  
✅ **Automation:** All 5 flows active and tested  
✅ **Analytics:** 6 reports + 1 dashboard with live data  
✅ **UX:** Redesigned record pages with Dynamic Forms  
✅ **Documentation:** All required documents submitted  

---

## NOTES & TIPS

### Week-by-Week Priority
1. **Week 1 & 2 are foundational** - Complete these first before moving forward
2. **Week 3 builds on Week 2** - Security requires objects to exist
3. **Week 4 requires Weeks 1-3** - Flows need objects, fields, and users
4. **Week 5 requires data** - Can't build reports without records
5. **Week 6 polishes everything** - Final UX improvements

### Common Pitfalls to Avoid
- Don't skip the Schema Builder diagram (Task 2.6)
- Test security with "Login As" feature thoroughly
- Activate all flows before considering Week 4 complete
- Import varied sample data (different statuses, tiers, dates)
- Take screenshots at key milestones for documentation

### Time Estimates
- Week 1: 3-4 hours
- Week 2: 5-6 hours (most complex)
- Week 3: 4-5 hours
- Week 4: 4-5 hours (flow building)
- Week 5: 3-4 hours
- Week 6: 3-4 hours

**Total estimated time: 22-28 hours**

---

## SUBMISSION CHECKLIST

Before final submission, verify:

- [ ] All 36 tasks marked complete
- [ ] All flows are Active status
- [ ] All 8 test users created and functional
- [ ] Dashboard displays data correctly
- [ ] All documentation files created:
  - [ ] Setup Exploration Notes
  - [ ] Security Architecture Document
  - [ ] Security Validation Report
  - [ ] Flow testing documentation
  - [ ] AppExchange Evaluation Report
  - [ ] Deployment Notes
- [ ] Schema Builder screenshot saved
- [ ] Change Set screenshot saved
- [ ] Org credentials documented securely

---

**End of TechNova Implementation Checklist**
