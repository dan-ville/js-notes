[[Index]]

# React

[React](https://reactjs.org/) is a JavaScript library for building user interfaces.

In addition to being knowledgeable on the JavaScript fundamentals, including how to work with data structures and [[Object Oriented Programming]], it's recommended to know a few topics in ES6+ before learning React. Primarily, you should know:
- destructuring arrays and objects
- higher order functions and methods like map, filter, and reduce
- arrow functions
- Fetch API and Promises, and
- Classes

It would be difficult to learn React and these other concepts simultaneously because it may be unclear which parts of the library come from React vs which come from plain JavaScript.

To start using React, you need to add the React and ReactDOM packages to your project. Check out the website to add [React to a project](https://reactjs.org/docs/getting-started.html).

## Components
The most fundamental building block of React is the *component*. With React, we aim to break our application into reusable, self-contained components. They make up our user interface a handle our data, and by creating multiple components and combining them we can get complex applications. 

Components are created using JavaScript, HTML and CSS together, and we separate concerns based on the purpose of each component. 

There are currently two types of components: class and function. Historically, class components were dominant because function components didn't have access to all the features. With the introduction of React Hooks, function components are the defacto component for writing React code. 

We're going to proceed learning with Functional components and Hooks.

A functional component is basically just a function that returns something and renders it into the DOM.

React uses its own version of the DOM and updates the real DOM when changes are made. To render anything to the DOM, we need to use `ReactDOM.render()`.

This will take two parameters; 1) the thing to be rendered, and (2) the element to render it in. Regarding (2), Developers commonly render into a div element with the id of `root`. In your HTML file, make that div now. 

Let's now get into (1), the things to be rendered.

### JSX
React combines HTML with JavaScript functionality to create its own markup language, JSX, which is just a syntax extension of JavaScript--meaning you can extend the "valid" syntax and allow JavaScript to be written directly in the HTML. More accurately, you write JavaScript in the JSX.

But since it's not true JavaScript, it has to be compiled into JavaScript. Babel is a transpiler that can achieve this. You can add Babel to a project using npm or yarn. 

Create a JSX element:
```js
const JSX = <h1>Hello, world!</h1>
ReactDOM.render(JSX, document.getElementByID('root'))
```

That's a simple JSX element that gets rendered into the DOM. You can create more complex elements by nesting elements. However, there must be only *one* element returned. For example, if you want to render a list of 3 paragraph elements, you need to nest them in a parent div first, and then return that parent div. This is a common workflow--nesting elements within a parent wrapper element.

Tip:  add comments in JSX using the syntax `{*/ comment here /*}`

### Stateless Functional Component
Let's get back to components.

There are two ways to create a React component. The first is to use a JavaScript function. Defining a component in this way creates a stateless functional component. For now, think of a stateless component as one that can receive data and render it, but not manage or track it.

To create a component with a function, you simply write a JavaScript function that returns either JSX or `null`.

Here's an example of a stateless functional component that assigns an HTML class in JSX:
```js
// After being transpiled, the <div> will have a CSS class of 'customClass'
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

### Class Components
The other way to define a React component is with the ES6 `class` syntax.

In the following example, Kitten "extends" React.Component:
```js
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

This creates an ES6 class Kitten which "extends "the React.Component class, meaning it gives the Kitten class access to many useful React features, such as local state and lifecycle hooks, much like JSX "extends" the HTML syntax to include JavaScript. Don't worry if you aren't familiar with these terms yet. Also notice the Kitten class has a constructor defined within it that calls `super()`. It uses `super()` to call the constructor of the parent class, in this case `React.Component`. The constructor is a special method used during the initialization of objects that are created with the class keyword. It is best practice to call a component's constructor with super, and pass props to both. This makes sure the component is initialized properly. For now, know that it is standard for this code to be included when creating a class component. Soon you will see other uses for the constructor as well as props.

### Rendering React Components
To render JSX Elements to the DOM, we used `ReactDOM.render(JSX, document.getElementById('root'))`. To render React components rather than just JSX elements, the syntax is only a little different. You still need to use `render()` and pass in two parameters (the component to render and the target node), but you need to put the component inside `< />`. You use this syntax for both ES6 class components and functional components.

To recap, a React Class component is an ES6 class that extends `React.Component`. The constructor calls  `super()`, and props is passed as an argument to both `constructor` and `super`. Then, the component has a `render` property with a return statement, which returns JSX or null. You can also nest components into the return statement. Note: the return statement uses `()` not `{}`. Then, you can render the component with `ReactDOM.render(componentToRender, targetNode)`.

### Props
`props` is a very common feature in React; you can pass `props`, or properties, to child components.?/