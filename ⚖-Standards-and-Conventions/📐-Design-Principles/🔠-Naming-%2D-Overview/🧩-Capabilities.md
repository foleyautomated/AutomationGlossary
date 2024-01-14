# Capabilities Overview
Reusable Workflows inside Processes or Libraries typically fall into one of four categories: 
_**States**, **Waits**, **Gets** or **Gotos**._ Collectively, we call these **Capabilities.**

All "**Capabilities**":
- Should have a variable of type `System.String` called **`XamlFileName`** with a default value of `"YourWorkflowName.xaml"`
- Should have a variable of type `System.DateTime` called **`StartedAt`** with a default value of `DateTime.Now`
- Should, when needed, have an in_argument of type `System.Double` called **`in_TimeoutSeconds`**
- Should, when needed, have an in_argument of type `System.Boolean` called **`in_ContinueOnError`** with a default value of `false`
- Should, upon completion, append workflow duration to their final log using the format: `(0.99 seconds)` 
- Should be driven by in_arguments to encourage Re-usability and Test-ability.
- Should have as generic a name as is possible without becoming vague:

| `DownloadReport.xaml` with an `in_ReportName` arg is better than a hardcoded `DownloadSalesReport.xaml` |
|-------------------------------------------------------------------------------------------------------- |
- Should have associated [Testing and Debugging](/How-To-Use-This-Wiki/📐-Design-Principles/🧪-Unit-Testing-and-Debugging) workflows, when not easily debugged without. 
---
# States
**State workflows** check for a given state, and then return a single boolean as their result. 
Because **State workflows** can help other developers [Waiting correctly](/How-To-Use-This-Wiki/📐-Design-Principles/🕗-How-To-Wait) while using your library to create Processes, **State** workflows should always be **Public/Publishable**. **State Workflows** should be dynamic when possible, named according to whatever they are checking, and have an _out_ argument with the same name as the Workflow.

A "**State Workflow**": 
- Should use **`LogLevel.Trace`**
- Should, upon completing, log their duration and result using the format: 
  `IsSomeState.xaml --> [out_IsSomeState.ToString()] (0.99 seconds)`
- Should have an in_argument of type `System.Double` called **`in_TimeoutSeconds`** with a default value of 0.0.
- Should have an out_argument of type `System.Boolean` called "**`out_`** + **`IsSomeState`**"
- Should briefly [highlight](/How-To-Use-This-Wiki/📐-Design-Principles/✨-Highlights) any visible element it is checking to confirm a state, or highlight the window if the target element is not visible. 

- _Can have_ an in_argument of type `System.Boolean` called **`in_ContinueOnError`**
- _Can have_ an io_argument of type `Dictionary<string, boolean>` called **`io_State`** which receives the key value pair `{"IsYourStateHere" : true/false}`


| Example 'State' Workflow Names        | 'out_' Boolean Argument Names  |
|---------------------------------------|--------------------------------|
| `HomeScreenIsLoaded.xaml`             | out_HomeScreenIsLoaded         |
| `InvoiceIsComplete.xaml`              | out_InvoiceIsComplete          |
| `ReportFileFound.xaml`                | out_ReportFileFound            |

A "**Determine State Workflow**":
- Contains Multiple **State Workflows** executed in sequence or in parallel.
- Returns all **State Workflow** results as either a series of out_arguments named after the out_arguments of the **State Workflows**, or as a `Dictionary<string, boolean>` which maps state names to the results of the check. 
- Is typically Invoked inside a **Goto Workflow** (see below)
- Should be located in the same folder as the corresponding **Goto Workflow** 
- Should be named according to the related **Goto Workflow** (i.e `DetermineReadyState.xaml` for `GotoReady.xaml`)

| Examples of 'Determine State' Workflow Names | Corresponding Goto Workflow Name |
| ---------------------------------------------|----------------------------------|
| DetermineReadyState.xaml                     | GotoReady.xaml                   |
| DetermineReportDownloadState                 | GotoReport.xaml                  |

---
# Waits
A **Wait Workflow** (also called a **'Wait Until'**) is essentially a **State Workflow** wrapped a loop. These exist to wants to avoid _static-waits_ as described in  [How To Wait](/How-To-Use-This-Wiki/📐-Design-Principles/🕗-How-To-Wait).
Two of most common '**Wait Until**' scenarios are **waiting for a page to load**, and **waiting for a file to download**.

A "**Wait Workflow**": 
- Should repeatedly execute a zero-timeout **State Workflow** until a condition is met, or until the workflow times out.
- Because **State Workflows** should [highlight](/How-To-Use-This-Wiki/📐-Design-Principles/✨-Highlights) their target element, **Wait Workflows** will often show up as a series of repeated blinks.
- The simplest way to create a **Wait Workflow** is to invoke a **State Workflow** int a `retry` activity, and repeat until the `retry` condition is met. 
- Should have an in_argument of type `System.Double` called **`in_TimeoutSeconds`** with a default value _representative of typical performance._

| Example 'Wait Until Check' Workflow Name' |
|-------------------------------------------|
| `WaitForLoginPageToFullyLoad.xaml`        |
| `WaitForReportToFullyDownload`            |


---
# Steps
**Step Workflows** represent our smallest units of work which have no direct application to Business Logic. Because their function is unrelated to business logic, Steps should be **generic** and driven by **arguments** so as to encourage maximum re-usability and maximum simplicity of testing/debugging. 
Usually, steps should use **`LogLevel.Trace`** and, if a step isn't reusable outside a library, it should be set to **Private/Ignore from Publish** to avoid confusing other devs. 
A "**Step Workflow**":
- Should do _exactly one thing_
- _Can_ include some of our standard arguments (`in_TimeoutSeconds`, `in_ContinueOnError`) 
- Should have a concise, specific name.

| Example 'Step' Workflow Names |
|-------------------------------|
| `ClickButtonByName.xaml`      |
| `SetPassword.xaml`            |
| `GetInvoiceTableRows.xaml`    |
---
# Selects
**Select Workflows** will typically take in an object or list of objects denoting items to be 'Selected' from something in the GUI. Selects are commonly found in Restaurant POS Automations--Imagine a Restaurant Pos Region called 'Toppings' with a different button for each Topping. If you wrote a **Select Workflow** called `SelectToppings.xaml` with an `string[]` in_argument called `in_Toppings`, you're workflow could loop through the toppings and select whichever ones are desired.  


---
# Gets -> Reads/Finds/Takes
**Get Workflows** (also called **Read Workflows**) retrieve _something_ from an application. When a **Get Workflow** retrieves a UiElement (or a collection of UiElements) it is common to use the word 'Find' in place of get, a practice whose origin was solidified by the UiPath "Find Children" activity years ago. For example, if we have a workflow called `FindTableRows.xaml`, we clearly see that the GUI is not being modified--only ingested, whereas `Get` or `Take` might incorrectly imply that the rows in question are being actively removed. Conversly, a **Get Workflow** can be named useing the key-workd "Read" to more explicitly express the read-only nature of whatever interaction is taking place. 
As a general rule, **Get Workflows** will have an out argument _**named after the get workflow**_. This makes it easier to know where values in a cluttered Workflow are coming from. 

# Additional Common Workflow Keywords:
### FindSomething.xaml: _Returns a UiElement or a collection of UiElements_
### SelectSomething.xaml
### ReadSomething.xaml
Often, if you are litterlly reading a file, 'Read' is a better, more precise term than 'Get'. 
