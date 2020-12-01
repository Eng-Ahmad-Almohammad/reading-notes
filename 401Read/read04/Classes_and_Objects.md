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