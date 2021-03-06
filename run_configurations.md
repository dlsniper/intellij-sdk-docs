---
layout: editable
title: Run Configurations
---


Run configurations allow users to run a certain type of external processes from within the IDE, i.e a script, an application, a server, etc.
You can provide UI for the user to specify execution options, as well as an option to create run configuration based on a specific location in the source code.


# Architectural overview

Classes used to manipulate *IntelliJ IDEA's* run configurations can be split into the following groups:

*  [Run configuration management](run_configuration_management.html)
   This includes creation, persistence, and modification.

*  [Execution](run_configuration_execution.html)

This diagram shows the main classes related to **IntelliJ IDEA** run configurations

![Architecture](img/run_configurations/classes.png)

