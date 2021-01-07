[[Index]]

# React Crash Course
[Youtube video](https://www.youtube.com/watch?v=sBws8MSXN7A&t=1035s)

## Setting up a new project
Create a directory for your React project.

In the terminal, navigate to that directory and then use the command  `npx create-react-app` to create the framework of files in your project folder. This will install the framework only in the folder and not globally on your machine.

In your *package.json* file, there should be several dependencies; **react**, **react-dom**, and **react-scripts**.

There should also be a directory called "public" in your project folder. It should have an *index.html* file. React is a single-page framework, meaning that your entire app should working off of a single page, vis-a-vis this index.html page. The index.html page will have a div element with an id of root, and the entire app will actually be getting rendered from within this element.

The key to the rendering is in the index.js file of the *src* directory. It may change in future versions of React, but for the most part the concept is simple. Your javascript file, index.js, is connected to the index.html page. Using javascript, you render all of your React components, the elements of your page, into the index.html via the *root* div. It should typically look like this:

```js
ReactDOM.render(<App />, document.getElementById('root'));
```

In other words, that one line will render the *App* component into the *root* div, and that is how your web app works. Of course, you will have to build a bunch of other components and that will go inside the main App component. But that's basically how React works!

## the App component
Every component in React will have a `render()` function which *returns* JSX elements. JSX looks like HTML but it's actually an extension of JavaScript that allows you to write elements that look like HTML in a JavaScript file. By having the render() function return a ton of JSX elements, we can create the structure of our web app. That's how you do it in React.

The App component will normally be found in the *src* folder in the App.js file, and it will typically be a *class* extending the React *Component*, and then it will be exported so that other files (like index.js) can access the App component.

Thus, you will see these lines of code in the App.js file:
```js
import React, {Component} from 'react';

class App extends Component {
	render() {
		return (
		<div id="header">JSX Header element</div>
		)
	}
}

export default App;
```

Sometimes, the syntax might look a little different, but it works the same way:
```js
// in the previous method, the import statement directly imports the Component object
import React from 'react';

class App extends React.Component {...} // etc
```