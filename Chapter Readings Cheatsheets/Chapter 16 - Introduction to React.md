# Introduction to React
- React is “a JavaScript library for building user interfaces” developed by Facebook.
- React allows you to dynamically generate and interact with the DOM, similar to what you might do with jQuery and using the DOM API.
- React was created to make it much easier to define and manipulate lots of different parts of the DOM, and to do so quickly.
- You declare a web app in terms of different components (think: “things” on a web page) that can be independently managed—this lets you design and implement web apps at a higher level of abstraction.
- Components are usually associated with some set of data, and React will automatically “re-render” (show) the updated component when the data changes.
- React is currently the most popular “framework” for building large-scale web applications (its chief competitors being Angular and Vue.js).
    - This means that React is generally very well documented.

## Getting Set Up: Create React App
- React makes use of a significant amount of advanced and custom JavaScript syntax (described below), including extensive use of ES6 Modules. Thus in practice, using developing React apps requires using a large number of different development tools.
- Facebook does provide an amazing application which combines many of these these different development tools together.
- Create React App (CRA) is a command line application that generates scaffolding (“starter code”) for a React application, as well as provides built-in scripts to run, test, and deploy your code.
- You can use Create React App to create a new React app by running the program and specifying a name for the folder you want the app to be created inside of.
- Below command will create a new folder called my-app that contains all of the code and tools necessary to create a React app:
```bash
# Create a new React app project in a new `my-app` directory
# This may take a minute...
npx create-react-app my-app --use-npm

# Change into new project directory to run further commands
cd my-app
```
- The npx command is installed alongside npm 5.2.0 and later, and can be used to (temporarily) install and run a global command in a single step. So rather than needing to use npm install -g create-react-app, you can just use npx.
