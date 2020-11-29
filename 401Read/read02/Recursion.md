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

