# React Documentation
## Documentation Links
#### React & JavaScript 
- [JavaScript Info](https://javascript.info/)
- [Official React Documentation](https://react.dev/)
#### HTML
- [HTML Cheat Sheet](https://htmlcheatsheet.com/)
- [W3C HTML Reference](https://www.w3schools.com/tags/ref_byfunc.asp)
#### CSS
- [CSS W3schools Core Building Blocks](https://www.w3schools.com/w3css/w3css_references.asp)
- [CSS How To W3schools](https://www.w3schools.com/css/default.asp)
#### Vite
- [Vite Official Documentation](https://vitejs.dev/guide/)
#### Project Guidance
- [Redux Style Guide: Structure files as feature folders](https://redux.js.org/style-guide/style-guide#structure-files-as-feature-folders)
- [Bulletproof React: Project structure](https://github.com/alan2207/bulletproof-react/blob/master/docs/project-structure.md)
- [Feature-Sliced Design: Layers overview](https://feature-sliced.design/docs/reference/layers)
- [Vite Guide: Project root & entrypoint](https://vitejs.dev/guide/#index-html-and-project-root)


## Table of Contents
- [Documentation Links](#documentation-links)
- [Setup and Installation](#setup-and-installation)
- [Project Structure and Pathing](#project-structure-and-pathing)
- [Core React Concepts](#core-react-concepts)
- [Core React Framework](#core-react-framework)
- [Props](#props)
- [State](#state)
- [Render](#render)
- [Events](#events)
- [Context](#context)
- [Hooks](#hooks)
- [Usage Examples](#usage-examples)
- [Key Features](#key-features)
- [Import Patterns](#import-patterns)

## Setup and Installation
You'll need to have a few things set up and start running `react` applications on your local machine.
### Node.js & npm
To get started with React, you need to have Node.js and npm (Node Package Manager) installed on your machine. You can download and install them from [Node.js official website](https://nodejs.org/).
```shell
npm -v # Check if npm is already installed and on the PATH
nodejs -v # Check if Node.js is already installed and on the PATH
winget install NodeJS.LTS # This installs Node.js and npm on Windows
# or
sudo apt install nodejs npm # use apk for alpine
nodejs -v # Make sure it's installed by checking nodejs version
npm -v # Make sure it's installed by checking npm version

# No! -g flags 
# No! npm install npm     # This can lead to version conflicts and unexpected behavior.
```
### npm
npm - Node Package Manager is the worlds largest software registry. Open source developers from around the world use npm to share and reuse code. npm makes it easy for developers to create, share, and distribute code.

### Setup Dev Server
To run React applications locally, you can use a local web development server. One popular choice is `vite`, which is a fast build tool that provides a development server with hot module replacement and easy stop start of the server.
```shell
mkdir my-new-project-parent # Create a new parent directory for your project if you need it.
cd my-new-project-parent # Navigate into the project parent directory.
npm init -y # Initializes a new Node.js project; -y flag accecpts all default settings
npm install --save-dev eslint # Installs eslint as a development dependency
npm install --save-dev vite # Installs vite as a development dependency
npm install --save-dev vite @vitejs/plugin-react # Installs vite with react plugin as a development dependency
```

Now you've got the core installs done, you can create a new React project using Vite's project scaffolding tool:
```shell
npm create vite@latest my-new-project-name react # Sets up a new React project using Vite
```
If Vite did not detect React automatically, you can specify it like this:
```shell
npm create vite@latest my-new-project-name -- --template react
```
```shell
press h + enter to show help
  Shortcuts
  press r + enter to restart the server
  press u + enter to show server url
  press o + enter to open in browser
  press c + enter to clear console
  press q + enter to quit
# This lets vite act as your compiler and local web server.
# After shutting the mini server down once, you can start it again with:
npm run dev

```
### Advanced Project Setup
[Vite Production Build & Deployment](https://vite.dev/guide/build)
When you're ready to create a production build of your React application, you can use the following command:
```shell
vite --config mypath/vite.config.js # Use a custom Vite config file or location if needed
npm install --save <my package name> # Save any additional production packages your project needs to your package.json
npm install --save-dev <my dev package name> # Save any additional dev packages your project needs
npm install # Installs all dependencies listed in package.json
npm run build # Builds the project for production
vite build --base=/my/public/path/ # Specify the base path for your production build the base is '/' by default
```
### Other Advanced Configurations
Remember the key terms & that they are often used interchangeably between Vite and npm:
- Build = Production
- Serve = Development
- Command = Script

Vite allows for extensive configuration through a `vite.config.js` or `vite.config.ts` file in the root of your project. Here you can customize various aspects of the build and development process, such as plugins, server settings, and build options.
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000, // Change the development server port
    open: true, // Open the browser automatically
  },
  build: {
    outDir: 'dist', // Specify the output directory for the build
    sourcemap: true, // Generate source maps for debugging
  },
})
```

Vite and npm allow you to set environment variables to customize your build and development process. You can set the `NODE_ENV` variable to specify the environment mode:
```shell
export NODE_ENV=development # for serve
export NODE_ENV=production # for build
```

Both Vite and npm use the terms "scripts" and "commands" interchangeably to refer to the same thing. In npm, scripts are defined in the `package.json` file under the "scripts" section. These scripts can be executed using the `npm run <script-name>` command.

### Intellisense Hints for VSCode
Because the nature of javascript is dynamic not static typing, linters and intellisense are crucial while developing. To ensure your react and JavaScript linters work properly type hints can tell them to ignore certain files or folders.
```typescript
// This typscript file will set off linters if it's used in a jsx file.
// The @type hint tells VSCode to treat this file as a Vite config file for intellisense purposes.
/** @type {import('vite').UserConfig} */
export default {
  // ...
} satisfies import('vite').UserConfig;
```

### JSON Server for Mock APIs
To set up a mock API server using JSON Server, you can follow these steps:
```shell
npm install json-server --save-dev
```
Create a `db.json` file in the root of your project with some sample data:
```json
{
  "assets": [
    { "id": 1, "name": "Northern Timber Plot", "type": "Land", "status": "Active" },
    { "id": 2, "name": "Riverside Acres", "type": "Property", "status": "Pending" }
  ],
  "users": [
    { "id": 1, "name": "Admin User", "role": "SuperAdmin" }
  ]
}
```
Each top-level key (like assets or users) automatically becomes a RESTful endpoint.

Start the JSON Server with the following command:
```shell
npx json-server --watch db.json --port 8008
# --watch: Automatically restarts the server if you edit your db.json
# --port 8008: Specifies a port to avoid conflicts with your React app (which typically uses 3000).
```
Now you can access the mock API endpoints like:
```jsx
useEffect(() => {
  fetch("http://localhost:8008/assets")
    .then(response => response.json())
    .then(data => setAssets(data))
    .catch(error => console.error("Error fetching assets:", error));
}, []);
```

### JSON Server Advanced Options
Remember JSON server has to be started separately from your React development server.
#### Using the `--status` flag
```shell
# This will make every request return a 404 Not Found
npx json-server db.json --port 8008 --status 404
```
### Using middleware.cjs
#### Create a `middleware.cjs` file in the root of your project:
```cjs
// middleware.cjs
module.exports = (req, res, next) => {
  // Example: allow CORS in dev
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization");
  res.setHeader("Access-Control-Allow-Methods", "GET,POST,PUT,PATCH,DELETE,OPTIONS");

  if (req.method === "OPTIONS") return res.sendStatus(204);

  next();
};

```
Start JSON Server with the middleware:
```shell
npx json-server@0.17.4 db.json --port 8008 --middlewares ./middleware.cjs
```
#### Standard Response Codes
Code	Meaning	Typical Usage in your Project
- `201`	Created	Successfully added a new Land Asset via POST.
- `400`	Bad Request	Form data is missing a required field like name.
- `401`	Unauthorized	The user isn't logged in to Miller Land Management.
- `404`	Not Found	Trying to fetch an asset ID that doesn't exist.
- `500`	Internal Error	The mock "database" had a catastrophic failure.


### Other Useful Packages
```shell
# TailwindCSS
npm install --save-dev tailwindcss
npx tailwindcss init

npm install react-router-dom --save # React Router for routing
npm install axios --save # Axios for making HTTP requests
npm install @base-ui/react --save # BaseUI for UI components
npm install redux react-redux --save # Redux for state management
npm install styled-components --save # Styled-components for styling
npm install framer-motion --save # Framer Motion for animations
npm install react-helmet --save # React Helmet for managing document head
npm install react-icons --save # React Icons for icons
npm install react-query --save # React Query for data fetching
npm install @testing-library/react # React Testing Library for testing
npm install eslint --save-dev # ESLint for linting
npm install prettier --save-dev # Prettier for code formatting
npm install husky --save-dev # Husky for Git hooks
npm install lint-staged --save-dev # Lint-staged for running linters on staged files
npm install commitizen --save-dev # Commitizen for standardized commit messages
npm install conventional-changelog-cli --save-dev # Conventional Changelog for generating changelogs
npm install semantic-release --save-dev # Semantic Release for automated releases
npm install @babel/core @babel/preset-env @babel/preset-react --save-dev # Babel for JavaScript transpiling
npm install webpack webpack-cli webpack-dev-server --save-dev # Webpack for module bundling
npm install parcel-bundler --save-dev # Parcel for module bundling
npm install loglevel --save-dev # logging library
npm install dotenv --save-dev # dotenv for environment variables
npm install prop-types # PropTypes for type checking
```

## Project Structure and Pathing
#### `root`
The root directory typically contains configuration files and folders for source code, public assets, and dependencies.

In the case of React the root directory is where the index.html file is located along with the src/ folder that contains all the React components and application logic.

#### `base` which is `/`
relative path `/`
absolute path `/root/`
#### `src` 
relative path `/src/`
absolute path `/root/src/`
**Co-location** (great for medium apps)
```markdown
features/
├── products/
│   ├── ProductGrid.jsx
│   ├── ProductCard.jsx
│   ├── ProductFilters.jsx
│   └── useProducts.js    # Custom hook
├── cart/
│   ├── Cart.jsx
│   ├── CartItem.jsx
│   └── useCart.js
```

**The "folder-per-component" approach** (for large apps):
```markdown
components/
├── ProductCard/
│   ├── ProductCard.jsx
│   ├── ProductCard.styles.js
│   ├── ProductCard.test.js
│   └── index.js          # Re-exports
```
```jsx
// ProductGrid.jsx
const ProductCard = ({ product }) => { /* 30 lines */ };
const ProductFilters = ({ onFilter }) => { /* 40 lines */ };
const ProductGrid = () => { /* 50 lines using above */ };

export default ProductGrid;
```

The Sweet Spot: Component-per-File with Logical Grouping
File Structure:
```markdown
src/
├── components/
│   ├── common/          # Shared across app
│   │   ├── Button.jsx
│   │   ├── Input.jsx
│   │   ├── Card.jsx
│   │   └── Modal.jsx
│   ├── layout/          # Layout components
│   │   ├── Theme.jsx
│   │   ├── Navigation.jsx
│   │   ├── Background.jsx
│   │   ├── ContentContainer.jsx
│   │   ├── Header.jsx
│   │   ├── ContentBody.jsx
│   │   ├── Footer.jsx
│   │   └── Sidebar.jsx
│   └── features/        # Feature-specific
│       ├── ProductCard.jsx
│       ├── Form.jsx
│       ├── ProductGrid.jsx
│       └── ProductFilter.jsx
├── pages/
│   ├── HomePage.jsx
│   ├── ProductPage.jsx
│   └── CheckoutPage.jsx
└── App.jsx
```
#### Project Structure Summary

Keep in ONE file when:
- Components are tightly coupled (ProductCard only used in ProductGrid)
- Total file is under ~300 lines
- Components share significant state/logic
- It's a page component with its specific sub-components

Split into separate files when:
- Component is reused in 2+ places
- Component exceeds ~150 lines
- Component has complex logic worth isolating
- You're working with a team (easier git diffs)


## Core React Concepts
### JavaScript
#### JavaScript Types
```markdown
Feature    |	Primitive Types                              |	Object Types
-----------|-----------------------------------------------|-----------------------------------------------------
Data Stored| Single, simple values.                        |	Collections of key-value pairs (properties and methods).
Mutability | Immutable (cannot be changed after creation). |	Mutable (can be modified dynamically).
Passed By	 | Value (a copy of the value is used).          |	Reference (a pointer to the memory location is used).
Examples	 | string, number, boolean, null, undefined, Symbol, BigInt |	Object, Array, Function, Date, Map, Set
```
#### Variable Declarations
- `const primitiveType` Block-scoped, cannot be reassigned. Cannot be reinstantiated. Cannot change property values. Is Immutable.
- `const objectType` Block-scoped, cannot be reassigned. Cannot be reinstantiated. Properties can be added changed, or deleted. Is Mutable.
  - Running in `StrictMode` prevents constant type mutation. But still allows reassignment.
  - `Object.freeze()`	Makes the object's top-level properties read-only and prevents adding or removing properties.
  - `Object.seal()`	Prevents properties from being added or removed, but allows existing properties to be modified.
- `let` Block-scoped, can be reassigned. can be reinstantiated. Mutable.
- `var` Function-scoped, can be reassigned.Is Mutable.

#### JS Modules
JavaScript modules allow you to break your code into separate files and import/export functionality between them. This helps in organizing code and reusing components or functions across different parts of your application.

`import` statement is used to bring in functions, objects, or primitives that have been exported from another module.
```js
import * as name from "MyModule"; // Can be namespace or filepath
//Static	
import { add } from './math.js';	// At load time
//Dynamic	
const math = await import('./math.js');	// means only import this when/if needed
```
##### `export default` & `export`
prefix is a standard JavaScript syntax (not specific to React). It lets you mark the main function in a file so that you can later import it from other files.

You do not use curly braces `{}` when importing a default export.
```jsx
export default getAge;
//imported like this:
import getAge from './age.js';
// or rename it on import
import anyNameYouWant from './age.js';
// export without default requires curly braces {}
import { checkIfDateType } from './age.js';
 // age.js 
const getAge = (birthDateInput) => {
  const today = new Date(); // default value is now for constructor
  checkIfDateType(birthDateInput); // helper function to validate input
  const birthDate= new Date(birthDateInput); // convert input to Date type
  ageInMilliSec = today - birthDate; 
  ageInYears = Math.floor(
    ageInMilliSec / 1000 // convert to seconds
    / 60   // convert to minutes
    / 60   // convert to hours
    / 24  // convert to days
    / 365.25 // convert to years
  ); // Math.floor rounds down to nearest whole number, in this case year.
  return ageInYears;
}
export const checkIfDateType = (input) => {
  if (Object.prototype.toString.call(input) !== "[object Date]") {
    throw new Error("Input is not a valid Date type");
  }
}
```
#### JS Object Properties
JavaScript objects are collections of key-value pairs, where keys are strings (or Symbols) and
Object.keys() is how you get an array of an object's own enumerable property names.
```js
var user; // Create Object
user = {name: "Jane", age: 40}; // Add Properties
let myArr = Object.keys(user); // Fill Array with Object keys
```

#### obj.method() call 
You can call a method on its parent object using the dot notation.

However, if you extract the method from the object and call it separately, the `this` context inside the method will be lost, leading to unexpected behavior.

This is solved by
#### JavaScript Arrow Function (or fat arrow function)
- Arrow functions provide a concise syntax for writing functions in JavaScript. They are often used in React for defining functional components and event handlers. 
- Arrow functions do not have their own `this` context, they inherit from the **surrounding lexical scope**.
- They imply a return statement when there are no curly braces `{}` used.
- They hard code their call inside the function that calls them much like other OOP languages.

In this example the traditional function causes an error because JavaScript's `this` is undefined in that context, whereas the arrow function correctly inherits `this` from the surrounding `Timer` scope. Likewise if Timer were called from another object the arrow function would inherit that object's `this` context.

Another way of putting it:
```js
const myTV = {
  name: "TV 1",
  background: "black",
  turnRed: function() { this.background = "red"; }
}

const myTV2 = {
  name: "TV 2",
  background: "blue",
  // Note: TV2 has NO turnRed function of its own!
}

myTV2.turnOtherTVRed = () => {turnRed} //generates a new function prop for myTV2 that calls myTV's turnRed function
myTV2.turnOtherTVRed(); // this won't work because the arrow function doesn't bind to myTV2
console.log(myTV2.background); // will throw undefined at best.
console.log(myTV.background); // you might find an error or something completely unexpected here because `this` is undefined in the arrow function context
// but if I want to inherit the function as a property of a totally different object.

const myCar={ background: "white"}
myCar.turnRed = myTV.turnRed; // creates a new prop on myCar that copies the turnRed function from myTV
myCar.turnRed(); // this turns myCar red because myCar now has turnRed as its own function property
console.log(myCar.background); // is now red
// myTV in myTV.turnRed becomes the locator for the turnRed function, not the binding of the function itself.


//and why this all needed sorted out was because people would try to do something like:
element.getId("myButton").onEvent("click",turnRed); // and nothing would happen because the turnRed function wasn't being bound to anything

// Prior to ES6, you would see explicit binding like this: 
turnRed.bind(myBackground);
```


### Virtual DOM (VDOM)
Instead of editing the literal String representation of html's DOM, React creates an abstraction layer betweeen the physical DOM and what is rendered on screen called the Virtual DOM or VDOM. 
Instead of manipulating and displaying the DOM directly React updates the virtual DOM with changes, and then asynchronously updates the physical DOM.
Example of a traditional DOM that React builds its VDOM on top of:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Meta Data Title</title>
  </head>
  <body>
    <!-- The root element where React mounts the application -->
    <div id="root"></div>
    <!-- The bundled JavaScript file is loaded here -->
    <script type="module" src="/src/helloWorld.jsx"></script>
  </body>
</html>
```
### Javascript XML (JSX)
JSX is a syntax extension for JavaScript that looks similar to XML or HTML. It allows you to write HTML-like code within JavaScript, which React then transforms into JavaScript objects.
#### Example of JSX with VDOM rendering:
Use the html above as your index.html file and create a helloWorld.jsx file in the src/ directory with the following code:
```jsx
import { createRoot } from 'react-dom/client'
createRoot(document.getElementById('root')).render(
    <h1>Hello, world!</h1>
);
```
### Reusibility
Reusibility is a pattern that allows you to reuse objects instead of creating new ones every time you need them.
```jsx
// file tableOfContents.jsx
export function tableOfContents() {
    // Add this anywhere with: <TableOfContents />
  return (
    <>
      <PageLayout>
        <NavigationHeader>
          <SearchBar />
          <Link to="/docs">Docs</Link>
        </NavigationHeader>
        <Sidebar />
        <PageContent>
          <TableOfContents />
          <DocumentationText />
        </PageContent>
      </PageLayout>
    </>
  );
}
```
You can now put this table of contents component anywhere in your app:
- Use its specific file to build its look, depending on if it's in a sidebar, or in a dropdown menu, on a large screen or a mobile screen. 
- Set dynamic color changes based on themes like dark mode or light mode. 
- Add state controls to hide or show it. Populate it with API data from other parts of your application or hardcode it for static use cases. 

## Core React Framework
### Components
1. Components are functions in React.
2. The function must start with a capital letter to differentiate it from regular HTML elements.
3. Components can accept inputs, called "**props**", and return React elements that describe what should appear on the screen.
### Component Types
  #### Fragment Components
  #### Canary Fragment Components
  #### Profiler Components
  #### Suspense Components
  #### Strict Mode Components
  #### Activity Components
### Built-in components 
- `<Fragment>`, alternatively written as <>...</>, lets you group multiple JSX nodes together.
- `<Profiler>` lets you measure rendering performance of a React tree programmatically.
- `<Suspense>` lets you display a fallback while the child components are loading.
- `<StrictMode>` enables extra development-only checks that help you find bugs early.
- `<Activity>` lets you hide and restore the UI and internal state of its children.

### Fragments
Fragments let you group a list of children without adding extra nodes to the DOM. 
JSX tag `<></>`is shorthand for `<Fragment></Fragment>` in most cases.
Example usage of Fragments:
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

function Table() {
  return (
    <>
      <tr>
        <td>Column 1</td>
        <td>Column 2</td>
      </tr>
      <tr>
        <td>Column 3</td>
        <td>Column 4</td>
      </tr>
    </>
  );
}

ReactDOM.render(<Table />, document.getElementById('root'));
```

### `<Fragment>` 
Wrap elements in `<Fragment>` to group them together in situations where you need a single element. Grouping elements in Fragment has no effect on the resulting DOM; it is the same as if the elements were not grouped. The empty JSX tag <></> is shorthand for `<Fragment></Fragment>` in most cases.

#### Fragment Props 
optional key: Fragments declared with the explicit `<Fragment>` syntax may have keys.

### Canary Fragment
A **canary** feature allows you to pass a **ref** to a Fragment.
A **ref object** (e.g. from **useRef**) or **callback function**. React provides a **FragmentInstance** as the ref value that implements methods for interacting with the DOM nodes wrapped by the Fragment.
### Canary only FragmentInstance 
When you pass a ref to a fragment, React provides a FragmentInstance object with methods for interacting with the DOM nodes wrapped by the fragment:

### Canary Event handling methods:
- **addEventListener**(type, listener, options?): Adds an event listener to all first-level DOM children of the Fragment.
- **removeEventListener**(type, listener, options?): Removes an event listener from all first-level DOM children of the Fragment.
- **dispatchEvent**(event): Dispatches an event to a virtual child of the Fragment to call any added listeners and can bubble to the DOM parent.
#### Layout methods:

- **compareDocumentPosition**(otherNode): Compares the document position of the Fragment with another node.
- If the Fragment has children, the native compareDocumentPosition value is returned.
- Empty Fragments will attempt to compare positioning within the React tree and include Node.DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC.
- Elements that have a different relationship in the React tree and DOM tree due to portaling or other insertions are Node.DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC.
- **getClientRects()**: Returns a flat array of DOMRect objects representing the bounding rectangles of all children.
- **getRootNode()**: Returns the root node containing the Fragment’s parent DOM node.

#### Focus management methods:

- **focus**(options?): Focuses the first focusable DOM node in the Fragment. Focus is attempted on nested children depth-first.
- **focusLast**(options?): Focuses the last focusable DOM node in the Fragment. Focus is attempted on nested children depth-first.
- **blur**(): Removes focus if document.activeElement is within the Fragment.

#### Observer methods:
- **observeUsing**(observer): Starts observing the Fragment’s DOM children with an IntersectionObserver or ResizeObserver.
- **unobserveUsing**(observer): Stops observing the Fragment’s DOM children with the specified observer.
#### Caveats 
If you want to pass key to a Fragment, you can’t use the <>...</> syntax. You have to explicitly import Fragment from 'react' and render `<Fragment key={yourKey}>...</Fragment>`.

React does not reset state when you go from rendering `<><Child /></> to [<Child />]` or back, or when you go from rendering `<><Child /></>` to `<Child />` and back. This only works a single level deep: for example, going from `<><><Child /></></>` to `<Child />` resets the state. See the precise semantics here.

Canary only If you want to pass ref to a Fragment, you can’t use the <>...</> syntax. You have to explicitly import Fragment from 'react' and render `<Fragment ref={yourRef}>...</Fragment>`.


#### Returning multiple elements 
Use **Fragment**, or the equivalent `<>...</>` syntax, to group multiple elements together. You can use it to put multiple elements in any place where a single element can go. For example, a component can only return one element, but by using a Fragment you can group multiple elements together and then return them as a group:

### Tracking visibility with Fragment refs 
Fragment refs are useful for visibility tracking and intersection observation. This enables you to monitor when content becomes visible without requiring the child Components to expose refs:
```jsx
import { Fragment, useRef, useLayoutEffect } from 'react';

function VisibilityObserverFragment({ threshold = 0.5, onVisibilityChange, children }) {
  const fragmentRef = useRef(null);

  useLayoutEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        onVisibilityChange(entries.some(entry => entry.isIntersecting))
      },
      { threshold }
    );
    
    fragmentRef.current.observeUsing(observer);
    return () => fragmentRef.current.unobserveUsing(observer);
  }, [threshold, onVisibilityChange]);

  return (
    <Fragment ref={fragmentRef}>
      {children}
    </Fragment>
  );
}

function MyComponent() {
  const handleVisibilityChange = (isVisible) => {
    console.log('Component is', isVisible ? 'visible' : 'hidden');
  };

  return (
    <VisibilityObserverFragment onVisibilityChange={handleVisibilityChange}>
      <SomeThirdPartyComponent />
      <AnotherComponent />
    </VisibilityObserverFragment>
  );
}
```

### Suspense
`<Suspense>` lets you display a fallback while the child components are loading. This is useful for code-splitting and data-fetching scenarios where you want to show a loading indicator until the content is ready.
```jsx
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```
### Suspense Props
#### children 
The actual UI you intend to render. If children suspends while rendering, the Suspense boundary will switch to rendering fallback.
#### fallback 
An alternate UI to render in place of the actual UI if it has not finished loading. Any valid React node is accepted, though in practice, a fallback is a lightweight placeholder view, such as a loading spinner or skeleton. Suspense will automatically switch to fallback when children suspends, and back to children when the data is ready. If fallback suspends while rendering, it will activate the closest parent Suspense boundary.

### `<Activity>`
`<Activity>` lets you hide and restore the UI and internal state of its children.
```jsx
<Activity mode={visibility}>
  <Sidebar />
</Activity>
// or
<Activity isActive={isSidebarVisible}>
  <Sidebar />
</Activity>
```
### Restoring the state of hidden components 
In React, when you want to conditionally show or hide a component, you typically **mount** or **unmount** it based on that condition:
```jsx
{isShowingSidebar && (
  <Sidebar />
)}
```
But **unmounting a component destroys its internal state**, which is not always what you want.
When you **hide** a component using an **Activity boundary** instead, React will “save” its state for later:
```jsx
<Activity mode={isShowingSidebar ? "visible" : "hidden"}>
  <Sidebar />
</Activity>
```
### Example of Using `<Activity>` to Hide and Restore State
```jsx
// Sidebar.jsx
import { useState } from 'react';

export default function Sidebar() {
  const [isExpanded, setIsExpanded] = useState(false)
  
  return (
    <nav>
      <button onClick={() => setIsExpanded(!isExpanded)}>
        Overview
        <span className={`indicator ${isExpanded ? 'down' : 'right'}`}>
          &#9650;
        </span>
      </button>

      {isExpanded && (
        <ul>
          <li>Section 1</li>
          <li>Section 2</li>
          <li>Section 3</li>
        </ul>
      )}
    </nav>
  );
}
```
```jsx
// App.jsx
import { Activity, useState } from 'react';

import Sidebar from './Sidebar.js';

export default function App() {
  const [isShowingSidebar, setIsShowingSidebar] = useState(true);

  return (
    <>
      <Activity mode={isShowingSidebar ? 'visible' : 'hidden'}>
        <Sidebar />
      </Activity>

      <main>
        <button onClick={() => setIsShowingSidebar(!isShowingSidebar)}>
          Toggle sidebar
        </button>
        <h1>Main content</h1>
      </main>
    </>
  );
}
```
#### Pre-rendering content with `<Activity>`
```jsx
<Activity mode="hidden">
  <SlowComponent />
</Activity>
```

### Activity Props

### Activity State




### Activity APIs
  #### Client APIs
  #### Server APIs
  #### Static APIs


---

## Props
[Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component)
Props (short for "properties") are a way to pass data from a parent component to a child component in React. They are read-only and should not be modified by the child component. Example usage of props:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render( Welcome(element), document.getElementById('root'));
```
### Passing Props to a Component
React components use props to communicate with each other. 

Every parent component can pass some information to its child components by giving them props.

The child component does not need to have defaults or know what props it will receive; it simply uses whatever props the parent gives it. Parent components can pass:
- `objects`
  - Note key is used by React for lists; not accessible as `props.key`
- `arrays`
- `functions`
- `primitives` (strings, numbers, booleans, etc.)
- `components` (React elements or other components)
- `references` (refs created with `React.createRef()` or `useRef()`)
  - Note only available through `forwardRef` or `canary fragments`
- `children` (the content between the opening and closing tags of a component)
- `Render props` (functions that return React elements)

### 3 Ways to Pass Props
#### Hardcoding a variable inside the component definition
This is the simplest way to use props, and ensures the props are always the same.
```jsx
const MyComponent = () => {
  let greeting = "Hello, World!"; // you cannot change greeting from outside the component.
  return (
    <h1>{greeting}</h1>
  );
};
```
#### Passing props from a larger scope
Each time the component is rendered, it uses the value of the variable from the lexical scope.
```jsx
let greeting = "Hello, World!";
const MyComponent = () => (
    <h1>{greeting}</h1> // you can now change greeting from outside the component.
  );
```
#### Passing props from a parent component
This is the most flexible way to use props, as the parent component can pass different values each time it renders the child component.
```jsx
//props is passed in as a parameter, if you pass nothing react always passes an empty object, so to use default values you have to destructure it with a default empty object.
const MyComponent = (
  props = {
    greeting: "Default Value for Greeting!",
    ...otherProps
  } = {} // destructure with default empty object
  ) => (
    <h1>{props.greeting}</h1> // you can now change greeting from outside the component.
  );
```

#### children
Not “reserved” in the same way as `key`/`ref`, but it’s special-cased by JSX syntax.
- Anything between the tags becomes `props.children`.
- Special DOM props (only for built-in elements like <div>, <input>)
#### key
Used by React to track items in a list for reconciliation.
- Not available inside the component (`props.key` is `undefined`).
- Only meaningful when **rendering arrays**.
```jsx
items.map(item => <Row key={item.id} item={item} />)
```

### ref
Used to get a reference to a DOM node or component handle.
- Not available as a normal prop unless you use `forwardRef`.
- For function components, you need `React.forwardRef` to accept it.
```jsx
const Button = React.forwardRef((props, ref) => <button ref={ref} />)
```
#### References (refs)
Refs are a way to access DOM nodes or React elements created in the render method, this called **imperative access**.

Created with `React.createRef()` or `useRef()`.

`refs` differ from `state` in that changing a `ref` does not cause a **re-render**.

They can be used for:
- a `DOM element` (most common)
- a `mutable value` you want to persist **without re-rendering** between renders (useRef)
- an `imperative handle` exposed by a component (useImperativeHandle)
- focus/scroll/measure
- integration with non-React APIs
- performance patterns (store values without re-render)
- Other common uses:
  - manage focus 
  - text selection
  - media playback
  - trigger imperative animations
  - integrate with third-party DOM libraries
```jsx
{/* Before mount: inputRef.current === null
    After mount: inputRef.current points to the <input> DOM node 
*/}
import { useRef } from 'react';
function Example() {
  const inputRef = useRef(null);
  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current?.focus()}>
        Focus the input
      </button>
    </>
  );
}
```
#### ref rules
- Do **NOT** use `refs` in function components without `forwardRef`.
- Do **NOT** modify `refs` during rendering.
- `refs` are for **imperative access** to DOM nodes or component instances, not for data flow.
- `refs` only point to one value at a time, so avoid assigning them to multiple `elements`.
- Do **NOT** use `refs` to read `state` or `props` for rendering. Use `state`/`props` instead.
- Do **NOT** mutate DOM that React owns (except for safe operations)
- Safe:
  - `focus()`, `scrollIntoView()`, `reading sizes`
- Risky:
  - setting `innerHTML`, manually changing `styles`/`classes` that React also controls



#### imperative access



### HTML Attribute Props
React supports all standard HTML attributes as props on built-in components. Some have special names or behaviors
#### className / htmlFor

- React uses `className` instead of `class`.


#### `style`
Used to apply inline styles to an element.
- Must be an object, not a string.
```jsx
<div style={{ marginTop: 8, backgroundColor: 'black' }} />
```

#### `htmlFor`
- React uses `htmlFor` instead of `for` (because `for` is a JS keyword).
- used on a `<label>` to associate it with a `form control` by that control’s `id`
```jsx
<label htmlFor="email">Email</label>
<input id="email" name="email" type="email" />
```

#### `dangerouslySetInnerHTML`
Used to inject raw HTML.

Value must be an object: `{ __html: "..." }`.
```jsx
const htmlString = "<p>This is raw HTML</p>";
<div dangerouslySetInnerHTML={{ __html: htmlString }} />
```

#### Controlled vs uncontrolled form props
React treats these specially on **form elements**:
- `value` / `checked` (controlled)
- `defaultValue` / `defaultChecked` (uncontrolled)
- `onChange` ties into controlled updates
```jsx
<form>
<input value={state} onChange={e => setState(e.target.value)} />
<input defaultValue="x" />
</form>
```
### Event handlers

Props like `onClick`, `onChange`, `onSubmit`, etc. are wired to React’s event system.

<button onClick={handleClick} />

suppressHydrationWarning (SSR/hydration)

Used when server-rendered HTML might not match client on first render.

<span suppressHydrationWarning>{time}</span>

Two important rules for “extra props”

Custom components can receive any prop name (nothing is reserved except key/ref behavior). If you don’t read it, it’s ignored.

If you spread props onto a DOM element, unknown attributes may be dropped or warn. Use data-* for custom attributes.

<button data-test="save" aria-label="Save" />

-------------------------------------------------------------------------------------------------------
## State
State is a built-in object that allows components to create and manage their own data. Unlike props, state is mutable and can be changed over time, usually in response to user actions or other events.

### [State Rules](#State-Rules)
- State is isolated and private (Basically its scoped to the page or component that uses it.)
- You can NOT use state during effects or event handlers.
- You can ONLY use state at the top level of your React function.
- You can ONLY use state in React functions.
- Hooks require a stable call order on every render.

#### State Good Practices
[Choosing the State Structure](https://react.dev/learn/choosing-the-state-structure)
It is a good idea to have multiple state variables if their state is unrelated, like index and showMore in this example. But if you find that you often change two state variables together, it might be easier to combine them into one. For example, if you have a form with many fields, it’s more convenient to have a single state variable that holds an object than state variable per field.

### Stable Call Order - State is just an array under the hood
[State is just an incrementing array](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e)

**Hooks** rely on a **stable call order** on every **render** of the **same component**. This is why you can only call Hooks at the top level of your React function and not inside loops, conditions, or nested functions. If you violate this rule, the order of Hook calls will change on every render, and React will not be able to associate state variables with their respective Hook calls.

There is no “identifier” that is passed to `useState` to distinguish between different `state variables`. Instead, React relies on the order in which `useState` calls are made. On each render, React keeps track of the **order of Hook calls** and associates each state variable with its corresponding `useState` call based on that order.

Internally, React holds an array of state pairs for every component. It also maintains the current pair index, which is set to 0 before rendering. Each time you call `useState`, React gives you the next state pair and increments the index.

***Initial value tells react, "hey we're at 0 on this value, when we get to the next useState call, increment to 1 and bind that second value(can be an object, list, etc) to array index 1"***
```jsx
[valueToUpdate, changeValueFunction()] = useState(initialValue); // also an example of destructuring assignment
```

### State Variables
[React Dev State Variables](https://react.dev/learn/state-a-components-memory)
- Use a state variable when a component needs to “remember” some information between renders.
- State variables are declared by calling the **useState Hook**.
- **Top Level** 
  - Means in the body of the function component, not inside loops, conditions, or nested functions.
  - No curly braces `{}` for top level parts except the ones that wrap the function aka code block.
  - Another way to think of **top level** is **outermost scope of the code block** aka **not nested**.
### Setting and Getting State with Hooks
Go to Hooks for specifics: [Hooks: State Hooks](#State-Hooks)

### useState Hook
[useState Hook React Docs](https://react.dev/reference/react/useState)
The `useState` Hook is a special function that allows you to add state to functional components. It returns an array with two elements: the current state value and a function to update that value.
```jsx
import React, { useState } from 'react';
import ReactDOM from 'react-dom';
function Counter() {
  // [valueToUpdate, changeValueFunction] = useState(initialValue); // also an example of destructuring assignment
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
ReactDOM.render(<Counter />, document.getElementById('root'));
```



## Render
Rendering is an official process of the React Framework. This is when React changes the virtual DOM, which tells the browser to update the pixels on the screen.

It only happens when ***all the event handlers have run and have called their [set functions](#setstate)***

### ReactDOM.render()
The `ReactDOM.render()` method is used to render a React element into the DOM. It takes two arguments: the React element to render and the DOM node where you want to mount the element.
```jsx

```

### Batching State Changes
React batches state updates. 

It updates the screen after ***all the event handlers have run and have called their set functions***. This prevents multiple re-renders during a single event. In the rare case that you need to force React to update the screen earlier, for example to access the DOM, you can use [`flushSync`](https://react.dev/reference/react-dom/flushSync).
-----------------------------------------------------------------------------------------------------------------


-------------------------------------------------------------------------------------------------------------------
## Events
Handling events in React is similar to handling events in regular HTML, but with some syntactic differences. In React, event names are written in camelCase, and you pass a function as the event handler instead of a string. Example usage of event handling:
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
function handleClick() {
  alert('Button was clicked!');
}
<button onClick={handleClick}>Click me</button>
```
### Wrapping Actions in Functions
In React, when you want to pass arguments to an event handler function, you need to wrap the function call in another function. This is because if you call the function directly, it will execute immediately instead of when the event occurs. Example:
```jsx
// 1. A generic function that takes ANY element and turns it red
const turnAnythingRed = (elementToPaint) => {
   elementToPaint.style.backgroundColor = 'red';
}

const myContainer = document.getElementById('main-container');
const myHeader = document.getElementById('main-header');

document.getElementById('btn-a').addEventListener('click', () => {
    turnAnythingRed(myContainer);
});
```

### Using Fragment refs for DOM interaction 
Fragment refs allow you to interact with the DOM nodes wrapped by a Fragment without adding extra wrapper elements. This is useful for event handling, visibility tracking, focus management, and replacing deprecated patterns like ReactDOM.findDOMNode().
```jsx
import { Fragment } from 'react';

function ClickableFragment({ children, onClick }) {
  return (
    <Fragment ref={fragmentInstance => {
      fragmentInstance.addEventListener('click', handleClick);
      return () => fragmentInstance.removeEventListener('click', handleClick);
    }}>
      {children}
    </Fragment>
  );
}
```
## Context
[React Context API Reference](https://react.dev/reference/react/context)
Context provides a way to pass data through the component tree without having to pass props down manually at every level. It is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.
### Do's of Context
- **Do** use Context to share data that is considered global for a tree of React components.
- **Do** create a separate Context for each type of data you want to share.
- **Do** use the `useContext` Hook to access Context values in function components.
- **Do** use context as a unified way to show themes, locales, or user authentication status across your app.
- **Do** wrap your component tree with the Context Provider to make the Context values available to child components.

### Don'ts of Context
- **Don't** use Context to pass data that changes frequently, as it can lead to performance issues.
- **Don't** use Context for screen resizing or other high-frequency updates; use state or props instead.
- **Don't** overuse Context; it can make your component tree harder to understand and maintain.
- **Don't** use Context as a replacement for props in all situations; props are still the preferred way to pass data between components when possible.
- **Don't** mutate Context values directly; always use the provided methods to update them.
- **Don't** forget to provide a default value when creating a Context, as it will be used when a component does not have a matching Provider above it in the tree.
- **Don't** use Context in class components; it is designed to work with function components and Hooks.
- **Don't** use Context for local component state; use `useState` or `useReducer` instead.
- **Don't** forget to wrap your component tree with the Context Provider to make the Context values available to child components.

```jsx
import { createContext, useContext, useState } from 'react';
```

---------------------------------------------------------------------------------------------------------------------
## Hooks
[React Hooks API Reference](https://react.dev/reference/react/hooks)

Hooks are special functions that let you "hook into" React features. They allow you to use state and other React features without writing a class. Hooks are defined using JavaScript functions, but they represent a special type of reusable UI logic with restrictions on where they can be called.
#### Good Examples of Hooks Usage
```jsx
function Counter() {
  // Good: top-level in a function component
  const [count, setCount] = useState(0);
  // ...
}

function useWindowWidth() {
  // Good: top-level in a custom Hook
  const [width, setWidth] = useState(window.innerWidth);
  // ...
}
```

### Rules of Hooks
### Do's of Hooks
- Hooks are **functions** whose names start with ***use*** in React. 
- You can **only call Hooks** while React is rendering a function component or from within another custom Hook.
- **Only** call Hooks from **React functions**. 
- Only call Hooks at the top level of your React function.
- Hooks require a stable call order on every render.
### Do Not's of Hooks
- Do ***NOT*** pass Hooks as **arguments** to other functions.
- Do ***NOT*** call Hooks **inside conditions or loops**.
- Do ***NOT*** call Hooks **after a conditional return statement**.
- Do ***NOT*** call Hooks in **event handlers**.
- Do ***NOT*** call Hooks in **class components**.
- Do ***NOT*** call Hooks **inside functions passed to useMemo, useReducer, or useEffect**.
- Do ***NOT*** call Hooks inside **try/catch/finally** blocks.
- Do ***NOT*** call Hooks in **regular JavaScript functions**.

### List & Links of React Hooks
- [useActionState](https://react.dev/reference/react/useActionState)
- [useCallback](https://react.dev/reference/react/useCallback)
- [useContext](https://react.dev/reference/react/useContext)
- [useDebugValue](https://react.dev/reference/react/useDebugValue)
- [useDeferredValue](https://react.dev/reference/react/useDeferredValue)
- [useEffect](https://react.dev/reference/react/useEffect)
- [useEffectEvent](https://react.dev/reference/react/useEffectEvent)
- [useId](https://react.dev/reference/react/useId)
- [useImperativeHandle](https://react.dev/reference/react/useImperativeHandle)
- [useInsertionEffect](https://react.dev/reference/react/useInsertionEffect)
- [useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)
- [useMemo](https://react.dev/reference/react/useMemo)
- [useOptimistic](https://react.dev/reference/react/useOptimistic)
- [useReducer](https://react.dev/reference/react/useReducer)
- [useRef](https://react.dev/reference/react/useRef)
- [useState](https://react.dev/reference/react/useState)
- [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore)
- [useTransition](https://react.dev/reference/react/useTransition)

## State Hooks
State lets a component “remember” information like user input. For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.

### useState
[useState](https://react.dev/reference/react/useState) 
Also see [useState Hook](#usestate-hook)
```jsx
const [state, setState] = useState(initialState)
```
A **state control Hook** that lets you add `React state`(an array bound to your variable) to function components. 
```jsx
import { useState } from 'react';

function MyComponent() {
  const [age, setAge] = useState(28);
  const [name, setName] = useState('Taylor');
  const [todos, setTodos] = useState(() => createTodos());
  ...function continued...
```
### initialState 
The object or value that you're going to keep "stateful" and its initial value. In the above it is `age`, `name`, and `todos`.
### [set functions aka setState functions](#set-state-functions)
The function that lets you update the state variable. In the above it is `setAge`, `setName`, and `setTodos`. 
- **`set functions` do** ***NOT*** **have a `return value`.**
- The `set function` **only** updates the `state variable` for the next **render** cycle.
- Calling the `set function` triggers a re-render of the component with the new state value.
  - If you read the state variable after calling the set function, you will still get the old value that was on the screen before your call
  - You have to wait for the **next render cycle** to handle state variables.
  - You'll only see the new value on the ***NEXT RENDER*** **cycle**.
  - It preloads the new value for the **next render cycle**.
- If the new value you provide is identical to the **current state**, as determined by an **[Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)** comparison, React will **skip** re-rendering the component and its children.


## Effect Hooks



### useEffect
[useEffect Hook React Docs](https://react.dev/reference/react/useEffect)
`useEffect` is a Hook that lets you perform side effects in function components.

Typically for syncing with external systems like APIs, timers, logging, and manually manipulating the DOM.

`useEffect` takes two parameters:
#### `setup` 
The function with your Effect’s logic. 
  - Your `setup` function may also optionally return a `cleanup` function. When your component commits, React will run your `setup` function. 
  - After every commit with changed `dependencies`, React will first run the `cleanup` function (if you provided it) with the old values, and then run your `setup` function with the new values. 
  - After your component is removed from the DOM, React will run your `cleanup` function.
#### `dependencies`: **An Optional Parameter** : 
Is the list of all `reactive values` referenced inside of the setup code. 

[Dependencies Explained](https://react.dev/reference/react/useEffect#examples-dependencies)

`Reactive values` referenced inside the `setup function` include props, state, and all the variables and functions declared directly inside your component body. 

If your linter is configured for React, it will verify that every `reactive value` is correctly specified as a `dependency`. 

The list of `dependencies` ***MUST HAVE***
- A **constant number of items** 
- And be **written inline** like [dep1, dep2, dep3]. 
 
React will compare each `dependency` with its previous value using the `Object.is` comparison. 

**If you omit this argument**, your **Effect will re-run after every commit of the component**. 

See the difference between passing 
- an array of dependencies 
- an empty array
- no dependencies at all

#### Example of useEffect with dependencies
```jsx
import { useState, useEffect } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
  	const connection = createConnection(serverUrl, roomId);
    connection.connect();
  	return () => {
      connection.disconnect(); 
  	};
  }, [serverUrl, roomId]);
  // ...
}
```

#### Example of useEffect with empty dependency array
```jsx

```

#### Example of useEffect with no dependency array
```jsx

```

### useEffectEvent
[useEffectEvent Hook React Docs](https://react.dev/reference/react/useEffectEvent)




### Layout Effect Hook
[useLayoutEffect Hook React Docs](https://react.dev/reference/react/useLayoutEffect)
The `useLayoutEffect` Hook is similar to `useEffect`, but it fires synchronously after all DOM mutations. Use this to read layout from the DOM and synchronously re-render. Updates scheduled inside `useLayoutEffect` will be flushed synchronously, before the browser has a chance to paint.
```jsx
import React, { useLayoutEffect, useRef, useState } from 'react';
function LayoutEffectExample() {
  const [width, setWidth] = useState(0);
  const divRef = useRef(null);

  useLayoutEffect(() => {
    // Read layout from the DOM
    if (divRef.current) {
      setWidth(divRef.current.offsetWidth);
    }
  }, []); // Empty dependency array means this effect runs once after mount

  return (
    <div ref={divRef} style={{ width: '50%' }}>
      <p>The width of this div is: {width}px</p>
    </div>
  );
}
```

### [useReducer](https://react.dev/reference/react/useReducer)
is a Hook that lets you manage more complex state logic in function components.

### Context Hooks
Context lets a component receive information from distant parents without passing it as props. For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

    `useContext` reads and subscribes to a context.


### Dependency Array
The dependency array is the second argument to the `useEffect` Hook. It is an array
```jsx
useEffect(() => { ... }, []); // Runs once after the initial render (component mounts).
useEffect(() => { ... }, [dep1, dep2])// Runs after the first render, and then only when dep1 or dep2 change between renders.
```
### [Removing Effect Dependencies](https://react.dev/learn/removing-effect-dependencies#move-dynamic-objects-and-functions-inside-your-effect)


####
#### Ref Hooks
#### Performance Hooks
#### Custom Hooks
#### Other Hooks & Form Hooks

```jsx
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

ReactDOM.render(<Example />, document.getElementById('root'));
```




```shell
########################################################################################################
```
## Usage Examples

### Hooks
```jsx
import { useBreakpoint, useForm, useDebounce } from './hooks';

function MyComponent() {
  const breakpoint = useBreakpoint();
  const { values, handleChange, handleSubmit } = useForm({
    initialValues: { name: '' },
    onSubmit: (values) => console.log(values)
  });
  
  return breakpoint.isMd ? <DesktopView /> : <MobileView />;
}
```

### Utilities
```jsx
import { cn, clamp, toTitleCase, ApiError } from './utils';

// Combine classes
const classes = cn('btn', isActive && 'active');

// Number clamping
const value = clamp(50, 0, 100); // 50

// String formatting
const title = toTitleCase('hello_world'); // 'Hello World'

// Custom errors
throw new ApiError('Request failed', { status: 404 });
```

### API Client
```jsx
import { api, createApiClient } from './api';

// Use global client
const data = await api.get('/endpoint');

// Or create custom client
const client = createApiClient({
  baseUrl: 'https://api.example.com',
  getAuthToken: () => localStorage.getItem('token')
});
```

### Components
```jsx
import {
  Button, Input, Modal, Card, CardBody, DataTable,
  PageLayout, NavBar, Container
} from './components';
import { useBreakpoint, useForm } from './hooks';

function App() {
  const [open, setOpen] = useState(false);
  const form = useForm({ initialValues: {} });

  return (
    <PageLayout
      nav={<NavBar brand="MyApp" />}
      children={
        <Card>
          <CardBody>
            <Button onClick={() => setOpen(true)}>Open Modal</Button>
            <Modal open={open} onClose={() => setOpen(false)}>
              Modal content
            </Modal>
          </CardBody>
        </Card>
      }
    />
  );
}
```

## Key Features

- **Modular**: Each component/hook/utility is in its own file
- **Tree-shakeable**: Only import what you need
- **TypeScript-ready**: Easy to add type definitions
- **Responsive**: Built-in breakpoint detection
- **Accessible**: ARIA attributes where appropriate
- **Customizable**: Inline styles and className support
- **Lightweight**: No external dependencies (uses React only)

## Import Patterns

### Individual imports
  ```jsx
  import { Button } from './components/OpenAiPrimitives/Button';
  import { useForm } from './hooks/OpenAiHooks/useForm';
  ```

### Grouped imports
```jsx
import * as Components from './components';
import * as Hooks from './hooks';
import * as Layouts from './layouts';
```

### Barrel imports
```jsx
import { Button, Input, Modal } from './components';
import { useBreakpoint, useForm } from './hooks';
```
