# TechNova Solutions - Quick Reference Guide

## 🎯 Project At A Glance

**Company:** TechNova Solutions BV  
**Location:** Indore, Madhya Pradesh, India  
**Employees:** 150 across 4 departments  
**Project Duration:** 6 weeks  
**Total Tasks:** 36 major tasks with 180+ sub-tasks  
**Estimated Time:** 22-28 hours  

---

## 📋 Week-by-Week Summary

### WEEK 1: Foundation Setup (3-4 hours)
**Goal:** Set up basic Salesforce environment

**Key Deliverables:**
- Developer Org configured
- TechNova CRM app created
- 3 custom objects: Project, Client, Deliverable
- Custom tabs with icons (Briefcase, Building, Checklist)

**Critical Settings:**
- Currency: USD
- Timezone: IST (Asia/Kolkata +5:30)
- Fiscal Year: April start
- Business Hours: Mon-Fri 08:00-18:00 CET

---

### WEEK 2: Data Model (5-6 hours) ⚠️ MOST COMPLEX
**Goal:** Build complete data architecture

**Key Objects & Field Counts:**
- **Project:** 12 fields (includes Budget Variance formula)
- **Client:** 12 fields (includes Total Projects roll-up)
- **Deliverable:** 9 fields (includes Hours Variance formula)
- **Resource:** 6 fields (auto-number: RES-{0000})
- **Project Resource:** Junction object (5 fields)

**Critical Relationships:**
- Client → Project (Master-Detail)
- Project → Deliverable (Master-Detail)
- Project → Account (Lookup)
- Project ↔ Resource (Many-to-Many via junction)

**Record Types:**
- Internal Project (hide Budget/Billing fields)
- Client Project (show all fields)

---

### WEEK 3: Security (4-5 hours)
**Goal:** Implement layered security model

**Role Hierarchy (10 roles):**
```
CEO
├── Sales Director → Sr Sales Mgr → Sales Exec
├── Delivery Director → Sr PM → PM
├── Operations Mgr → Operations Analyst
└── Support Mgr → Sr Support Agent → Support Agent
```

**4 Custom Profiles:**
1. TechNova Sales User
2. TechNova Delivery User
3. TechNova Operations User
4. TechNova Support User

**8 Test Users:**
- Alice van Berg (Sales Executive)
- Bob de Vries (Senior Sales Manager)
- Clara Smit (Project Manager)
- David Bakker (Senior Project Manager)
- Eva Jansen (Operations Analyst)
- Frank Visser (Operations Manager)
- Grace Meijer (Support Agent)
- Hans Mulder (Senior Support Agent)

**OWD Configuration:**
- Account, Contact, Opportunity, Project, Case: **Private**
- Client: **Public Read Only**

---

### WEEK 4: Automation (4-5 hours)
**Goal:** Build 5 production-ready Flows

**Flow 1:** Auto-Assign PM (Record-Triggered)
- Assigns David Bakker to new Client Projects
- Creates Chatter notification

**Flow 2:** Status Change Notification (Record-Triggered)
- Stamps End Date when Completed/Cancelled
- Emails all Project Resources

**Flow 3:** Client Onboarding (Screen Flow)
- 3 screens: Basic Info → Contract → Confirmation
- Creates Client and redirects to record

**Flow 4:** Overdue Escalation (Scheduled)
- Runs every Monday 08:00 AM
- Blocks overdue deliverables
- Emails Project Managers

**Flow 5:** Budget Overspend Alert (Record-Triggered)
- Updates Status to "On Hold"
- Creates Chatter post with @Frank Visser

---

### WEEK 5: Analytics (3-4 hours)
**Goal:** Build reports and executive dashboard

**Sample Data Required:**
- 10 Clients (mix of Platinum, Gold, Silver, Bronze)
- 15 Projects (various statuses)
- 30 Deliverables
- 5 Resources

**6 Reports:**
1. Project Pipeline Summary (Summary)
2. Overdue Deliverables (Tabular)
3. Client Portfolio by Tier (Summary)
4. Budget vs Actual (Matrix + conditional highlighting)
5. Resource Allocation (Summary)
6. Deliverable Completion Rate (Summary + Donut)

**Executive Dashboard:** 8 components
- Running User: Frank Visser
- Layout: Metrics → Charts → Large visuals

**Automation:**
- Weekly email: Overdue Deliverables (Mon 07:00)
- 2 Duplicate Rules (Client + Project)

---

### WEEK 6: Polish & Deploy (3-4 hours)
**Goal:** Optimize UX and prepare deployment

**Project Record Page:**
- Dynamic Form with 3 tabs (Overview, Financials, Timeline)
- Left 70% / Right 30% layout
- Show Financials only for Client Projects

**Client Record Page:**
- Dynamic Form with conditional visibility
- Show Annual Revenue only for Operations Users
- Show Contract fields only if Is_Active = True

**Dynamic Actions:**
- Edit (always)
- Delete (Operations only)
- Mark Complete (if Status = Active)
- Escalate (if Priority = Critical)
- Clone, Change Status (always)

**AppExchange:**
- Install "Salesforce Adoption Dashboards"
- Write evaluation report

**Change Set:**
- 10 components ready for deployment
- Deployment notes documented

---

## 🔑 Key Field API Names Reference

### Project Object
- `Project_Name__c`
- `Project_Code__c`
- `Status__c`
- `Budget__c`
- `Actual_Cost__c`
- `Budget_Variance__c` (Formula)
- `Priority__c`
- `Completion_Percentage__c`
- `Is_Billable__c`

