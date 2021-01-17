# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|31|[ES6 Syntax and Feature Overview](ES6-Syntax-and-Feature-Overview.md)
|31|[React - Hello World](React-Hello-World.md)
|31|[React - JSX](React-JSX.md)
|31|[React - Rendering Elements](React-Rendering-Elements.md)
|31|[React - Components & Props](React-Components-and-Props.md)











# ES6 Syntax and Feature Overview

## Variables and constant feature comparison

|Keyword | Scope | Hoisting | Can Be Reassigned | Can Be Redeclared |
|:---------: |:--------------:|:--------------:|:--------------:|:--------------:|
|var|Function scope|Yes|Yes|Yes
|let|Block| scope|	No|	Yes	|No
|const|	Block |scope|	No|	No|	No

## Arrow functions
### The arrow function expression syntax is a shorter way of creating a function expression. Arrow functions do not have their own this, do not have prototypes, cannot be used for constructors, and should not be used as object methods.
```javascript
let func = (a) => {} // parentheses optional with one parameter
let func = (a, b, c) => {} // parentheses required with multiple parameters
```
## Template literals
## Concatenation/string interpolation
### Expressions can be embedded in template literal strings.
```javascript
let str = `Release Date: ${date}`
```
## Multi-line strings
### Using template literal syntax, a JavaScript string can span multiple lines without the need for concatenation.
```javascript
let str = `This text
            is on
            multiple lines`
```
## Implicit returns
### The return keyword is implied and can be omitted if using arrow functions without a block body.
```javascript
let func = (a, b, c) => a + b + c // curly brackets must be omitted
```
## Key/property shorthand
### ES6 introduces a shorter notation for assigning properties to variables of the same name.
```javascript
let obj = {
  a,
  b,
}
```
## Method definition shorthand
### The function keyword can be omitted when assigning methods on an object.

```javascript
let obj = {
  a(c, d) {},
  b(e, f) {},
}
```
## Array iteration (looping)
### A more concise syntax has been introduced for iteration through arrays and other iterable objects.
```javascript
for (let i of arr) {
  console.log(i)
}
```
## Classes/constructor functions
### ES6 introducess the class syntax on top of the prototype-based constructor function.
```javascript
class Func {
  constructor(a, b) {
    this.a = a
    this.b = b
  }

  getSum() {
    return this.a + this.b
  }
}

let x = new Func(3, 4)
```
## Inheritance
### The extends keyword creates a subclass.
```javascript
class Inheritance extends Func {
  constructor(a, b, c) {
    super(a, b)

    this.c = c
  }

  getProduct() {
    return this.a * this.b * this.c
  }
}

let y = new Inheritance(3, 4, 5)
```
## Modules - export/import
### Modules can be created to export and import code between files.
```javascript
let func = (a) => a + a
let obj = {}
let x = 0

export {func, obj, x}
```
```javascript
import {func, obj, x} from './export.js'

console.log(func(3), obj, x)
```





# React - Hello World
## The smallest React example looks like this:
```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```
### It displays a heading saying “Hello, world!” on the page.





# React - JSX
## Consider this variable declaration:
```JSX
const element = <h1>Hello, world!</h1>;
```
### This funny tag syntax is neither a string nor HTML.

### It is called JSX, and it is a syntax extension to JavaScript. We recommend using it with React to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript.

## Why JSX?
### React embraces the fact that rendering logic is inherently coupled with other UI logic: how events are handled, how the state changes over time, and how the data is prepared for display.

### Instead of artificially separating technologies by putting markup and logic in separate files, React separates concerns with loosely coupled units called “components” that contain both. 
### Embedding Expressions in JSX
### In the example below, we declare a variable called name and then use it inside JSX by wrapping it in curly braces:
```JSX
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
### You can put any valid JavaScript expression inside the curly braces in JSX. For example, 2 + 2, user.firstName, or formatName(user) are all valid JavaScript expressions.

### In the example below, we embed the result of calling a JavaScript function, formatName(user), into an <h1> element.
```JSX
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
## Specifying Attributes with JSX
### You may use quotes to specify string literals as attributes:
```JSX
const element = <div tabIndex="0"></div>;
```
### You may also use curly braces to embed a JavaScript expression in an attribute:
```jsx
const element = <img src={user.avatarUrl}></img>;
```
### Don’t put quotes around curly braces when embedding a JavaScript expression in an attribute. You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.
```
Warning:

Since JSX is closer to JavaScript than to HTML, React DOM uses camelCase property naming convention instead of HTML attribute names.

For example, class becomes className in JSX, and tabindex becomes tabIndex.
```

## Specifying Children with JSX
### If a tag is empty, you may close it immediately with />, like XML:
```jsx
const element = <img src={user.avatarUrl} />;
```
### JSX tags may contain children:
```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```
## JSX Prevents Injection Attacks
### It is safe to embed user input in JSX:
```jsx
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
### By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.

## JSX Represents Objects
### Babel compiles JSX down to React.createElement() calls.

### These two examples are identical:
```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```
```jsx
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```
### React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this:
```jsx
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```
### These objects are called “React elements”. You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date.





# React - Rendering Elements
## Elements are the smallest building blocks of React apps.

### An element describes what you want to see on the screen:
```jsx
const element = <h1>Hello, world</h1>;
```
### Unlike browser DOM elements, React elements are plain objects, and are cheap to create. React DOM takes care of updating the DOM to match the React elements.
## Rendering an Element into the DOM
### Let’s say there is a <div> somewhere in your HTML file:
```jsx
<div id="root"></div>
```
### We call this a “root” DOM node because everything inside it will be managed by React DOM.

### Applications built with just React usually have a single root DOM node. If you are integrating React into an existing app, you may have as many isolated root DOM nodes as you like.

### To render a React element into a root DOM node, pass both to ReactDOM.render():
```jsx
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```
## Updating the Rendered Element
### React elements are immutable. Once you create an element, you can’t change its children or attributes. An element is like a single frame in a movie: it represents the UI at a certain point in time.

### With our knowledge so far, the only way to update the UI is to create a new element, and pass it to ReactDOM.render().

### Consider this ticking clock example:
```jsx
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```




# React - Components & Props
## Function and Class Components
### The simplest way to define a component is to write a JavaScript function:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
### This function is a valid React component because it accepts a single “props” (which stands for properties) object argument with data and returns a React element. We call such components “function components” because they are literally JavaScript functions.

### You can also use an ES6 class to define a component:
```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
### The above two components are equivalent from React’s point of view.

## Rendering a Component
### Previously, we only encountered React elements that represent DOM tags:
```jsx
const element = <div />;
```
### However, elements can also represent user-defined components:
```jsx
const element = <Welcome name="Sara" />;
```
### When React sees an element representing a user-defined component, it passes JSX attributes and children to this component as a single object. We call this object “props”.

### For example, this code renders “Hello, Sara” on the page:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
