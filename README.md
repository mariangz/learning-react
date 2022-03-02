# Learning React

1. What is React?
It’s a JavaScript [library](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/) for building User Interfaces created and mostly maintained by Facebook. 
The UI is composed of small units (text boxes, buttons, images, etc) and React allows us to combine them into reusable and nestable components and then rendering them and updating the UI whenever it changes. 

2. How to install?
`npm install react` once installed we can import it:
`import React from "react"` We have to do it in every js file where we need it because every js file is a standalone module, so the content of one file (variables, functions, imports) don't affect other files.


3. Creating an element
In JS we use `document.createElement` but in React we use a method `React.createElement`. The first one return a **DOM element** and thr last one an **object**
