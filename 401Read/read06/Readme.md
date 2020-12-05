# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|6|[How to use Random Module](How-to-use-Random-Module.md)
|6|[What is Risk Analysis](What-is-Risk-Analysis.md)









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



# What is Risk Analysis

### The probability of any unwanted incident is defined as Risk. In Software Testing, risk analysis is the process of identifying the risks in applications or software that you built and prioritizing them to test. After that, the process of assigning the level of risk is done.

## Why use Risk Analysis?
### After knowing about the risk areas, it helps the developers and managers to mitigate the risks. When a test plan has been created, risks involved in testing the product are to be taken into consideration along with the possibility of the damage they may cause to your software along with solutions.

### Possible risks that you could encounter
1- Use of new hardware
2- Use of new technology
3- Use of new automation tool
4- The sequence of code
5- Availability of test resources for the application

### there are certain risks that are unavoidable:
1- The time that you allocated for testing

2- A defect leakage due to the complexity or size of the application

3- Urgency from the clients to deliver the project

4- Incomplete requirements

### In such cases, you have to tackle the situation with care. Following points can be taken care of:

- Conduct Risk Assessment review meeting

- Use maximum resources to work on high-risk areas

- Create a Risk Assessment database for future use

- Identify and notice the risk magnitude indicators: high, medium, low

###  what are these risk magnitude indicators?
### **High:** means the effect of the risk would be very high and non-tolerable. The company might face loss.

### **Medium:** it is tolerable but not desirable. The company may suffer financially but there is a limited risk.

### **Low:** it is tolerable. There lies little or no external exposure or no financial loss.

## Risk Assessment

### In the risk analysis process, these steps prove to be the most important one. It is said that this step is way too complex and should be tackled with the utmost care. After risk identification, assessment has to be dealt programmatically. 

## The perspective of Risk Assessment:
### There are three perspectives of Risk Assessment:


### **Effect** – To assess risk by Effect. In case you identify a condition, event or action and try to determine its impact.

### **Cause** – To assess risk by Cause is opposite of by Effect. Initialize scanning the problem and reach to the point that could be the most probable reason behind that.

### **Likelihood** – To assess risk by Likelihood is to say that there is a probability that a requirement won’t be satisfied.


## How to perform Risk Analysis?
### There are three steps:

1- Searching the risk

2- Analyzing the impact of each individual risk

3- Measures for the risk identified
