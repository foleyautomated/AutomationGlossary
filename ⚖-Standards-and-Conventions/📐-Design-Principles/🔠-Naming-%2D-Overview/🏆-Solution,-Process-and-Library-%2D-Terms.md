# Overview 
The "**Solution Namespace**" is the foundational building block for all other names on an RPA team. 

_Examples:_
| Solution Parent Folder      | Solution Name                     | **Solution Namespace**                     | **Solution Path**                           |
| --------------------------- | --------------------------------- | ------------------------------------------ | --------------------------------------------|
| Sales/Tax                   | StoreDepreciationReporting        | Sales.Tax.StoreDepreciationReporting       | Sales/Tax/StoreDepreciationReporting        |                             
| HR/Payroll                  | MonthlyQuickbooksReconciliation   | HR.Payroll.MonthlyQuickbooksReconciliation | HR/Payroll/MonthlyQuickbooksReconciliation  |

---
# Terms and Definitions
### A "**Solution**"
- Delivers **ROI**
- Solves a **Use Case.**
- Is comprised of one or more **Automations**
- Should have at least one **Queue** (for the sake of reporting)
- Is Confined to one **Solution Folder**, but can have sub-folders
- Must have a **Solution Namespace**

### A "**Process**"
- Is a single, UiPath project of type 'Process'
- Has a role. Typically: _Dispatcher_, _Performer_, or _Reporter_
- Lives in it's own Repo and has it's Own Pipeline
- Will reference **Library** packages

### A "**Library**"
- Is a single, UiPath project of type 'Library'
- Has reusable **Capabilities** 
- Lives in it's own Repo and has it's own Pipeline

### A "**Capability**"
`ExportReport.xlsx`
- Lives inside a **Library**
- Is typically a [State, Wait, Step, Get, or Goto]()

# Solution Naming Deep-Dive

### A "**Solution Parent Folder Path**":  `VSIT/HR`
 - Should start with the Name or Acronym of the Business Unit Receiving the Solution
 - _Can_ include multiple sub-folders, separated by a '/', to differentiate areas of that business unit
 - Should Have **_No Spaces_** 
 - Should Be written in **CamelCase**
 - Should Not include Special Characters (&, %, #, \\, /, etc)

### A "**Solution Name**":  `KronosDFF`
 - Uniquely Identify the Automation using _Use-Case or Business-Domain Specific Terminology_
 - Have at least 2 words
 - Should Have **_No Spaces_** 
 - Should Be written in **CamelCase**
 - Should Be Brief
 - Should Not include Special Characters (&, %, #, \\, /, etc)

### A "**Solution Short Name**" `DFF`
 - Should be Unique among other **Solution Short Names**
 - Should Be an abbreviated version of  the **SolutionName**
 - _Can_ be or include an acronyms
 - Is commonly used for unofficial communication
 - Is commonly used for chat communication with the Client Team
 - Should **_not_** be used for official documents

### A "**Solution Namespace**" `VSIT/HR/KronosDFF`
 - Is just the **Solution Parent Folder Path/Solution Name** 
 - Represents a fully unique and specific  full-name for a given solution 


| Bad 'Solution Namespace' Examples            | Good 'Solution Namespace' Examples              | Reasoning                                       |
| ------------------------------------------ | --------------------------------------------- | ----------------------------------------------- |
| ❌BI/Sales Report                           | ✅FOL/BI/QuarterlySalesCalculation         | 'Sales Report' is too generic                   |
| ❌Finance/Depreciation                      | ✅Finance/AnnualStoreDepreciation           | Avoid 1 word Solution Names                     |
| ❌DailyManagerRemediationUpdate             | ✅HR/Staffing/DailyManagerRemediationUpdate | Missing Biz unit/domain                         |
| ❌HR/customer_service/consumer_data_cleanup | ✅HR/CustomerService/ConsumerDataCleanup    | Use Camel Case, not snake_case                  |
| ❌IT/ServiceDesk/DailyTicket13423           | ✅IT/ServiceDesk/DailyBackofHouseRestart    | Use Domain Specific Terminology over id numbers |


# Process Naming Deep-Dive
A typical RPA team will have _dozens_ of processes, and therefore, dozens of Repos. With that said, good Process Naming is essential. 
### A "**Process Type**" is typically:
- "Dispatcher" -> Gathers QueueItems for the **Performer** to process
- "Performer" -> Processes each QueueItem, as a transaction. 
- "Reporter" -> Typically sends out an email summary or chat message to report results. 
- "Disporter" -> A Combination between **Dispatcher** and **Reporter**; The **Disporter** dispatches queue items, suspends while processing queue items, and then reports. 
- Some combination/modification of those^



### A "**Process Namespace**" is determined using these steps:
1. Insert the **Feature Number** before the end of the **Solution Name** in the **Solution Namespace**
2. Add '/' + the **Process Type** to the end
3. A **Repo Name** should be identical to the **Process Namespace** of the Process it contains!

| Solution Namespace | Feature Number | Process Type | **Process Namespace** (same as repo name)  |
| ------------------ | -------------- | ------------ | ------------------------------------------ |
| VSIT.HR.KronosDFF  | 1271           | Dispatcher   | VSIT.HR.1271.KronosDFF.Dispatcher          | 

_occasionally, a Solution will house more than one Process with the same Process Type. 
In such cases, add a brief descriptor before the standard Process Type when determining each Process Namespace:_

| Solution Namespace | Feature Number | Process Type | **Process Namespace**  (same as repo name) |
| -------------------| -------------- | ------------ | ------------------------------------------ |
| VSIT.HR.KronosDFF  | 1234           | Reporter     | VSIT.HR.1271.KronosDFF.DailyReporter       |
| VSIT.HR.KronosDFF  | 1234           | Reporter     | VSIT.HR.1271.KronosDFF.MonthlyReporter     |


### A "**ProjectName**"
- Is the literal value of the 'name' property in the project.json


# Automation Naming Deep-Dive
If Processes and Solution naming is done correclty, Automation naming (i.e, "Display Name") is easy. If the **Process Name** is relatively short, use that. If it is too long, remove the **Solution Namespace** and **Feature Number**:


| **Automation Display Name (Long)**               | **Automation Display Name (Short)** |
|--------------------------------------------------|-------------------------------------|
| FOL.Sales.1234.CommissionAnalysis.DailyReporter | CommissionAnalysis.DailyReporter    |


# Conclusion: Why take these standards seriously?

## Consider all the Software Items Required To execute a Solution:
 - Dispatchers
 - Reporters
 - Performers
 - Apps
 - Integrations
 - Queues
 - Storage Buckets
 - Databases
 - Test Cases
 - Test Scenario Definitions
 - Test Schedules
 - Email templates
 - Users with Popper Access
 - Anything else required to execute the automation
 - Shared Drive Output Location
 - Shared Drive Input Location
 - Shared Drive Exception Screenshot Location
 

## Now, consider all the Tertiary Items Required to build, maintain, and collaborate on a solution:
 - Repos
 - Pipelines
 - DevOps Features
 - DevOps Epics
 - SDD (Design Diagrams)
 - PDD (Must capture ROI)
 - Chats
 - Email Chains 
 - Sample Input/Output Documents
 - Screenshots
 - Demo Videos
 - Meeting Notes

Without proper conventions for each item above, the team will rapidly bury itself under a mass of unsearchable, unmaintainible, demoralizing confusion. 

If we create and follow a standard naming convention for **Solution Namespaces**, we can use those namespaces as the _basis for all other names in our org_. See the rest of the sub-pages under **Naming** in the Wiki to see how. 

