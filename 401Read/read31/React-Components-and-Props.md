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
