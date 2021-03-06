---
layout: editable
title: Safe Delete Refactoring
---


The ```Safe Delete``` refactoring also builds on the same ```Find Usages``` framework as ```Rename```.
In addition to that, in order to support ```Safe Delete```, a plugin needs to implement two things:

*  The
   [RefactoringSupportProvider](https://github.com/JetBrains/intellij-community/blob/master/platform/lang-api/src/com/intellij/lang/refactoring/RefactoringSupportProvider.java)
   interface, registered in the `com.intellij.lang.refactoringSupport` extension point, and the `isSafeDeleteAvailable()` method, which checks if the ```Safe Delete``` refactoring is available for a specific PSI element

*  The
   [PsiElement.delete()](https://github.com/JetBrains/intellij-community/blob/master/platform/core-api/src/com/intellij/psi/PsiElement.java#L371)
   method for the
   [PsiElement](https://github.com/JetBrains/intellij-community/blob/master/platform/core-api/src/com/intellij/psi/PsiElement.java)
   subclasses for which ```Safe Delete``` is available.
   Deleting PSI elements is implemented by deleting the underlying AST nodes from the AST tree (which, in turn, causes the text ranges corresponding to the AST nodes to be deleted from the document).


**Example:**
[delete()](https://github.com/JetBrains/intellij-community/blob/master/plugins/properties/properties-psi-impl/src/com/intellij/lang/properties/psi/impl/PropertyImpl.java#L363)
implementation for a
[Property language plugin](https://github.com/JetBrains/intellij-community/blob/master/plugins/properties/)


If needed, it's possible to further customize how Safe Delete is performed for a particular type of element (how references are searched, etc).
This is done by implementing the `SafeDeleteProcessorDelegate` interface.


**Example**:
[SafeDeleteProcessorDelegate](https://github.com/JetBrains/intellij-community/blob/master/plugins/properties/src/com/intellij/lang/properties/refactoring/PropertiesFilesSafeDeleteProcessor.java)
implementation for a .properties file