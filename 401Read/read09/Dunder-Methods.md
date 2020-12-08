# Dunder Methods
## What Are Dunder Methods?
### In Python, special methods are a set of predefined methods you can use to enrich your classes. They are easy to recognize because they start and end with double underscores, for example __init__ or __str__.


## **Object Initialization: __ init __:** 
### To construct account objects from the Account class I need a constructor which in Python is the __ init __ dunder:

```python
class Account:
    """A simple account class"""

    def __init__(self, owner, amount=0):
        """
        This is the constructor that lets us create
        objects from this class
        """
        self.owner = owner
        self.amount = amount
        self._transactions = []
```

### The constructor takes care of setting up the object. In this case it receives the owner name, an optional start amount and defines an internal transactions list to keep track of deposits and withdrawals.

## **Object Representation: __ str __, __ repr __:**
### It’s common practice in Python to provide a string representation of your object for the consumer of your class (a bit like API documentation.) There are two ways to do this using dunder methods:
- **__ repr __:** The “official” string representation of an object. This is how you would make an object of the class. The goal of __ repr __ is to be unambiguous.

- **__ str __:** The “informal” or nicely printable string representation of an object. This is for the enduser.

```python
class Account:
    # ... (see above)

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)
```

## **Operator Overloading for Comparing Accounts: __ eq __, __ lt __:**

###  Why does > work equally well on integers, strings and other objects (as long as they are the same type)? This polymorphic behavior is possible because these objects implement one or more comparison dunder methods.

## **Callable Python Objects: __ call __:**
### You can make an object callable like a regular function by adding the __call__ dunder method.



