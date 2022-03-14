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
import Welcome from './Welcome';
import NavBar from './NavBar';

function Home() {
	return (
		<>
			<Welcome name='Juan' />
			<NavBar />
		</>
	);
}
```

To keep in mind:

- We need to use parethensis when we use `return` because of [ASI](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi).
- As I wrote [before](#03-creating-an-element), an `element` in React is an `object` that is returned by `React.createElement()` and as we know we can not return many object in a function, what we can do is to return an object that contents many others, that is the reason because we need to wrap the element. We can use `<> </>` or `<div> </div>`, the first is better because it doesn't add extra code ("div" tags). This has a name, [React.Fragment](https://reactjs.org/docs/fragments.html), so, third option: `<React.Fragment></React.Fragment>`.

#### 06. How To Visualize Elements

To see our React Elements on our page we need `ReactDOM.render()` and we have to tell it _what_ we want to render and _where_. Usually, we'll have a React Element like `<App />` that will contain many other, this is our _what_, and then we'll need a `<div id="root"></div>` element located in our `index.html`, we've to capture it and then use it (`ìndex.js` my entry point), this is our _where_, so:

```js
/// index.js
import ReactDOM from 'react-dom';

const root = document.querySelector('#root'); // <div id="root"></div>

ReactDOM.render(<App />, root); // <App /> must be imported
```

#### 07. JSX

We can say that JSX is syntactic sugar for `React.createElement()`. But what is it exactly? [It is a syntax extension to JavaScript](https://reactjs.org/docs/introducing-jsx.html). It allows us write HTML-like markup inside a JavaScript file.

```js
const paragraph = <p>This is a React element</p>; // JSX

const paragraph = React.createElement('p', {}, 'This is a React element');
```

We can see how [Babel compile our JSX element](https://babeljs.io/repl#?browsers=&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=MYewdgzgLgBADgQwE4IOYrgCxgXhgHjgD4AVTASwhkpgRgCUBTBYWRgG0YFtGwp8A9MSA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact&prettier=false&targets=&version=7.17.6&externalPlugins=&assumptions=%7B%7D). That is because our browser doesn't understand `JSX` code. So, this tool converts our JSX to JS code.

To keep in mind:

- JSX is an object because that is what `React.createElement()` returns.
- We can use JS expressions inside JSX by wrapping them with `{}` curly braces. They are like a "window into JS".
- We can use self-closing tags (as long as the element doesn't contain children).

#### 08. Props

Props is an object. Attributes on Components get converted into that object. React Components use props to comunicate with each other and it's its only argument. Every Component can pass some information to its child component by giving them props.

```js
// child component
function User(props) {
	return <h2>Hi, {props.user}</h2>; // it will receive information from its parent component
}

// parent component
function Welcome() {
	return (
		<>
			<h1>Welcome</h1>
			<User name='Emilia' />
		</>
	);
}
```

To keep in mind:

- Keep Components pure. That means: they should never change any arguments (props) they receive.

#### 09. Conditional Rendering

We can conditionally render one thing instead of another, there are many ways to achieve that, here are some of them:

- if - else

```js
if (user) {
	return <p>Hi {user}</p>;
} else {
	return <p>Hi guest</p>;
}
```

- ? ternary operator

```js
const user = "Emil"; // user is truthy, so it will show the name
  return <p>Hi {user ? user : "guest"}</p>;
}
```

- && and operator

```js
const loggin = true; // because it's true, it'll show a welcome message
return <p>{loggin && `You're welcome`}</p>;
```

#### 10. Rendering List

[We can render multiple components at once](https://reactjs.org/docs/lists-and-keys.html). To do it we use `map()` or `filter()` in case that we need to filter out our data.

```js
function List() {
	const sports = [football, volley, tennis];

	const listSports = sports.map((sport) => <li key={sport}>sport</li>);

	return <ul>{listSports}</ul>; // each <li> will be displayed correctly
}
```

To keep in mind:

- Each `<li key={uniqueID}></li>` needs an unique id to identify. It shouldn't be its index position and shouldn't be modified.

#### 11. CLSX

I found [this library](https://github.com/lukeed/clsx/) to work with classes more easily. We can't only give it normal values but also JS expressions and create conditional classes.

#### 12. Events

Like in vanille JS, event handlers are functions that will be triggered in response to user interactions. How can we add them?

1. Define a function inside our component.
2. Pass it as a prop to the appropiate JSX tag.

```js
// step 1
function WelcomeButton({ message }) {
	function handleClick() {
		// they have access to the component’s props because there are inside the component
		alert(message);
	}

	return (
		// step 2
		<button onClick={handleClick}>Click me to see the message</button>
	);
}

