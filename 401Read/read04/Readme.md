|Read No. | Name of chapter|
|:---------: |:--------------:|
|4|[Classes and Objects](Classes_and_Objects.md)
|4|[Thinking Recursively in Python](Thinking-Recursively-in-Python.md)








# Classes and Objects

### We have previously looked at two paradigms of programming - imperative (using statements, loops, and functions as subroutines), and functional (using pure functions, higher-order functions, and recursion).

### Another very popular paradigm is object-oriented programming (OOP).
### Objects are created using classes, which are actually the focal point of OOP.
### The class describes what the object will be, but is separate from the object itself. In other words, a class can be described as an object's blueprint, description, or definition.
### You can use the same class as a blueprint for creating multiple different objects.

### Classes are created using the keyword **class** and an indented block, which contains class methods (which are functions).

```python
class Cat:
  def __init__(self, color, legs):
    self.color = color
    self.legs = legs

felix = Cat("ginger", 4)
rover = Cat("dog-colored", 4)
stumpy = Cat("brown", 3)
```

## Accessing Object Variables:

### To access the variable inside of the newly created object "myobjectx" you would do the following:

```python
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()

myobjectx.variable
```

### You can create multiple different objects that are of the same class(have the same variables and functions defined). However, each object contains independent copies of the variables defined in the class.

## Accessing Object Functions

### To access a function inside of an object you use notation similar to accessing a variable:
```python
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()

myobjectx.function()
```




# Thinking Recursively in Python

## Recursive Functions in Python

###  A recursive function is a function defined in terms of itself via self-referential expressions.

### This means that the function will continue to call itself and repeat its behavior until some condition is met to return a result. All recursive functions share a common structure made up of two parts: base case and recursive case.


## Maintaining State

### When dealing with recursive functions, keep in mind that each recursive call has its own execution context, so to maintain state during recursion you have to either:

- Thread the state through each recursive call so that the current state is part of the current call’s execution contextز
- Keep the state in global scope


## Recursive Data Structures in Python

### A data structure is recursive if it can be deﬁned in terms of a smaller version of itself. A list is an example of a recursive data structure. Let me demonstrate. Assume that you have only an empty list at your disposal, and the only operation you can perform on it is this:
```python
# Return a new list that is the result of
# adding element to the head (i.e. front) of input_list
def attach_head(element, input_list):
    return [element] + input_list
```

### Using the empty list and the attach_head operation, you can generate any list. For example, let’s generate [1, 46, -31, "hello"]:

```python
def attach_head(1,attach_head(46,attach_head(-33,attach_head('hello',[]))))
```

