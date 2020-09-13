# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |7|[Domain modeling](https://eng-ahmad-almohammad.github.io/Domain-Modeling/)|
 |7|[Tables](https://eng-ahmad-almohammad.github.io/Tables/)|
 |7|[Functions, Methodes, and objects](https://eng-ahmad-almohammad.github.io/Functions-Methods-and-Objects/)|










 # Domain Modeling
### Domain modeling is the process of creating a conceptual model in code for a specific problem. A model describes the various entities, their attributes and behaviors, as well as the constraints that govern the problem domain. An entity that stores data in properties and encapsulates behaviors in methods is commonly referred to as an *object-oriented* model.
## Define a constructor and initialize properties
### To define the same properties between many objects, you'll want to use a constructor function. Below is a table that summarizes a JavaScript representation of an EpicFailVideo object.
|Property|Data|Type|
|--------|----|-----|
|epicRating|1 to 10|Number|
|hasAnimals|true or false|Boolean|
### Here's an implementation of the EpicFailVideo constructor function.
![code](https://user-images.githubusercontent.com/70091044/93015271-c83a2080-f5c0-11ea-8358-5dcd103825b8.PNG)
### This is object-oriented programming in JavaScript at its most fundamental level.
#### 1- The *new* keyword instantiates (i.e. creates) an object.
#### 2- The constructor function initializes properties inside that object using the *this* variable.
#### 3- The object is stored in a variable for later use.
## Generate random numbers
### To model the random nature of user behavior, you'll need the help of a random number generator. Fortunately, the JavaScript standard library includes a Math.random() function for just this sort of occasion.
### The function uses both Math.floor and Math.random to calculate and return a random integer between min and max.
![code1](https://user-images.githubusercontent.com/70091044/93015364-878ed700-f5c1-11ea-834d-3595e0808566.PNG)
## Calculate daily Likes
### Popularity of a video is measured in Likes. And the formula for calculating Likes is the number of viewers times the percentage of viewers who'll Like a video. In other words, viewers times percentage. To calculate the number of viewers per day, generate a random number between 10 and 30 and then multiply it by the epic rating of that video.
![code2](https://user-images.githubusercontent.com/70091044/93015452-506cf580-f5c2-11ea-9af0-b742a759534c.PNG)








# Tables
## Basic Table Structure
* < table >: The < table > element is used to create a table. The contents of the table are written out row by row. 

* < tr >: You indicate the start of each row using the opening < tr > tag. (The tr stands for table row.) 

* < td >: Each cell of a table is represented using a  td > element. (The td stands for table data.)
## Table heading
## < th >
### The < th > element is used just like the < td > element but its purpose is to represent the heading for either a column or a row. (The th stands for table heading.) 
## Spanning ColumnS
### The colspan attribute can be used on a < th > or < td > element and indicates how many columns that cell should run across.
![Table](https://user-images.githubusercontent.com/70091044/93024905-71553b00-f602-11ea-83bc-cc03dc299885.PNG)
## Spanning rows 
### The rowspan attribute can be used on a < th > or < td > element to indicate how many rows a cell should span down the table.

## Long tables
### There are three elements that help distinguish between the main content of the table and the first and last rows (which can contain different content). These elements help people who use screen readers and also allow you to style these sections in a different manner than the rest of the table (as you will see when you learn about CSS).

* < thead >: The headings of the table should sit inside the <thead> element. 
* < tbody >: The body should sit inside the < tbody > element. 
* < tfoot >: The footer belongs inside the < tfoot > element.






# Functions, Methods, and Objects
## creating an object: Constructor notation
### The new keyword and the object constructor create a blank object. You can the add properties and methods to the object.
![constructor notation](https://user-images.githubusercontent.com/70091044/93028148-9a81c580-f61a-11ea-87b4-035567098ad4.PNG)
## Creating many objects: constructor notation
### Sometime you will want several objects to represent similar things. Object constructors can use a function as a *template* for creating objects.
![several objects](https://user-images.githubusercontent.com/70091044/93028279-74105a00-f61b-11ea-9167-bf512ad834e0.PNG)
## reating an instance of the date object
### In order to work with dates, you creat an instance of the *Date* object. Y can then specify the time and date you want it to represent.
![Date](https://user-images.githubusercontent.com/70091044/93028720-50024800-f61e-11ea-88a1-285233daa48e.PNG)
