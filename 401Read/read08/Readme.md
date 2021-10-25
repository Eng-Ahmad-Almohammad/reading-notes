# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|8|[List Comprehensions](List-Comprehensions.md)





# List Comprehensions
### It consists of brackets containing an expression followed by a for clause, then zero or more for or if clauses. The expressions can be anything, meaning you can put in all kinds of objects in lists.

### The result will be a new list resulting from evaluating the expression in the context of the for and if clauses which follow it.

### The list comprehension always returns a result list.

## Syntax
### The list comprehension starts with a **‘[‘ and ‘]’, square brackets,** to help you remember that the result is going to be a list.

```python
[ expression for item in list if conditional ]
```

### This is equivalent to:
```python
for item in list:
    if conditional:
        expression
```

## Examples

## Show the first letter of each word

```python
listOfWords = ["this","is","a","list","of","words"]

items = [ word[0] for word in listOfWords ]

print items
```

## Using list comprehension in functions:
```python
# Create a function and name it double:
def double(x):
  return x*2

# If you now just print that function with a value in it, it should look like this:
print double(10)
#outout 20
```

### We can easily use list comprehension on that function.

```python
>>> [double(x) for x in range(10)]

print double
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# You can put in conditions:

>>> [double(x) for x in range(10) if x%2==0]
[0, 4, 8, 12, 16]

# You can add more arguments:

>>> [x+y for x in [10,30,50] for y in [20,40,60]]
[30, 50, 70, 50, 70, 90, 70, 90, 110]
```