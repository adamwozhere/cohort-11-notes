# React

28, 29 Nov, 1, 5 Dec

[https://reactjs.org/docs/hello-world.html](https://reactjs.org/docs/hello-world.html)

- Made by Facebook
- Componentises things so they are reusable
- Built from components, each component can have child components
- Airbnb is a React app
- Can use chrome extension ‘wappalyzer’ (web app analyser) to inspect what tech a site uses

## Installing Node

Node is a JavaScript runtime - allows JS to be run outside of the browser; e.g. command line or backend apps and servers.

For Mac: [https://github.com/nvm-sh/nvm#installing-and-updating](https://github.com/nvm-sh/nvm#installing-and-updating)

For Win: [https://www.freecodecamp.org/news/nvm-for-windows-how-to-download-and-install-node-version-manager-in-windows-10/](https://www.freecodecamp.org/news/nvm-for-windows-how-to-download-and-install-node-version-manager-in-windows-10/)

- Once NVM (Node Version Manager) is installed you can check `nvm --version`
- Then install Node: `nvm install --lts` (Long Term Support)
- Can use `nvm install latest` but better to use `lts`
- Set NVM to use desired version of Node `nvm use lts`
- Should now be able to use `npm` (Node Package Manager)

## Create-react-app

Use `create-react-app` to create a base React app with a git repository initialised

- Navigate to a folder, right-click, `Git Bash Here`
- `npx create-react-app my-app-name` will create a folder `my-app-name` with base React project and an initialised git repository
- Can also install `create-react-app` globally and use that:
  - `npm install -g create-react-app` then:
  - `create-react-app my-app-name`
  - Note: Had deprecation warnings and vulnerabilities when using both: not sure what is best?

## React App

- Main file is `App.js` You can then import all components into there
- `public` folder can hold static files (like an `images` folder etc.) you can then use the file-path in a `img src="filepath"` just like normal
- Or you can keep images in `src` folder and `import myImg from './my-img.png'` etc. and use it as `img src={myImg}`

## React Components

- React components are reusable blocks of code; they allow us to not repeat ourselves
- They can be created in two ways:
  - Functional components
  - Class components
- Components are declared with a capital letter, e.g. `MyComponent` not `myComponent`
- Components can have `props` which are like passing in a variable to a component
- Can have `state`, special ‘variables’ that contain values that will change; this allows us to make components interactive
- State always passes down the document tree. It cannot pass back upwards.
- Components are usually (but don’t have to be) written with `JSX` a language / syntax that allows us to write html within JS:
  - JSX can have JS expressions / variables inside: use curly brackets `prop={myValue}`
  - Names are always camelCase, and some names are different, e.g. `class` as that is a JS protected keyword. Use `className="my-class-name"` or `className={myClassNameVariable}` etc.
  - To enable proper linting, use emmet etc. make sure that VSCode recognises the language in the bottom-right corner as `JavaScript React`

### Basic functional component

- functional components are declared in their own JS file in usually in `src/components` folder:
- Filename should be the same as the component (including capital letter) `MyComponent.js`
- The `default` keyword is used when only exporting one function from a file
  - You can export inline: `export default function MyComponent() {`
  - Imports are written at the top of the file
  - Exports at the bottom

```jsx
components / MyComponent.js;

function MyComponent({ prop1, prop2 }) {
  return <div class="my-component">...</div>;
}

export default MyComponent;
```

- Import the component into the parent, e.g. `App.js`

```jsx
App.js;

import MyComponent from './components/MyComponent';

function App() {
  return (
    <div className="App">
      <MyComponent />
    </div>
  );
}

export default App;
```

- Imports in React are usually done in two ways:
  - `import MyComponent from './path';` to import a `default` component
  - `import { useState, useEffect } from 'react';` to import functions from a file that contains multiple named exports

### Props

`props` let us pass in variables to components, you declare them all in one object and pass it in to the component function, you can then use those props within the component:

```jsx
components/MyComponent.js

function MyComponent({ title, text }) {
	return (
		<div>
			<h2>{title}</h2>
			<p>{text}</h2>
		</div>
	);
}

export default MyComponent;
```

### useState

`useState` is a React `hook`. It does something when called to change the `state` of the component.

- always create states in a pair - the actual state and then a set method (set method seems to be actually created by react but you must pass in the name to the array.)
- declare `useState` with array `destructuring`
- you can pass in a default state value directly into `useState` e.g. `false`

```jsx
const [darkMode, setDarkMode] = useState(false);
const [currentUser, setCurrentUser] = useState();
```

- Create a function to actually alter the state
- Note: always alter the state through the `set` function and not with the state variable directly

```jsx
const toggleDarkMode = () => {
  setDarkMode(!darkMode);
};
```

- The `toggleDarkMode` function can then be called through a button with `onClick`
- Now we can query the state to describe what the component looks like conditionally

```jsx
components/MyComponent.js

function MyComponent({ title, text }) {

	const [darkMode, setDarkMode] = useState(false);

	const toggleDarkMode = () => {
		setDarkMode(!darkMode);
	};

	return (
		<div className={`my-component ${darkMode ? 'darkMode' : ''}`}>
			<button onClick={toggleDarkMode}>Toggle Dark Mode</button>
			<h2>{title}</h2>
			<p>{text}</h2>
		</div>
	);
}

export default MyComponent
```

### Lifting up state

- State can be lifted up (moved to a parent function)
- The state can then be passed down the document tree by passing it in to a component as a prop.
- e.g. create the `darkMode` state on the `App` component, then pass down `darkMode` to child components as a prop
  - Alternatively don’t pass down a prop, but set `darkMode` class on `App`
  - Then target the styling in CSS: `.App.dark-mode .my-component { background-color: black }`

### useEffect

`useEffect` is like a special function that is a side effect of some stage happening within the components lifecycle, for example when the component mounts.

- Still don’t fully understand this; perhaps similar in a way to an `Event Listener` runs when something else happens, when state changes etc. ?
- the empty array `[]` at the end is where the other ‘listeners’ go, empty means it will just run when the component `mount`s (added to the DOM) ?

```jsx
useEffect(() => {
	...
},[]);
```

## Tasks:

Refactor the `advice-generator-app` with react components.

- create a function to get the data from the API
- put that function in `useEffect` so that it can be called on load
- set the function so it’s called from the button `onClick`

## Routing

A route is usually a different page - a different ‘route’ on the site e.g. `/` for the home or index page or `/about` etc. We can use routing to create a Single Page App: [https://www.w3schools.com/react/react_router.asp](https://www.w3schools.com/react/react_router.asp)

- Create a new react app `npx create-react-app multipage-app`
- Install react-router-dom `npm i react-router-dom -D`
  - `i` is short for `install`
  - `-D` is short for `--save-dev` (saves as a development dependency - it is not needed in the final build)
- Import into the `App.js` and use `BrowserRouter`, `Routes` and `Route` to define the different page structures

```jsx
src / App.js

import { BrowserRouter, Route, Route } from 'react-router-dom';

// import Pages and Layouts...

function App() {
	return (
		<BrowserRouter>
			<NavComponent/>
			<Routes>
				<Route path="/" element={<Layout/>}>
					<Route index element={<Home/>}/>
					<Route path="/about" element={<About/>}/>
				</Route>
			</Routes>
		<BrowserRouter/>
	);
}

export default App;
```

- `route`s can be nested inside each other, here the `Layout` contains an `<Outlet/>` component where the inner-nested `route`s will be rendered e.g. `Layout` could contain a navbar that is rendered on each page, or there could be various layouts like a normal, or a logged-in dashboard that each show child pages - (In the case of a navbar on every page, its probably easier to just place it outside of routes: `<NavComponent/>` )
- Use `index` attribute on the main, default page to be displayed
- `<> ... </>` is a `Fragment` tag. React can only return one node so usually we render one `div` with contents inside, but sometimes it’s better to prevent div soup, so a `Fragment` will create an group for us without the extra html element
- Use the `<Link to="/path">` tag to link to other routes within a Single Page App as this prevents the browser from reloading (absolute paths e.g. to external sites should be normal `anchor` tags

```jsx
Layout / Main.js;

import React from 'react';
import { Link, Outlet } from 'react-router-dom';

const Layout = () => {
  return (
    <>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          ...
        </ul>
      </nav>
      <Outlet />
    </>
  );
};

export default Layout;
```

- Pages can be created as as a normal react component

```jsx
pages / Home.js;

import React from 'react';

const Home = () => {
  return (
    <div>
      <h1>Home page</h1>
    </div>
  );
};

export default Home;
```

## Tasks:

- Add a light/dark mode toggle to the multi-page app
- Add a `Dashboard` Layout with the image (can clone from Olly’s repo) and use `useState` to select a status for the cat and display it on the page e.g. Scared, Surprised etc.
- Can use SASS to use CSS nesting `npm install --save-dev sass` or install globally `npm install -g sass` [https://sass-lang.com/](https://sass-lang.com/)

## Deploying to Netlify

- Sign in with GitHub to [https://www.netlify.com/](https://www.netlify.com/)
- Add new site
- Import existing GitHub project
- Select repo
- Check build commands are default: `npm run build`

## Forms / Events

5 Dec

- In React you generally add event listeners to directly to the element rather than getting an object by ID and then adding an event listener

```jsx
Form.js

const submitHandler = (e) => {
	e.preventDefault();
	...
}

return (
	<form action="" id="myForm" onSubmit={submitHandler}>
		...
	</form>
);

```

- When working with inputs you need to set the state variable of the input via a method on the element e.g. `onChange, onClick, onInput`
- The value of the input should then equal the state variable e.g. `value={state}`
- Event handler functions can be written inline if it's simple, e.g. just setting state:

```jsx
Form.js

const [name, setName] = useState('');

return (
	<form>
		...
		<input type="text" name="name" id="name" value={name} onChange={(e) =>
		setName(e.target.value)}>
	</form>
);

```

- This sort of pattern in React is called 'control values', 'controlled' inputs ???

  - Event sets state, state sets value

- You can create instanced inputs in the HTML by mapping over them:

```jsx
Form.js;

return (
  <fieldset>
    <legend>Allergies</legend>
    {allergyOptions.map((option, i) => {
      return (
        <div key={`option-${i}`}>
          <label htmlFor="{option}">{option.toUpperCase()}</label>
          <input
            type="checkbox"
            name="allergies"
            id={option}
            value={option}
            checked={allergies[i]}
            onChange={() => handleCheckboxChange(i)}
          />
        </div>
      );
    })}
  </fieldset>
);
```

- Add handleer code:

```jsx
Form.js;

const allergyOptions = ['peanuts', 'seafood', 'other'];
const [allergies, setAllergies] = useState(
  new Array(allergyOptions.length).fill(false)
);

const handleCheckboxChange = (position) => {
  const updatedCheckedState = allergies.map((item, index) =>
    index === position ? !item : item
  );
  setAllergies(updatedCheckedState);
};
```

- Default state of `allergies` is set to a new array that is the same length of `allergyOptions`
- An index is passed into `handleCheckboxChange`
- Map over the `allergies` array comparing array index, `i` to the checkbox index, `position`
- If they are the same, then toggle the checkbox, `!item` otherwise keep it the same
- Use the new array of updated allergies to change the state `setAllergies(updatedCheckedState);`

- NOTE: think I mostly understand this, but I have no idea what the `key={`option-${i}`}>` is or does ???
- Still don't understand `useState`, could that be used instead - just listen for the change of the state, then handle actually changing / toggling checkboxes etc.
- How / where do you write code to do validation??

# Task:

- Complete the form in React? - can't think how to get the 'other - (specify)' option working with the allergies inputs
