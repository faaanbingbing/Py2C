> I wrote this in June 2014 as a part of a 14000 char Markdown document for self-reference, before I took a long break from the project.

------

### Managers
Each "stage" in the translation process is managed by their own separate Managers.

Managers do not work with/on the data-structures directly instead they manage the lower-level classes that work on the data-structures. This allows for a dual-layer abstraction of the Translation process. Think of what Classes and functions/methods are for a program, that's what Managers and Worker classes are to the Translation process in Py2C.

Every Manager has options which can be modified. The lower level classes use these options and the data passed to them to do their work.

Currently there are 5 managers:

  1. PreProcessingManager:
    - Manages the pre-processing of the code and the building of the FlowTree.
    - Team:
      - ToFlow
  2. AnalysisManager:
    - Manages the process of analysis of the FlowTree to figure out what all the code does and builds and populates the VariableMap.
  3. ModifiersManager:
    - Manages FlowTree modification based on the information collected by the Analyser.
  4. CodeGenerationManager:
    - Manages the final stage of code-generation to convert the optimised and "translated" FlowTree into optimised C++ code.
  5. TranslationManager:
    - Manages the entire translation process. Like the boss of a company, the TranslationManager manages all the processes and does its best make the system perform optimally.

A description of how the specific manager manages it's "staff" is given wherever the manager is at work.

Now that you know a bit about how everything happens on the super-high level, let's talk about what we were here for...

------

## What's the story behind the Translation?
> Before I get to it, please note that I wrote this full section as a story of how stuff works at a company called "Py2C"... A company that specializes in source-to-source translation.
> Why? Because I was felling really bored. Plus it turned out to be a nice story. :P

[cropped]
<!-- Each file made is essentially a data-structure. -->
A request is sent to the TranslationManager by the customer to translate some code. This 'job' is handed to TranslationManager.

According to the company's protocols, if at any point of time there is a problem while working with the data given to a Manager by the TranslationManager, the Manager is to report the same to the TranslationManager who has to then inform the customer that they couldn't complete the translation due to the above problem.

The TranslationManager passes this code to the PreProcessingManager.

**PreProcessingManager** is responsible for generating a FlowTree. He does so by making an AST and then using that FlowTree to make a FlowTree. The PreProcessingManager gets his department working.

Following all the company protocols like all other managers in the company, the PreProcessingManager submits his results to the TranslationManager.

TranslationManager makes a magic-copy of the FlowTree which gets modified whenever the FlowTree is modified and keeps the magic-copy with himself. He then passes the FlowTree to the AnalysisManager. 

**AnalysisManager** gets his department working to figure out as much as they can about variables in the FlowTree and puts that into a new file named VariableMap. AnalysisManager returns the FlowTree with extra information added and all the collected variable information stored in a VariableMap to the TranslationManager.

TranslationManager now passes the FlowTree and VariableMap over to the ModifiersManager.

> Figure out beyond this better.

**ModifiersManager** gets his department working and make changes to the FlowTree file based on the VariableMap. He then returns the changed FlowTree file and the unchanged VariableMap back to the TranslationManager.

TranslationManager now takes a look at the file, looking for certain flaws and then passes the file over to **CodeGenerationManager** who generates a final report and submits it to TranslationManager who gives it to the customer.

Phew!! Now, if there's a problem with the final report and original file should be submitted to the project maintainer (me) by the customer... Right? :laughing:

[cropped]