function App() {
	return (
		</div>
			<h1>Hi!</h1>
			<WelcomeButton message='Welcome!' />
		</div>
	);
}
```

To keep in mind:

- We have to pass the name of the function rather than calling it: `<button onClick={handleClick}>` and **not** `<button onClick={handleClick()}>`. In the first case, React will call the function only when we the user clicks the button, in the other example, React calls it during the rendering.
- Naming convention: `handleSubjectEvent` => `handleNameChange`
- We can also define an event handler inline in the JSX tag (for short functions).
- [Event Propagation](https://beta.reactjs.org/learn/responding-to-events#event-propagation): as occurs in JS, event handlers will catch events from any children your component might have. We need to call `e.stopPropagation()` to keep the event from going up to its parent components. So, first we use this method and then call the function we want.
- `e.stopPropagation()` ≠ `e.preventDefault()`.

#### 13. State

`State` is the way that React “remembers” things: the current time, the current input value, etc. When we have a component with data that we want to update it and re-render it, we can not do it through local variables since they don't persist between renders (because React re-renders, it does it from scratch, that means it doesn't see any changes in these variables) and their changes don't trigger renders. So, `useState` Hook helps us doing exactly what we need, it's a function that returns the following:

- a variable to persite data between renders
- and a function to update that variable and trigger renders.

```js
const [currentValue, setCurrentValue] = useState(initialValue); // currentValue starts with the initialValue
```

We can update immutable (they are unchangeable or 'read only') values in this way like numbers, strings and booleans. But what if we have objects or arrays? We'll see...

To keep in mind:

- Hooks should be called at the top level of the components.
- Don't use them inside `if` (or any conditionals), loops, etc.
- The parent component can’t change the state variables, they are private to the componenent where they were declared

#### 14. Immutability: Update Arrays and Objects in State

When using methods like `.push` or `.unshift` what we are doing is changing the array, the same with objects if we do something like `property.a = newValue;`, and it's key when working with React not to **mutate** them. Every update that we have to do, we have to create a new value, leaving the old one untouched and that's because React needs a way to know if we've changed the `state`. So, we can say that if we want to update a value and then React triggers renders, we have to create a copy of our array/object and modify them, otherwise it doesn't work.

```js
// some examples with array
const [...users, newUser] // add
const [removeUser, ...users] // remove the first one, I'll keep the rest of users
const removeLastOne = users.slice(0, users.length - 1)

// some examples with object
const {...users, newUser: 'Emil'} // in this way we can add and update a key
const {keyToRemove, ...users}  = users
```

#### 15. How To Pass Down Function As Props

A parent component can pass down functions as prop to its children. First, we have to make sure that the component which handles the `state` is the parent, that means it's a `stateful component`. And the child component would be a `stateless component`. Also, we've to pay attention to the name of these function props. An example:

```js
function Welcome() {
	// parent component handles the state
	const [name, setName] = useState('');

	const handleNameChange = (event) => {
		setName(event.target.value);
	};

	return (
		<>
			<h1>Welcome {name}</h1>
			<NameChildComponent name={name} onNameChange={handleNameChange} />
		</>
	);
}

// child component
function NameChildComponent(props) {
	const { name, onNameChange } = props;
	return (
		<form>
			<input value={name} onChange={onNameChange} />
		</form>
	);
}
```
