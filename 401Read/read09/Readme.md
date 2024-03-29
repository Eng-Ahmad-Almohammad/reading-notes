# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|9|[Dunder Methods](Dunder-Methods.md)
|9|[Statistics - Probability](Statistics-Probability.md)







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










# Statistics - Probability

## What is probability?

### At the most basic level, probability seeks to answer the question, “What is the chance of an event happening?” An event is some outcome of interest. To calculate the chance of an event happening, we also need to consider all the other events that can occur. The quintessential representation of probability is the humble coin toss.

## From statistics to probability
### Our data will be generated by flipping a coin 10 times and counting how many times we get heads. We will call a set of 10 coin tosses a trial. Our data point will be the number of heads we observe. We may not get the “ideal” 5 heads, but we won’t worry too much since one trial is only one data point. If we perform many, many trials, we expect the average number of heads over all of our trials to approach the 50%. The code below simulates 10, 100, 1000, and 1000000 trials, and then calculates the average proportion of heads observed.

```python
import random
def coin_trial():
heads = 0
for i in range(100):
    if random.random() <= 0.5:
        heads +=1
    return heads
def simulate(n):
    trials = []
    for i in range(n):
        trials.append(coin_trial())
    return(sum(trials)/n)
simulate(10)
>>> 5.4
simulate(100)
>>> 4.83
simulate(1000)
>>> 5.055
simulate(1000000)
>>> 4.999781
```

### he coin_trial function is what represents a simulation of 10 coin tosses. It uses the random() function to generate a float between 0 and 1, and increments our heads count if it’s within half of that range. Then, simulate repeats these trials depending on how many times you’d like, returning the average number of heads across all of the trials. The coin toss simulations give us some interesting results.

### First, the data confirm that our average number of heads does approach what probability suggests it should be. Furthermore, this average improves with more trials. In 10 trials, there’s some slight error, but this error almost disappears entirely with 1,000,000 trials. As we get more trials, the deviation away from the average decreases. Sound familiar? Sure, we could have flipped the coin ourselves, but Python saves us a lot of time by allowing us to model this process in code. As we get more and more data, the real-world starts to resemble the ideal.

## The data and the distribution
### The normal distribution refers to a particularly important phenomenon in the realm of probability and statistics.The normal distribution looks like this: Normal Distribution Look:

![image](data:image/png;base64,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)

### The most important qualities to notice about the normal distribution is its symmetry and its shape. We’ve been calling it a distribution, but what exactly is being distributed? It depends on the context. In probability, the normal distribution is a particular distribution of the probability across all of the events. The x-axis takes on the values of events we want to know the probability of. The y-axis is the probability associated with each event, from 0 to 1.

## Revisiting the normal
### The normal distribution is significant to probability and statistics thanks to two factors: the Central Limit Theorem and the Three Sigma Rule.
## Central Limit Theorem
### In the previous section, we demonstrated that if we repeated our 10-toss trials many, many times, the average heads-count of all of these trials will approach the 50% we expect from an ideal coin. With more trials, the closer the average of these trials approach the true probability, even if the individual trials themselves are imperfect. This idea is a key tenet of the Central Limit Theorem. In our coin-tossing example, a single trial of 10 throws produces a single estimate of what probability suggests should happen (5 heads). We call it an estimate because we know that it won’t be perfect (i.e. we won’t get 5 heads every time).

### If we make many estimates, the Central Limit Theorem dictates that the distribution of these estimates will look like a normal distribution. The zenith of this distribution will line up with the true value that the estimates should take on. In statistics, the peak of the normal distribution lines up with the mean, and that’s exactly what we observed. Thus, given multiple “trials” as our data, the Central Limit Theorem suggests that we can hone in on the theoretical ideal given by probability, even when we don’t know the true probability. Central Limit Theorem lets us know that the average of many trials means will approach the true mean, the Three Sigma Rule will tell us how much the data will be spread out around this mean.

## Three Sigma Rule
### The Three Sigma rule, also known as the empirical rule or 68-95-99.7 rule, is an expression of how many of our observations fall within a certain distance of the mean. Remember that the standard deviation (a.k.a. “sigma”) is the average distance an observation in the data set is from the mean. The Three Sigma rule dictates that given a normal distribution, 68% of your observations will fall between one standard deviation of the mean. 95% will fall within two, and 99.7% will fall within three. A lot of complicated math goes into the derivation of these values, and as such, is out of the scope of this article. The key takeaway is to know that the Three Sigma Rule enables us to know how much data is contained under different intervals of a normal distribution.

## Z-score

### The Z-score is a simple calculation that answers the question, “Given a data point, how many standard deviations is it away from the mean?”
### By itself, the Z-score doesn’t provide much information to you. It gains the most value when compared against a Z-table, which tabulates the cumulative probability of a standard normal distribution up until a given Z-score. A standard normal is a normal distribution with a mean of 0 and a standard deviation of 1. The Z-score lets us reference this the Z-table even if our normal distribution is not standard. The cumulative probability is the sum of the probabilities of all values occurring, up until a given point.

### An easy example is the mean itself. The mean is the exact middle of the normal distribution, so we know that the sum of all probabilites of getting values from the left side up until the mean is 50%. The values from the Three Sigma Rule actually come up if you try to calculate the cumulative probability between standard deviations.



