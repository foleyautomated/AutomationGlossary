

# Repo Naming Rules
| Repo Type     | Naming Rule                                                                               |
| ------------- | ----------------------------------------------------------------------------------------- |
| **Process**   |*Exactly* the same as the ***Process Name***. See *Solutions, Processes, and Automations*  |
| **Library**   | CompanyName.FeatureNumber.TargetApplicationName                                           |
| **Template**  | **Template**.WhateverTheTemplateIsFor                                                     |
| **Utility**   | **Utility**.WhateverTheUtilityDoes                                                        |

# Note
The **Process Repo** name is exactly the same as the **Process Name** of the UiPath project it contains, which means the Feature Number is included. 
_Identical Process Name/Repo Name_
| Process Name                                     | Repo Name                                         |
|--------------------------------------------------|---------------------------------------------------|
| FOL.Sales.1234.CommissionAnalysis.DailyReporter | FOL.Sales.1234.CommissionAnalysis.DailyReporter  |


When naming **Libraries**, we _only include the Feature Name in the Repo, not the package_. This avoids a cluttered/confusing namespace for the workflows within the library without comprising on the traceability of the Repo

_Library Name without Feature Number, Repo name with:_
| Library Name  | Repo Name           |
|---------------|---------------------|
| FOL.HrAccess | FOL.1234.HrAccess  |

