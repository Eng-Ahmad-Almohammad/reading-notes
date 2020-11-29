|Read No. | Name of chapter|
|:---------: |:--------------:|
|2|[In Tests We Trust — TDD with Python](Python-Recursion.md)
|2|[Recursion](Recursion.md)















# Unit tests and TDD

### Unit tests are some pieces of code to exercise the input, the output and the behaviour of your code. You can write them anytime you want.

### The first one is the test name. The tests can be considered as your alive documentation. We need to be descriptive about it and to say what is expected and what we are testing.

### The test file name should follow the same name of module name. For instance, if our module is gender.py, our test name should be test_gender.py. It’s ideal to separate the tests folder from production code (the implementation)

## Other thing to care about is the structure. A convention widely used is the AAA: Arrange, Act and Assert.

- **Arrange**: you need to organize the data needed to execute that piece of code (input);

- **Act**: here you will execute the code being tested (exercise the behaviour);

- **Assert**: after executing the code, you will check if the result (output) is the same as you were expecting.

## The Cycle
### The cycle is made by three steps:
🆘 Write a unit test and make it fail (it needs to fail because the feature isn’t there, right? If this test passes, call the Ghostbusters, really).

✅ Write the feature and make the test pass! (you can dance after that).

🔵 Refactor the code — the first version doesn’t need to be the beautiful one (don’t be shy)



# Recursion

## What is Recursion? 
### The fundamental part of recursion is self-reference - functions calling themselves. It is used to solve problems that can be broken up into easier sub-problems of the same type.

## What is base condition in recursion? 
### In the recursive program, the solution to the base case is provided and the solution of the bigger problem is expressed in terms of smaller problems. 

```python
def factorial(x):
  if x == 1:
    return 1
  else: 
    return x * factorial(x-1)
    
print(factorial(5))

```
### In the above example, base case for n < = 1 is defined and larger value of number can be solved by converting to smaller one till base case is reached.

## What is the difference between direct and indirect recursion? 

### A function fun is called direct recursive if it calls the same function fun. A function fun is called indirect recursive if it calls another function say fun_new and fun_new calls fun directly or indirectly. 
```python
def is_even(x):
  if x == 0:
    return True
  else:
    return is_odd(x-1)

def is_odd(x):
  return not is_even(x)


print(is_odd(17))
print(is_even(23))
```

## How memory is allocated to different function calls in recursion? 

### When any function is called from main(), the memory is allocated to it on the stack. A recursive function calls itself, the memory for a called function is allocated on top of memory allocated to calling function and different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues.

