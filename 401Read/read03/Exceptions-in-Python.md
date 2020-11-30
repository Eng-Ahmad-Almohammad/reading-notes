# Python Exceptions

### A Python program terminates as soon as it encounters an error. In Python, an error can be a syntax error or an exception.

## Exceptions versus Syntax Errors

### Syntax errors occur when the parser detects an incorrect statement.

### exception error: This type of error occurs whenever syntactically correct Python code results in an error.

### Instead of showing the message exception error, Python details what type of exception error was encountered. Python comes with various built-in exceptions as well as the possibility to create self-defined exceptions.


## Raising an Exception
### You can raise exceptions by using the `raise` statement.

### If you want to throw an error when a certain condition occurs using raise, you could go about it like this:

```python
x = 10
if x > 5:
    raise Exception('x should not exceed 5. The value of x was: {}'.format(x))
```

## The AssertionError Exception

###  We assert a certain condition. If this condition turns out to be True, then that is excellent! The program can continue. If the condition turns out to be False, you can have the program throw an AssertionError exception.

## The try and except Block: Handling Exceptions

### To handle exceptions, and to call code when an exception occurs, you can use a try/except statement.
### The try block contains code that might throw an exception. If that exception occurs, the code in the try block stops being executed, and the code in the except block is run. If no error occurs, the code in the except block doesn't run.
### Example:
```python
try:
   num1 = 7
   num2 = 0
   print (num1 / num2)
   print("Done calculation")
except ZeroDivisionError:
   print("An error occurred")
   print("due to zero division")
```

### Result:
```
>>>
An error occurred
due to zero division
>>>
```

### A try statement can have multiple different except blocks to handle different exceptions.
### Multiple exceptions can also be put into a single except block using parentheses, to have the except block handle all of them.

### An except statement without any exception specified will catch all errors. These should be used sparingly, as they can catch unexpected errors and hide programming mistakes.

## The else Clause
### The else statement can be used with try/except statements. In this case, the code within it is only executed if no error occurs in the try statement.

## Cleaning Up After Using finally
### To ensure some code runs no matter what errors occur, you can use a finally statement. The finally statement is placed at the bottom of a try/except statement. Code within a finally statement always runs after execution of the code in the try, and possibly in the except, blocks.

