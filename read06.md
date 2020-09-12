# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |6|[Problem Domain](https://eng-ahmad-almohammad.github.io/problem-domain/)|
 |6|[Object Literals](https://eng-ahmad-almohammad.github.io/Object-Literals/)|
 |6|[Document Object Model](https://eng-ahmad-almohammad.github.io/Document-Object-Model/|)







# Understanding The Problem Domain Is The Hardest Part Of Programming
## A familiar problem
### By creating a familiar problem domain, I found that both the tasks of me teaching a new technology and the viewer learning that technology were much easier, because it is very difficult to learn more than one thing at once.
### Simply that by taking away the problem domain, or making it so trivial that it is easily understood, I am able to make both teaching and learning easier.
## Why problem domains are hard
### The big issue is that many problem domains are like a puzzle with a blurry picture or no picture at all.
### Writing code is a lot like putting together a jigsaw puzzle.  We put together code with the purpose of building components that we have taken out of the “bigger picture” of the problem domain.
### The real world is a messy place.  Many of the problem domains we face as programmers are difficult to understand and look completely different depending on your viewpoint.
### As programmers, we also are often not given complete information about the problem domain, so we don’t even have the information we need to understand it.
## Programming is easy if you understand the problem domain
###  It is very difficult to solve a problem before you know the question.  It’s like buzzing in on Jeopardy before you hear the clue and shouting out random questions.
## What can you do about it?
### If understanding the problem domain is the hardest part of programming and you want to make programming easier, you can do one of two things:

### 1-Make the problem domain easier

### 2-Get better at understanding the problem domain

### You can often make the problem domain easier by cutting out cases and narrowing your focus to a particular part of the problem.










 # Object Literals
## WHAT IS AN OBJECT?
### Objects group together a set of variables and functions to create a model of a something you would recognize from the real world. In an object, variables and functions take on new names. 
* IN AN OBJECT: VARIABLES BECOME KNOWN AS PROPERTIES 
* IN AN OBJECT: FUNCTIONS BECOME KNOWN AS METHODS 
## Creating an object: Literal notation
### Literal notation is the easiest way and most popular way to create objects.
![objects](https://user-images.githubusercontent.com/70091044/93000314-3f73a400-f530-11ea-8f12-f9a119eb5bf4.PNG)
## Accessing an object and **DOT NATATION**.
### You access the properties or methods of an object using dot notation. 
![call an object](https://user-images.githubusercontent.com/70091044/93000461-52d33f00-f531-11ea-91d3-196429e429d7.PNG)










# Document Object Model
### The Document Object Model (DOM) specifies how browsers should create a model of an HTML page and how JavaScript can access and update the contents of a web page while it is in the browser window. 
## THE DOM TREE IS A MODEL OF A WEB PAGE
### As a browser loads a web page, it creates a model of that page. The model is called a DOM tree, and it is stored in the browsers' memory. It consists of four main types of nodes:
* THE DOCUMENT NODE 
* ELEMENT NODES 
* ATTRIBUTE NODES
* TEXT NODES 


![DOM Tree](https://user-images.githubusercontent.com/70091044/93000953-1bb25d00-f534-11ea-91fc-0188fdd3c037.PNG)

## THE DOCUMENT NODE (yellow color)
### At the top of the tree a document node is added; it represents the entire page. When you access any element, attribute, or text node, you navigate to it via the document node. It is the starting point for all visits to the DOM tree. 

## ELEMENT NODES (green color)
### To access the DOM tree, you start by looking for elements. Once you find the element you want, then you can access its text and attribute nodes if you want to. This is why you start by learning methods that allow you to access element nodes, before learning to access and alter text or attributes. 

## ATTRIBUTE NODES
### The opening tags of HTML elements can carry attributes and these are represented by attribute nodes in the DOM tree.

## TEXT NODES
### Once you have accessed an element node, you can then reach the text within that element. This is stored in its own text node. 
## Caching DOM queries
### Methodw that find elements in the DOM tree are called *DOM queries*. When you need to work with an element more than once, you should use a variable to store the result of this query.
![DOM querie](https://user-images.githubusercontent.com/70091044/93001508-27078780-f538-11ea-96cb-a881aec89310.PNG)
## Methods that select individual elements
* getElementById(): is the quickest and most efficient way to access an ele,emt because no two elements van share the same value for their **id** attribute.

* querySelector(): is a more recent addition to the DOM, so it is not supported in older browsers. But it is very flexible because its parameter is a CSS selector, which means it can be used to accurately target many more elements.


![getElementById](https://user-images.githubusercontent.com/70091044/93001706-bc574b80-f539-11ea-86dc-3d2a00fd3160.PNG)

## SELECTING AN ELEMENT FROM A NODELIST 
### A Nodelist is a collection of element nodes. Each node is given an index number (a number that starts at zero, just like an array). 
### There are two ways to select an element from a Nodelist: The item() method and array syntax(variable name[] ). Both require the index number of the element you want. 
## Another methodes for selecting:
* SELECTI NG ELEMENTS USING CLASS ATTRIBUTES ( getElementByClassName() ) 
* SELECTING ELEMENTS BY TAG NAME (getElementByTagName() )
* SELECTING ELEMENTS USING CSS SELECTORS ( querySelector() ) (eturns the first element node that matches the CSS-style selector.) 
* querySe 1ectorA11 () returns a Nodelist of all of the matches. 
## Repeating actions for an entire nodelist
### When you have a NodeList, you can loop through each node in the collection and apply the same statements to each.
