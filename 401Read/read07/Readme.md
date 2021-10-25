# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|7|[Python Scope](Python-Scope.md)









# Python Scope
## Understanding Scope
### In programming, the scope of a name defines the area of a program in which you can unambiguously access that name, such as variables, functions, objects, and so on. A name will only be visible to and accessible by the code in its scope. 
### Most commonly, you’ll distinguish two general scopes:

-  **Global scope:** The names that you define in this scope are available to all your code.

- **Local scope:** The names that you define in this scope are only available or visible to the code within the scope.

## Python Scope vs Namespace
### In Python, the concept of scope is closely related to the concept of the namespace. As you’ve learned so far, a Python scope determines where in your program a name is visible. Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called namespaces. These are the concrete mechanisms that Python uses to store names. They’re stored in a special attribute called .__dict__.
### Names at the top level of a module are stored in the module’s namespace. In other words, they’re stored in the module’s .__dict__ attribute. Take a look at the following code:
```python
import sys
sys.__dict__.keys()
dict_keys(['__name__', '__doc__', '__package__',..., 'argv', 'ps1', 'ps2'])
```

### After you import sys, you can use .keys() to inspect the keys of sys.__dict__. This returns a list with all the names defined at the top level of the module. In this case, you can say that .__dict__ holds the namespace of sys and is a concrete representation of the module scope.

## Using the **LEGB** Rule for Python Scope
### Python resolves names using the so-called LEGB rule, which is named after the Python scope for names. The letters in LEGB stand for Local, Enclosing, Global, and Built-in. Here’s a quick overview of what these terms mean:
- **Local** (or function) scope is the code block or body of any Python function or lambda expression. This Python scope contains the names that you define inside the function.

- **Enclosing** (or nonlocal) scope is a special scope that only exists for nested functions.

- **Global** (or module) scope is the top-most scope in a Python program, script, or module. This Python scope contains all of the names that you define at the top level of a program or a module.

- **Built-in** scope is a special Python scope that’s created or loaded whenever you run a script or open an interactive session.

## Functions: The Local Scope
### he local scope or function scope is a Python scope created at function calls. Every time you call a function, you’re also creating a new local scope. On the other hand, you can think of each def statement and lambda expression as a blueprint for new local scopes. These local scopes will come into existence whenever you call the function at hand.

### By default, parameters and names that you assign inside a function exist only within the function or local scope associated with the function call. When the function returns, the local scope is destroyed and the names are forgotten.

## Nested Functions: The Enclosing Scope
### Enclosing or nonlocal scope is observed when you nest functions inside other functions. It takes the form of the local scope of any enclosing function’s local scopes. Names that you define in the enclosing Python scope are commonly known as **nonlocal** names.

```
>>> def outer_func():
...     # This block is the Local scope of outer_func()
...     var = 100  # A nonlocal var
...     # It's also the enclosing scope of inner_func()
...     def inner_func():
...         # This block is the Local scope of inner_func()
...         print(f"Printing var from inner_func(): {var}")
...
...     inner_func()
...     print(f"Printing var from outer_func(): {var}")
...
>>> outer_func()
Printing var from inner_func(): 100
Printing var from outer_func(): 100
>>> inner_func()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'inner_func' is not defined
```

### When you call outer_func(), you’re also creating a local scope. The local scope of outer_func() is, at the same time, the enclosing scope of inner_func(). From inside inner_func(), this scope is neither the global scope nor the local scope. It’s a special scope that lies in between those two scopes and is known as the **enclosing** scope.

### All the names that you create in the enclosing scope are visible from inside inner_func(), except for those created after you call inner_func(). Here’s a new version of outer_fun() that shows this point:

```
>>> def outer_func():
...     var = 100
...     def inner_func():
...         print(f"Printing var from inner_func(): {var}")
...         print(f"Printing another_var from inner_func(): {another_var}")
...
...     inner_func()
...     another_var = 200  # This is defined after calling inner_func()
...     print(f"Printing var from outer_func(): {var}")
...
>>> outer_func()
Printing var from inner_func(): 100
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    outer_func()
  File "<stdin>", line 7, in outer_func
    inner_func()
  File "<stdin>", line 5, in inner_func
    print(f"Printing another_var from inner_func(): {another_var}")
NameError: free variable 'another_var' referenced before assignment in enclosing
 scope
```
## Modules: The Global Scope
### From the moment you start a Python program, you’re in the global Python scope. Internally, Python turns your program’s main script into a module called __main__ to hold the main program’s execution. The namespace of this module is the main **global scope** of your program.

### Whenever you run a Python program or an interactive session like in the above code, the interpreter executes the code in the module or script that serves as an entry point to your program. This module or script is loaded with the special name, __main__. From this point on, you can say that your main global scope is the scope of __main__.

### There’s only one global Python scope per program execution. This scope remains in existence until the program terminates and all its names are forgotten. Otherwise, the next time you were to run the program, the names would remember their values from the previous run.

