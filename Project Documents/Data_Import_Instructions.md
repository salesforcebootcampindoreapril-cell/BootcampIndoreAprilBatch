TechNova Sample Data Import Instructions
============================================

Summary
-------
The sfdx CLI on this machine is producing a Node module error; automated imports failed. Use the Data Import Wizard (Setup > Data > Data Import) or Data Loader to import CSVs located in the `data/` folder in this repository.

Import Order (critical)
1. Clients (Client__c) — data/Client_Import.csv
   - Use Client_Code__c as the External ID
2. Projects (Project__c) — data/Project_Import.csv
   - Map Client__c by matching Client_Code__c (use external ID mapping)
   - For RecordType, set to API names: Client_Project or Internal_Project
3. Resources (Resource__c) — data/Resource_Import.csv
   - Employee__c should be matched to User by Full Name (use Data Loader to perform lookup or pre-populate with User Ids)
4. Deliverables (Deliverable__c) — data/Deliverable_Import.csv
   - Map Project__c using Project_Code__c (external id matching)
   - Assigned_To__c should be mapped to User ID (or use username)
5. Project Resources (Project_Resource__c) — data/ProjectResource_Import.csv
   - Map Project__c by Project_Code__c (external id)
   - Map Resource__c by Resource_Name__c or Resource Auto-Number if available

Data Loader tips (recommended for exact lookup mapping)
- Export Users (Id, Name, Username) first: `SELECT Id, Name, Username FROM User WHERE IsActive = true`
- If your Resource.Employee__c expects User Id, replace Employee names in Resource_Import.csv with User.Id using a JOIN in Excel or script.
- For Projects and Deliverables, create temporary CSVs where lookup fields contain the appropriate external id values (Client_Code for Client, Project_Code for Project)

Field mapping reference (sample)
- Client__c:
  - Client_Name__c -> Client_Name__c
  - Client_Code__c -> Client_Code__c (External ID)
  - Industry__c -> Industry__c
  - Country__c -> Country__c
  - Annual_Revenue__c -> Annual_Revenue__c
  - Client_Tier__c -> Client_Tier__c
  - Contract_Start__c -> Contract_Start__c
  - Contract_End__c -> Contract_End__c
  - Is_Active__c -> Is_Active__c
  - Website__c -> Website__c

- Project__c:
  - Project_Name__c -> Project_Name__c
  - Project_Code__c -> Project_Code__c (External ID)
  - Client__c -> Client__c (map by Client_Code__c external id)
  - RecordType -> RecordTypeId (use API name mapping if Data Loader supports it)
  - Status__c -> Status__c
  - Priority__c -> Priority__c
  - Start_Date__c -> Start_Date__c
  - End_Date__c -> End_Date__c
  - Budget__c -> Budget__c
  - Actual_Cost__c -> Actual_Cost__c
  - Completion_Percentage__c -> Completion_Percentage__c
  - Is_Billable__c -> Is_Billable__c

- Resource__c:
  - Resource Name (create mapping to Name field if needed)
  - Employee__c -> Employee__c (User Id)
  - Role__c -> Role__c
  - Daily_Rate__c -> Daily_Rate__c
  - Availability__c -> Availability__c
  - Skills__c -> Skills__c

- Deliverable__c:
  - Deliverable_Name__c -> Deliverable_Name__c
  - Project__c -> Project__c (map by Project_Code__c)
  - Status__c -> Status__c
  - Assigned_To__c -> Assigned_To__c (User Id)
  - Due_Date__c -> Due_Date__c
  - Estimated_Hours__c -> Estimated_Hours__c
  - Actual_Hours__c -> Actual_Hours__c
  - Completion_Notes__c -> Completion_Notes__c

- Project_Resource__c:
  - Project__c -> Project__c (map by Project_Code__c)
  - Resource__c -> Resource__c (map by Resource Name or external id)
  - Role__c -> Role__c
  - Allocation_Percent__c -> Allocation_Percent__c
  - Start_Date__c -> Start_Date__c
  - End_Date__c -> End_Date__c

Troubleshooting Checklist
- Ensure picklist values exist for Industry, Country, Client Tier, Status, Priority, Role
- Ensure Client_Code__c and Project_Code__c are marked as External ID in field settings
- If Data Loader complains about record types, supply RecordTypeId values (export RecordType dataset to map API names to Ids)
- If lookup mapping fails, perform two-step import: insert parents then update children with correct Salesforce IDs

If you want, I can:
- Provide a PowerShell script that replaces Employee names with User Ids (requires you to run `sfdx force:data:soql:query` to export users first), or
- Attempt CLI import again after you fix the sfdx/Node environment (I will provide the commands I would run).