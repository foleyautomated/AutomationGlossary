
# Overview

- [ ] Follow the [🧩 States, Waits, Steps, Gets, and Gotos](/⚖-Standards-and-Conventions/📐-Design-Principles/🧩-Capabilities) Guide
- [ ] As with everything else, use [Pascal Case](https://www.theserverside.com/definition/Pascal-case)
- [ ] Workflow Files **_do_** something, and should therefore include an [Imperative Verb](https://www.grammarly.com/blog/imperative-verbs/), in [Present Simple](https://www.grammarly.com/blog/simple-present/) tense:
_examples:_ `GotoHomePage`,_ `ReadRows`, `SearchByName`, `WaitUntilLoginIsLoaded` and `SetUsername`
_semi complete sentences are often helpful, but not required_
- [ ] TestCase Workflows meant for Debugging are named after the target workflow, followed by "\_Debug.xaml":
![image.png](/.attachments/image-de1a3b6d-13fa-4521-8082-ed734eb62363.png)
  _This causes the "Debug" workflow to sit alphabetically adjacent to the target wrokflow, simplifying maintainability._

- [ ] Treat Acronyms like words: ✅"**Url**" not ❌"**URL**"

|  _Using 'Url' instead of 'URL' avoids confusion when multiple acronyms are side by side: <br/> "NasaApiUrl" is easier to read than "NASAAPIURL"_|
|--|

- [ ] Keep filenames short; _one thing per workflow_. 
- [ ] In General, no spaces


| **If you can't think of a name that accurately describes a workflow, the workflow is probably too big.** |
|----------------------------------------------------------------------------------------------------------|



