# Learning React

#### 01. What is React?

It’s a JavaScript [library](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/) for building User Interfaces created and mostly maintained by Facebook. 
The UI is composed of small units (text boxes, buttons, images, etc) and React allows us to combine them into reusable and nestable components and then rendering them and updating the UI whenever it changes. 


#### 02. How to install/start?

~~`npm install react` once installed we can import it:~~ 
~~`import React from "react"` We have to do it in every js file where we need it because every js file is a standalone module, so the content of one file (variables, functions, imports) don't affect other files.~~ 

As of React version 17, we don't need to import React anymore. And to start a project: `create-react-app name-app`.


#### 03. Creating an element

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


#### 04. ReactDOM

To render and updating our elements we also need the **ReactDOM** package. We specially require the method `render()` so we can importe it by using **named imports**: `import { render } import from "react-dom` or also `import ReactDOM from "react-dom";` is possible. 


#### 05. Component

It's a function that returns one React Element. This element [can have many children](#03-creating-an-element). Components are also UI building blocks (**elements** are also buildings blocks but the smallest ones in React) [and let us split the UI into independent, reusable pieces, and think about each piece in isolation](https://reactjs.org/docs/components-and-props.html). It accepts arbitrary inputs (called “props”).

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
- As I wrote [before](#03-creating-an-element), an `element` in React is an `object` that is returned by `React.createElement()` and as we know we can not return many object in a function, what we can do is to return an object that contents many others, that is the reason because we need to wrap the element. We can use `<> </>` or  `<div> </div>`, the first is better because it doesn't add extra code ("div" tags). This has a name, [React.Fragment](https://reactjs.org/docs/fragments.html), so, third option: `<React.Fragment></React.Fragment>`.


#### 06. How To Visualize Elements
To see our React Elements on our page we need `ReactDOM.render()` and we have to tell it *what* we want to render and *where*. Usually, we'll have a React Element like `<App />` that will contain many other, this is our *what*, and then we'll need a `<div id="root"></div>` element located in our `index.html`, we've to capture it and then use it (`ìndex.js`), this is our *where*, so:
```js
/// index.js
import ReactDOM from 'react-dom';

const root = document.querySelector("#root"); // <div id="root"></div>

ReactDOM.render(<App />, root); // <App /> must be imported
```


#### 06. JSX
We can say that JSX is syntactic sugar for `React.createElement()`. But what is it exactly? [It is a syntax extension to JavaScript](https://reactjs.org/docs/introducing-jsx.html). It allows us write HTML-like markup inside a JavaScript file.
```js
const paragraph = <p>This is a React element</p> // JSX

const paragraph = React.createElement("p", {}, "This is a React element")
```

We can see how [Babel compile our JSX element](https://babeljs.io/repl#?browsers=&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=MYewdgzgLgBADgQwE4IOYrgCxgXhgHjgD4AVTASwhkpgRgCUBTBYWRgG0YFtGwp8A9MSA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact&prettier=false&targets=&version=7.17.6&externalPlugins=&assumptions=%7B%7D). That is because our browser doesn't understand `JSX` code. So, this tool converts our JSX to JS code.

To keep in mind: 
- JSX is an object because that is what `React.createElement()` returns.
- We can use JS expressions inside JSX by wrapping them with `{}` curly braces. They are like a "window into JS".