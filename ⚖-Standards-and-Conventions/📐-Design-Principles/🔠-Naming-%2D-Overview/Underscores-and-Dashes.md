# Underscores
As you've probably noticed, [Pascal Case](https://www.theserverside.com/definition/Pascal-case) doesn't really make use of underscores (`_`)--we purposefully exclude them from namespaces, variable names,  file names. But why waste such a useful character? 

The most common exception is in our convention for naming arguments, i.e `in_`, `out_` and `io_`. In this example the `_` is used to separate **_two fundamentally different principles_**. If I have an argument called `in_CountryName`, the `in_` is totally unrelated to the Country--the rest of the argument name takes care of that. In short `CountryName` describes the value being represented,  while `in_` describes the argument itself. 

Even if this doesn't give us a hard fast rule, it does give us a general principle: **Use underscores to separate two distinct concepts within the same name.**

_Common Exceptions to the no `_` rule_:
| Example                   | Description                                |
| ------------------------- | -------------------------------------------|
| Template_State.xaml       | 'Template_' files                          |
| in_MyArgumentName         | Argument Directions                        |
| MyWorkflow_Debug.xlsx     | a Debug Workflow named after its target    |
| MyWorkflow_DebugData.json | Debug Data named after its target          |


# Dashes

TODO: When to use Dashes?