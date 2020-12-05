# How to use Random Module

### The random module provides access to functions that support many operations. Perhaps the most important thing is that it allows you to generate random numbers.

## Random functions
### The Random module contains some very useful functions.

### **Randint**

### If we wanted a random integer, we can use the randint function Randint accepts two parameters: a lowest and a highest number. Generate integers between 1,5. The first value should be less than the second.
### It will not chose first value

### **Random**
### If you want a larger number, you can multiply it.

### For example, a random number between 0 and 100:
```python
import random
random.random()*100
```

### **Choice**
### he choice function can often be used for choosing a random element from a list.

```python
import random
myList = [2, 109, False, 10, "Lorem", 482, "Ipsum"]
random.choice(myList)
```

### **Shuffle**
### The shuffle function, shuffles the elements in list in place, so they are in a random order.

### **Randrange**
### Generate a randomly selected element from range(start, stop, step)

