|Read No. | Name of chapter|
|:---------: |:--------------:|
|4|[Classes and Objects](Classes_and_Objects.md)
|4|[Thinking Recursively in Python](Thinking-Recursively-in-Python.md)
|4|[Fixtures](401Read/read04/Fixtures.md)|








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

# Fixtures
### When you're writing tests, you're rarely going to write just one or two. Rather, you're going to write an entire "test suite", with each test aiming to check a different path through your code. In many cases, this means you'll have a few tests with similar characteristics, something that pytest handles with "parametrized tests".

### But in other cases, things are a bit more complex. You'll want to have some objects available to all of your tests. Those objects might contain data you want to share across tests, or they might involve the network or filesystem. These are often known as "fixtures" in the testing world, and they take a variety of different forms.

### Fixtures are used differently from global variables. For example, let's say you want to include this fixture in one of your tests. You then can mention it in the test's parameter list. Then, inside the test, you can access the fixture by name.

### You also can decide how often a fixture is run. For example, as it's written now, this fixture will run once per test that mentions it. That's great in this case, when you want to compare with a list or file-like structure. But what if you want to set up an object and then use it multiple times without creating it again? You can do that by setting the fixture's "scope". For example, if you set the scope of the fixture to be "module", it'll be available throughout your tests but will execute only a single time. You can do this by passing the scope parameter to the @pytest.fixture decorator:
```python
@pytest.fixture(scope='module')
def simple_file():
   return StringIO('\n'.join(['abc', 'def', 'ghi', 'jkl']))
```

## Coverage

### For example, let's assume you have a very strange function, only_odd_mul, which multiplies only odd numbers:
```python
def only_odd_mul(x, y):
   if x%2 and y%2:
       return x * y
   else:
       raise NoEvenNumbersHereException(f'{x} and/or {y}
 ↪not odd')
```

### Here's a test you can run on it: 
```python
def test_odd_numbers():
   assert only_odd_mul(3, 5) == 15
```
### Sure enough, the test passed. It works great! The software is terrific!

### Oh, but wait—as you've probably noticed, that wasn't a very good job of testing it. There are ways in which the function could give a totally different result (for example, raise an exception) that the test didn't check.

### Perhaps it's easy to see it in this example, but when software gets larger and more complex, it's not going to be so easy to eyeball it. That where you want to have "code coverage", checking that your tests have run all of the code.

### Now, 100% code coverage doesn't mean that your code is perfect or that it lacks bugs. But it does give you a greater degree of confidence in the code and the fact that it has been run at least once.

### So, how can you include code coverage with pytest? It turns out that there's a package called pytest-cov on PyPI that you can download and install. Once that's done, you can invoke pytest with the --cov option. If you don't say anything more than that, you'll get a coverage report for every part of the Python library that your program used, so I strongly suggest you provide an argument to --cov, specifying which program(s) you want to test. And, you should indicate the directory into which the report should be written


### This creates a directory called htmlcov. Open the index.html file in this directory using your browser, and you'll get a web-based report showing (in red) where your program still lacks coverage. Sure enough, in this case, it showed that the even-number path wasn't covered.




