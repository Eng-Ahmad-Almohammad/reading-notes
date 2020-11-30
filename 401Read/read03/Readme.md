|Read No. | Name of chapter|
|:---------: |:--------------:|
|3|[Python Exceptions](Exceptions-in-Python.md)
|3|[Read & Write Files in Python](Reading_and_Writing_Files_in_Python.md)












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



# Reading and Writing Files

## What Is a File?
### At its core, a file is a contiguous set of bytes used to store data. This data is organized in a specific format and can be anything as simple as a text file or as complicated as a program executable. In the end, these byte files are then translated into binary 1 and 0 for easier processing by the computer.

### Files on most modern file systems are composed of three main parts:

- **Header:** metadata about the contents of the file (file name, size, type, and so on)
- **Data:** contents of the file as written by the creator or editor
- **End of file (EOF):** special character that indicates the end of the file

## Opening and Closing a File in Python
### When you want to work with a file, the first thing to do is to open it. This is done by invoking the open() built-in function. open() has a single required argument that is the path to the file.

### When you’re manipulating a file, there are two ways that you can use to ensure that a file is closed properly, even when encountering an error:
1- try-finally block:
```python
reader = open('dog_breeds.txt')
try:
    # Further file processing goes here
finally:
    reader.close()
```

2- with statement:An alternative way of doing this is using with statements. This creates a temporary variable (often called f), which is only accessible in the indented block of the with statement.
```python
with open("filename.txt") as f:
   print(f.read())
```

### You can specify the mode used to open a file by applying a second argument to the open function.

- Sending "r" means open in read mode, which is the default.
- Sending "w" means write mode, for rewriting the contents of a file.
- Sending "a" means append mode, for adding new content to the end of the file.

- Adding "b" to a mode opens it in binary mode, which is used for non-text files (such as image and sound files).

## Reading and Writing Opened Files

### There are multiple methods that can be called on a file object to help you out:

- .read(size=-1): This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.

- .readline(size=-1): This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.

- .readlines(): This reads the remaining lines from the file object and returns them as a list.

## As with reading files, file objects have multiple methods that are useful for writing to a file:

- .write(string): This writes the string to the file.
- .writelines(seq):This writes the sequence to the file. No line endings are appended to each sequence item. It’s up to you to add the appropriate line ending(s).