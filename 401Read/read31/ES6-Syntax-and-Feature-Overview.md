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
