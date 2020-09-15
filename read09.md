# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |9|[Forms](https://eng-ahmad-almohammad.github.io/Forms/)|
 |9|[Lists, Tables & Forms](https://eng-ahmad-almohammad.github.io/Lists-Tables-Forms/)|
 |9|[Events](https://eng-ahmad-almohammad.github.io/Events/)








# Forms
## Form Structure: < form >
### Form controls live inside a < form > element. This element should always carry the action attribute and will usually have a method and id attribute too.
## action
### Every < form > element requires an action attribute. Its value is the URL for the page on the server that will receive the information in the form when it is submitted.
## method
### Forms can be sent using one of two methods: 
* get :  With the get method, the values from the form are added to the end of the URL specified in the action attribute. The get method is ideal for :

1- short forms (such as search boxes).

2- when you are just retrieving data from the web server

* post: With the post method the values are sent in what are known as HTTP headers. As a rule of thumb you should use the post method if your form:

1- allows users to upload a file.

2- is very long

3- contains sensitive data (e.g. passwords)

4- adds information to, or deletes information from, a database
### Defult method for form is *get*


## Text input: < input > 
### The < input > element is used to create several different form controls. The value of the type attribute determines what kind of input they will be creating.

* type="text": When the type attribute has a value of text, it creates a singleline text input

* name: The value of this attribute identifies the form control and is sent along with the information they enter to the server.

* size: The size attribute should not be used on new forms. It was used in older forms to indicate the width of the text input 

* maxlength: You can use the maxlength attribute to limit the number of characters a user may enter into the text field.


## Password Input
### type="password": When the type attribute has a value of password it creates a text box that acts just like a single-line text input, except the characters are blocked out. 

### All other attributes are same.

![forms](https://user-images.githubusercontent.com/70091044/93193746-ec783780-f74f-11ea-9bfc-35e4ea36e3e1.PNG)

## Text area < textarea >
### The < textarea > element is used to create a mutli-line text input. Unlike other input elements this is not an empty element. It should therefore have an opening and a closing tag. Any text that appears between the opening < textarea > and closing < /textarea > tags will appear in the text box when the page loads.

## Radio Button
### type="radio": Radio buttons allow users to pick just one of a number of options.
### value: The value attribute indicates the value that is sent to the server for the selected option. The value of each of the buttons in a group should be different (so that the server knows which option the user has selected).

![radio input](https://user-images.githubusercontent.com/70091044/93194643-fbabb500-f750-11ea-88c4-f8f2e794c74d.PNG)

## Checkbox
### type="checkbox": Checkboxes allow users to select (and unselect) one or more options in answer to a question.
### value:The value attribute indicates the value sent to the server if this checkbox is checked.

## Drop Down List Box: < select >

### The < select > element is used to create a drop down list box. It contains two or more < option> elements. 

### < option >: The < option > element is used to specify the options that the user can select from. The words between the opening < option > and closing < /option > tags will be shown to the user in the drop down box.

![drop list](https://user-images.githubusercontent.com/70091044/93195436-ed11cd80-f751-11ea-813b-197045becd44.PNG)

## File Input Box
### type="file": This type of input creates a box that looks like a text input followed by a browse button. When the user clicks on the browse button, a window opens up that allows them to select a file from their computer to be uploaded to the website.






# Lists Tables Forms
## Bullet point styles:list-style-type
### The list-style-type property allows you to control the shape or style of a bullet point (also known as a marker).It can be used on rules thatapply to the < ol >, < ul >, and < li > elements.
### *Unordered Lists*: for an unordered list you can use the following values:

* none

* disc

* circle

* square

### Ordered Lists: For an ordered (numbered) list you can use the following values:

* decimal 1 2 3

* decimal-leading-zero 01 02 03

* lower-alpha a b c

* upper-alpha A B C

* lower-roman i. ii. iii.

* upper-roman I II III

## Table properties
### *width*:to set the width of the table.
### *padding*:to set the space between the border of each table cell and its content.
### *text-transform*: to convert the content of the table headers to uppercase.
### *letter-spacing, font-size* to add additional styling to the content of the table headers.
### *border-top, border-bottom*: to set borders above and below the table headers.
### *text-align* to align the writing to the left of some table cells and to the right of the others.
### *background-color* to change the background color of the alternating table rows.







# Events
## TRADITIONAL DOM EVENT HANDLERS 
### All modern browsers understand this way of creating an event handler, but you can only attach one function to each event handler. 

![event](https://user-images.githubusercontent.com/70091044/93263272-3c85e700-f7ae-11ea-9924-4a870f375986.PNG)

## USING DOM EVENT HANDLERS 
![event example](https://user-images.githubusercontent.com/70091044/93263897-10b73100-f7af-11ea-9c2e-ca68c5d3a1be.PNG)

## EVENT LISTENERS 
### Event listeners are a more recent approach to handling events. They can deal with more than one function at a time but they are not supported in older browsers. 
![even l](https://user-images.githubusercontent.com/70091044/93264359-ad79ce80-f7af-11ea-9301-73c10919ee8c.PNG)

## THE EVENT OBJECT 
### When an event occurs, the event object tells you information about the event, and the element it happened upon. 

![even object](https://user-images.githubusercontent.com/70091044/93264692-2aa54380-f7b0-11ea-961e-fa3412488b38.PNG)


## EVENT DELEGATION
### Creating event listeners for a lot of elements can slow down a page, but event flow allows you to listen for an event on a parent element. 

![event d](https://user-images.githubusercontent.com/70091044/93264937-8d96da80-f7b0-11ea-993a-0fe303931e6c.PNG)
