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