### Client Object
- `Client_Name__c`
- `Client_Code__c`
- `Industry__c`
- `Country__c`
- `Client_Tier__c`
- `Account_Manager__c` (Lookup)
- `Contract_Start__c`
- `Contract_End__c`
- `Is_Active__c`
- `Total_Projects__c` (Roll-Up)
- `Annual_Revenue__c`

### Deliverable Object
- `Deliverable_Name__c`
- `Due_Date__c`
- `Status__c`
- `Assigned_To__c` (Lookup)
- `Estimated_Hours__c`
- `Actual_Hours__c`
- `Hours_Variance__c` (Formula)

### Resource Object
- `Employee__c` (Lookup to User)
- `Role__c`
- `Daily_Rate__c`
- `Availability__c`
- `Skills__c`

---

## 📊 Picklist Values Reference

### Project.Status__c
- Planning
- Active
- On Hold
- Completed
- Cancelled

### Project.Priority__c
- Low
- Medium
- High
- Critical

### Client.Industry__c
- Technology
- Finance
- Healthcare
- Retail
- Manufacturing
- Other

### Client.Country__c
- Netherlands
- Germany
- Belgium
- UK
- France
- Other

### Client.Client_Tier__c
- Platinum
- Gold
- Silver
- Bronze

### Deliverable.Status__c
- Not Started
- In Progress
- Under Review
- Completed
- Blocked

### Resource.Role__c
- Project Manager
- Developer
- Designer
- Analyst
- Tester
- Consultant

---

## ⚠️ Common Pitfalls & Solutions

### Week 1
**Issue:** Username format confusion  
**Solution:** Use `firstname.technova@bootcamp.indr` (note: .indr not .nl)

### Week 2
**Issue:** Master-Detail relationship order matters  
**Solution:** Create Client → Project BEFORE Project → Deliverable

**Issue:** Roll-Up Summary not working  
**Solution:** Ensure Master-Detail relationship exists first

**Issue:** Formula fields showing errors  
**Solution:** Check field API names match exactly (include `__c`)

### Week 3
**Issue:** Users can't see data after profile creation  
**Solution:** Check OWD, Sharing Rules, and FLS settings in that order

**Issue:** Field-Level Security seems backwards  
**Solution:** Hidden = checkbox UNCHECKED, Visible = checkbox CHECKED

### Week 4
**Issue:** Flow fails on save  
**Solution:** Check all required fields have values before Update

**Issue:** Scheduled Flow not appearing in monitoring  
**Solution:** Must activate flow AND set schedule frequency

**Issue:** Loop not iterating  
**Solution:** Verify Collection variable is properly assigned from Get Records

### Week 5
**Issue:** Reports show no data  
**Solution:** Import sample data first (Task 5.1)

**Issue:** Dashboard components blank  
**Solution:** Check report filters and ensure records match criteria

**Issue:** Matrix report looks wrong  
**Solution:** Verify Row Grouping and Column Grouping are correct objects

### Week 6
**Issue:** Dynamic Form tabs not showing  
**Solution:** Ensure Record Type or field values match visibility rules

**Issue:** Dynamic Actions not appearing  
**Solution:** Check profile permissions and field values match conditions

---

## ✅ Pre-Submission Checklist

### Documentation Files Required
- [ ] Setup Exploration Notes (10 sections)
- [ ] Security Architecture Document (1-2 pages)
- [ ] Security Validation Report (table format)
- [ ] Flow Testing Documentation (5 scenarios)
- [ ] AppExchange Evaluation Report (1 page)
- [ ] Deployment Notes (half page)

### Screenshots Required
- [ ] Schema Builder diagram (all objects visible)
- [ ] Change Set component list (10 components)
- [ ] Dashboard layout (optional but helpful)

### System Verification
- [ ] All 5 flows show "Active" status
- [ ] All 8 users can log in successfully
- [ ] Dashboard loads without errors
- [ ] Reports return data
- [ ] Sample data imported (65+ records)

### Metadata Counts
- [ ] 5 Custom Objects
- [ ] 50+ Custom Fields
- [ ] 4 Custom Profiles
- [ ] 10 Roles
- [ ] 8 Active Users
- [ ] 2 Permission Sets
- [ ] 2 Sharing Rules
- [ ] 5 Active Flows
- [ ] 6 Reports
- [ ] 1 Dashboard (8 components)
- [ ] 2 Record Types
- [ ] 3 Custom Tabs

---

## 🚀 Success Tips

1. **Complete weeks sequentially** - Each builds on the previous
2. **Test as you go** - Don't wait until the end
3. **Take screenshots early** - Easier to retake than remember
4. **Document decisions** - Why you chose certain settings
5. **Use Login As feature** - Essential for security testing
6. **Keep credentials safe** - You'll need them throughout
7. **Ask questions early** - Don't get stuck for hours
8. **Back up your work** - Use Change Sets or SFDX periodically

---

## 📞 Key Contacts (Fictional Test Users)

**Delivery Team:**
- David Bakker (Senior PM) - Main project manager contact
- Clara Smit (PM) - Secondary project manager

**Operations Team:**
- Frank Visser (Ops Manager) - Main admin/ops contact
- Eva Jansen (Analyst) - Data management

**Sales Team:**
- Bob de Vries (Senior Sales Manager)
- Alice van Berg (Sales Executive)

**Support Team:**
- Hans Mulder (Senior Support Agent)
- Grace Meijer (Support Agent)

---

**Last Updated:** Week 0 - Planning Phase  
**Next Milestone:** Week 1 Completion  
**Status:** Ready to Begin Implementation