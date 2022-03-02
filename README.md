# Learning React

1. What is React?

It’s a JavaScript [library](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/) for building User Interfaces created and mostly maintained by Facebook. 
The UI is composed of small units (text boxes, buttons, images, etc) and React allows us to combine them into reusable and nestable components and then rendering them and updating the UI whenever it changes. 

2. How to install?

`npm install react` once installed we can import it:
`import React from "react"` We have to do it in every js file where we need it because every js file is a standalone module, so the content of one file (variables, functions, imports) don't affect other files.


3. Creating an [element](https://reactjs.org/docs/rendering-elements.html)

In JS we use `document.createElement()` but in React we use a method `React.createElement()`. The first one return a **DOM element** and the second one an **object**, so `React.createElement("p")` is equal to:
```js
{
  type: "p", 
  key: null, 
  ref: null, 
  props: Object, 
  props: Object,
  _owner: null,
  _store: Object
}
```
and that is because React works in a [virtual DOM](https://stackoverflow.com/questions/21965738/what-is-virtual-dom).
If we use [console.dir](https://developer.mozilla.org/en-US/docs/Web/API/Console/dir) we can see all its properties and manipulate them. For example, if I want to create this element `<p class="active">I'm learning React</p>` I'd do something like this `React.createElement("p", {className: "active}, "I'm learning React")` => `(React.createElement(type, options/Reactclass, children)`).
```js
{
  type: "p",
  key: null,
  ref: null,
  props: Object,
  className: "active",
  children: "I'm learning React",
  _owner: null,
  _store: Object
}
```
4. ReactDOM

To render and updating our elements we also need the **ReactDOM** package. We specially require the method `render()` so we can importe it by using **named imports**: `import { render } import from "react-dom` or also `import ReactDOM from "react-dom";` is possible. 

5. Component

It's a function that returns one React Element. This element can have many children. Components are also UI building blocks (**elements** are also buildings blocks but the smallest ones in React) [and let us split the UI into independent, reusable pieces, and think about each piece in isolation](https://reactjs.org/docs/components-and-props.html). It accepts arbitrary inputs (called “props”).

Note: we have to use capital letter to name them (UpperCamelCase): 
```js
export default function Navbar() {
    return (
        <ul>
            <li>Home</li>
            <li>Contact</li>
        </ul>
    );
}

export default function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// shorter
const Welcome = ({name}) => <h1>Hello, {name}</h1>; // but in this case we can't use default export
```
These ones are **funcional components** because the Component are definened as a function but also there are **Class Component**. We can "translate" them:

```js
// in this case, we should import the Component object
import React, { Component } from "react";

export default class Navbar extends Component {
  render() {
    return (
      <ul>
        <li>Home</li>
        <li>Contact</li>
      </ul>
    )
  }
}

export default class Welcome extends Component {
  constructor(props) {
    super(props) 
    //why do we need super here? because we have a constructor,
    //I'd like to go deeper to understand better this point
  }

  render() {
    return  <h1>Hello, {this.props.name}</h1>;
  }
}
```

Why do we export a component? Bacause we can nest it inside other components.

```js
import Welcome from "./Welcome";
import NavBar from "./NavBar";

function Home() {
  return (
    <> 
      <Welcome name="Juan" />
      <NavBar />
    </>
  )
}
```

Two things to keep in mind:
- We need to use parethensis when we use `return` because of [ASI](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi).
- As I wrote before, an `element` in React is `object` that is returned by `React.createElement()`? And as we know we can not return many object in a function, what we can do is to return an object that contents many others, that is the reason because we need to wrap the element. We can use `<> </>` or  `<div> </div>`, it seems like the first is better because it doesn't add extra code ("div" tags). This has a name, [React.Fragment](https://reactjs.org/docs/fragments.html), so, third option: `<React.Fragment></React.Fragment>`.