# Learning React

1. What is React?
It’s a JavaScript [library](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/) for building User Interfaces created and mostly maintained by Facebook. 
The UI is composed of small units (text boxes, buttons, images, etc) and React allows us to combine them into reusable and nestable components and then rendering them and updating the UI whenever it changes. 

2. How to install?
`npm install react` once installed we can import it:
`import React from "react"` We have to do it in every js file where we need it because every js file is a standalone module, so the content of one file (variables, functions, imports) don't affect other files.


3. Creating an [element](https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html#elements-describe-the-tree)
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
To render and updating our elements we also need the **ReactDOM** package. We specially require the method `render()` so we can importe it by using the **named imports**so: `import { render } import from "react-dom` or `import ReactDOM from "react-dom";`. 

5. Component


