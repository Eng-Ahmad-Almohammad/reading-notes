# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |10|[Debugging](https://eng-ahmad-almohammad.github.io/Debugging/)









 # Debugging
## ORDER OF EXECUTION
### To find the source of an error, it helps to know how scripts are processed. The order in which statements are executed can be complex; some tasks cannot complete until another statement or function has been run.

## EXECUTION CONTEXTS
### The JavaScript interpreter uses the concept of execution contexts. There is one global execution context; plus, each function creates a new new execution context. They correspond to variable scope. 

## The stack
### The JavaScript interpreter processes one line of code at a time. When a statement needs data from another function, it stacks the new function on top of the curent task.


## ERROR OBJECTS 
### Error objects can help you find where your mistakes are and browsers have tools to help you read them. 

![even object](https://user-images.githubusercontent.com/70091044/93378664-6ea65000-f865-11ea-8cf2-eb90e166e59c.PNG)

## A DEBUGGING WORKFLOW 
### Debugging is about deduction: eliminating potential causes of an error. 
## BROWSER DEV TOOLS & JAVASCRIPT CONSOLE 
### The JavaScript console will tell you when there is a problem with a script, where to look for the problem, and what kind of issue it seems to be. 
## TYPING IN THE CONSOLE  
### You can also just type code into the console and it will show you a result. 
