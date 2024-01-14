

# Overview
 When naming Arguments and variables:
- Use **CamelCase**
- Use **singular nouns** for individual objects
- Use **plural nouns** for Lists or Arrays
- Use true/false statements for **Booleans**
- Append "JO" to the end of JObjects
- Append JA to the end of JArrays
- Append DT to the end of DataTables
- When Assigning from an Argument to a Variable, it's generally helpful to name the Variable after the Argument (sams the direction prefix), or vise versa. 

---
---
# Arguments
## Workflow Arguments
1. Use the correct direction prefix:

| Prefix | Direction |
|--------|-----------|
| in_    | In        |
| out_   | Out       |
| io_    | In/Out    |

2. Use Pascal Case after the prefix:

| Example           |
|-------------------|
| in_TimeoutSeconds |
| io_BusinessDataJO |


## Invoke Code Arguments
These are identical to Workflow Arguments, but should use _Camel Case_ instead of _PascalCase_, to prevent confusion within logs:

| Example           |
|-------------------|
| in_timeoutSeconds |
| io_businessDataJO |


## When should we use a Required vs Optional Argument?
If a Workflow cannot function properly without a non-null value for a given argument, then that argument should have its "**IsRequired**" Property set to **true**. This makes the usage of the Workflow more obvious to other developers.

If an argument is optional, leave the "_IsRequried_" Property **false**.

## When should we use Default Values for Arguments?
Default values for arguments suggest a common/convenient variable value _that won't lead to unexpected exceptions if forgotten._

### Default Values in Timeouts
✅ Default Values for **Timeouts** are great, because it gives other developers an idea for how long the workflow should typically take. If they are not adjusted, the worst things that can happen are (Probably) a timeout error or poor performance. 
❌ Default values for **Urls** or **UserNames** are bad, because failure to set the value could result in confusing exceptions in prod. 

---
---
# Variables
## Standards Variables
Standard Variables follow exactly the same conventions as **Arguments**, sans "io_", "in_", and "out_". 
## Activity Variables
Some Activities, like the varrious ForEach Activities, create a local variable defined only within their scope. 
The default names are often "CurrentRow", "CurrentItem" and such. To avoid confusion and add clarity, we prefer [CamelCase](https://developer.mozilla.org/en-US/docs/Glossary/Camel_case) where the first letter is _lower case_. This helps differentiate these atypical variables from other variables. 

## Parameter Variables
We use LINQ everyday, and LINQ often uses a local "parameter" variable within a lambda. 
As with **Activity Variables**, **Parameter Variables** should start with a lower case letter and be camel cased after.
Additionally, if the purpose of the **Parameter Variable** is clear enough from context, you can break the other rules and just use a single letter or abbreviation:
```
//Whose birthday is today?
Dictionary<string, DateTime> BirthdaysByName = GetNextBirthdaysByName();
Dictionary<string, DateTime> BirthdaysTodayByName = BirthdaysByName
    .Where(kvp, kvp.Value.Date == DateTime.Now.Date)
    .ToDictionary(n => n, bday => bday);

//"kvp" is a great sub in for "key Value Pair" because it's identity is obvious from context. 
```








_Note: In .NET, boolean variables and arguments have **always** start default value of false, unless otherwise assigned_
