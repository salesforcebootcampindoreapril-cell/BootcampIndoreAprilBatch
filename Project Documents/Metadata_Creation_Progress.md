# TechNova Solutions - Metadata Creation Progress

## Week 2 - Data Model, Objects & Relationships ✅ COMPLETE

### Task 2.4 - Resource Object ✅
- [x] Resource__c object created with Auto-Number name field (RES-{0000})
- [x] Employee__c (Lookup to User, Required)
- [x] Role__c (Picklist: Project Manager, Developer, Designer, Analyst, Tester, Consultant)
- [x] Daily_Rate__c (Currency)
- [x] Availability__c (Percent)
- [x] Skills__c (Text Area 500)

### Task 2.4 - Project Resource Junction Object ✅
- [x] Project_Resource__c object created with Auto-Number name (PR-{0000})
- [x] Sharing Model: ControlledByParent
- [x] Project__c (Master-Detail to Project__c) - relationshipOrder 0
- [x] Resource__c (Master-Detail to Resource__c) - relationshipOrder 1
- [x] Allocation_Percent__c (Percent field)
- [x] Start_Date__c (Date field)
- [x] End_Date__c (Date field)

**Junction Object Complete:** Creates Many-to-Many relationship between Projects and Resources

### Task 2.5 - Record Types ✅
- [x] Internal_Project record type created (for internal TechNova initiatives)
- [x] Client_Project record type created (for billable client work)
- [x] Internal Project Layout created (hides Budget and Billing fields)
- [x] Client Project Layout created (shows all fields including Budget Variance)

**Key Differences:**
- Internal Project Layout: No Budget, Actual_Cost, Budget_Variance, Is_Billable fields
- Client Project Layout: All financial fields visible including Budget Variance (readonly)

### Task 2.6 - Schema Builder Diagram
- [ ] To be created after deployment to org (requires Schema Builder UI)

---

## Week 2 Summary - Files Created: 67

### Objects (5):
1. Project__c
2. Client__c  
3. Deliverable__c
4. Resource__c
5. Project_Resource__c (Junction)

### Fields Total: 52
- Project__c: 13 fields
- Client__c: 12 fields
- Deliverable__c: 10 fields
- Resource__c: 6 fields
- Project_Resource__c: 5 fields

### Relationships (4):
1. Client → Project (Master-Detail)
2. Project → Deliverable (Master-Detail)
3. Project → Account (Lookup)
4. Project ↔ Resource (Many-to-Many via Project_Resource__c junction)

### Record Types & Layouts (4):
1. Internal_Project record type
2. Client_Project record type
3. Internal Project Layout
4. Client Project Layout

---

## Next: Week 3 - Security Model & User Management

### Planned Tasks:
1. **Task 3.2** - Configure Org-Wide Defaults (6 objects)
2. **Task 3.3** - Build Role Hierarchy (10 roles)
3. **Task 3.4** - Create Custom Profiles (4 profiles)
4. **Task 3.5** - Create 8 Test Users
5. **Task 3.6** - Create 2 Permission Sets
6. **Task 3.7** - Configure 2 Sharing Rules
7. **Task 3.8** - Configure Field-Level Security

**Note:** Week 3 tasks require manual configuration in the Salesforce UI and cannot be fully completed via metadata files alone. Some security settings (OWD, Role Hierarchy, FLS) require org setup.

---

## Deployment Status

**Ready for Deployment:** Week 1 + Week 2 metadata (67 files total)

**Command to deploy:**
```bash
sf project deploy start --source-dir force-app/main/default
```

**Post-Deployment Steps:**
1. Verify all objects and fields are created
2. Check Master-Detail relationships
3. Verify Roll-Up Summary field on Client__c
4. Test Record Types on Project__c
5. Create Schema Builder diagram (Task 2.6)