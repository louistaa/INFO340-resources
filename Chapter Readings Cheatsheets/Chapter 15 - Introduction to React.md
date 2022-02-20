# Chapter 15: Introduction to React
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

> If you specify the current directory (.) as the target folder name, Create React App will create a new react app in the current folder! This is useful when you want to create a React app inside an existing cloned GitHub repository.
- The --use-npm argument is optional, but will make sure that your app uses npm to manage packages and not an alternate manager (like yarn).

## Running the Development Server
- After you create a React app, you can use one of CRA’s provides scripts (the start script) to automatically start up a development webserver:

```bash
# Make sure you are in the project directory
cd path/to/project

# Run the development server script
npm start
```
- This will launch the webserver, and open up a new browser window showing the rendered web page! This development webserver will automatically perform the following whenever you change the source code:
1. It will transpile React code into pure JavaScript that can be run in the web browser.
2. It will combine (bundle) all of the different code modules into a single file, and automatically inject that single file into the HTML (adding the ```<script>``` tag for you).
3. It will display errors and warnings in your browser window.
4. It will automatically reload the page—whenever you change the source code.

- All these capabilities are provided by a tool called [webpack](https://webpack.js.org/).

> In order to stop the server, hit ctrl-c on the command line.

## Project Structure
A newly created React app will contain a number of different files:
1. The ```public/index.html``` file is the home page for your application when webpack builds the app. If you look at this file, you’ll notice that it doesn’t include any CSS ```<link>``` or JavaScript ```<script>``` elements—the CSS and JavaScript for your React app will be automatically injected into the HTML file when the app is built and run through the development server. The CSS and JavaScript files will be found in the src/folder. Thus, you rarely modify the index.html file (beyond changing the ```<title>``` and favicon and such).
- The src/ folder contains the source code for your React app.
-  Notice that the CSS files are imported from inside the JavaScript files (with e.g., import './index.css'). This is because the webpack build system that Create React App uses to run apps knows how to load CSS files, so you can “include” them through the JavaScript rather than needing to link them in the HTML.
- If you want to load an external stylesheet, such as Bootstrap or Font-Awesome, you can still do that by modifying the public/index.html file—but it’s better to instal them as modules and import them through the JavaScript.

## JSX
- Notice that the class attribute is specified with the className property. This is because class is a reserved keyword in JavaScript.
- React lets you create and define elements using JSX. JSX is a syntax extension to JavaScript: it provide a new way of writing the language—in particular, the ability to write bare HTML tags in JavaScript:
```js
//JSX can define nested elements
let header = (
    <header className="well">
        <h1>Hello world!</h1>
    </header>
);
```
- It’s very common to put elements on their own lines, intended as if you were writing HTML directly.
- You’ll need to surround the entire JSX expression in parentheses ().
- Notice that there is still a semicolon (;) at the end of the first line; you’re not actually writing HTML, but defining a JavaScript value using syntax that mostly looks like HTML!

> Since JSX is not actually valid JavaScript (you can’t normally include bare HTML), you need to “translate” it into real JavaScript so that the browser can understand and execute it. This process is called transpiling, and is usually performed using a compiler program called Babel. Babel is yet another piece of the toolchain used to create React applications; however, all the details about transpiling with Babel are automatically handled by the Create React App scaffolding.

## Inline Expressions
- JSX allows you to include JavaScript expressions (such as variables you want to reference) directly inside of the HTML-like syntax. You do this by putting the expression inside of curly braces ({}):

```js
let message = "Hello world!";
let element = <h1>{message}</h1>;
```
- When the element is rendered, the expression and the surrounding braces will be replaced by the value of the expression. So the above JSX would be rendered as the HTML: ```<h1>Hello World</h1>```.
- You can put any arbitrary expression inside of the {}—that is, any JavaScript code that resolves to a single value. This can include math operations, function calls, etc.

```js
//Including an inline expression in JSX. The expressions can be mixed directly 
//into the HTML
let element = <p>A leap year has {(365 + 1) * 24 * 60} minutes!</p>;
```
- If you include an array of React elements in an inline expression:
```js
//An array of React elements. Could also produce via a loop or function
let listItems = [<li>lions</li>, <li>tigers</li>, <li>bears</li>];

//Include the array as an inline expression; each `<li>` element will be 
//included as a child of the `<ul>`
let list = <ul>{listItems}</ul>;
```
- This is particularly useful when using a variable number of elements, or generating elements directly from data.
- Comments in JSX:
```js
let main = (
    <main>
      { /* A comment: the main part of the page goes here... */ }
    </main>    
)
```
## React Components
- When creating React applications, you use JSX to define the HTML content of your webpage directly in the JavaScript. However, writing all of the HTML out as one giant JSX expression doesn’t provide much advantage over just putting that content in .html files in the first place.
- Instead, the React library encourages and enables you to describe your web page in terms of components, instead of just HTML elements. In this context, a component is a “piece” of a web page.
- React components are most commonly defined using function components: JavaScript functions that return the DOM elements (the JSX) that will be rendered on the screen:

```js
//Define a component representing information about a user
function UserInfo(props) {
    //This is an everyday function; you can include any code you want here
    let name = "Ethel";
    let descriptor = "Aardvark";

    //Return a React element (JSX) that is how the component will appear
    return (
        <div>
            <h1>{name}</h1>
            <p>Hello, my name is {name} and I am a {descriptor}</p>
        </div>
    )        
}

//Create a new value (a React element)
//This syntax in effect "calls" the function
let infoElement = <UserInfo />;

//Show the element in the web page (inside #root)
ReactDOM.render(infoElement, document.getElementById('root'));
```
- This function defines a new component (think: a new HTML element!) called UserInfo. Things to note about defining this component:
1. A component function must be named starting with a Capital letter (and usually in CamelCase). This is to distinguish a custom component from a “normal” React element.
    - If you see a function with a Capitalized name, know that it’s actually a defining a Component!
2. Component functions take in a single argument representing the props (discussed below), which is conventionally named as such. As with all JavaScript functions, if you don’t to use the argument value you can omit giving it a name.
3. A component function is a regular function like any other that you’ve written. That means that it can and often does do more than just return a single value! You can include additional code statements (variable declarations, if statements, loops, etc) in order to calculate the values you’d like to include in inline expressions in the returned JSX.
4. A component function can only return a single React element (you can’t return more than one value at a time from a JavaScript function). However, that single React element can have as many children as you wish. It’s very common to “wrap” all of the content you want a component to include in a single <div> to return, as in the above example.

> NEVER include an inline callback function so that you have a return statement inside of a return statement.

## Component Organizatiom
- Components are usually defined inside of separate modules (files), and then imported by the modules that need them
- Recall that in order to make a variable or function (e.g., a Component) available to other modules, you will need to ```export``` that component from its own module, and then ```import``` that value elsewhere:

```js
/* in Messages.js file */

//Export the defined components (as named exports)
export function HelloMessage() { /* ... */ }

export function GoodByeMessage() { /* ... */ }
```

```js
/* in App.js file */

//Import components needed from other modules
import { HelloMessage, GoodbyeMessage } from `./Messages.js`; //named imports!

//Can also export as a _default_ export; common if the file has only one component
export default function App() {
    return (
        <div>
            {/* Use the imported components */}
            <HelloMessage />
            <GoodbyeMessage />
        </div>
    )
}
```

```js
/* in index.js file */

//Import components needed from other modules
import App from `./App.js`; //default import!

//Render the imported component
ReactDOM.render(<App />, document.getElementById('root'));
```
> Notice that this “export-import” structure implies a one-directional hierarchy: the Message components don’t know about the App component that will render them (they are self-contained). You should not have two files that import from each other!

- The index.js file will usually just import a single component; that file stays very short and sweet. Put all of your component definitions in other files.

## Properties (props)
- Props are the “input parameters” to a component

```js
//Passing a prop called `message` with value "Hello property"
<MessageItem message="Hello property!" />;
```
- Prop names are written in camelCase.
- props are received as a single argument to the function (usually called props). This argument is a regular JavaScript object whose keys are the props’ “names”:

```js
//Define a component representing information about a user
function UserInfo(props) {
    //access the individual props from inside the argument object
    let userName = props.userName;
    let descriptor = props.descriptor;

    //can use props for logic or processing
    let userNameUpper = props.userName.toUpperCase();

    return (
        <div>
            <h1>{userNameUpper}</h1>
            <p>Hello, my name is {name} and I am a {descriptor}</p>
        </div>
    )
}

let userInfo = <UserInfo userName="Ethel" descriptor="Aardvark" />;
```
> Again, all props are stored in the argument object—you have to access them through that value.

## Props and Composition
- Since props are specified when a component instance is created, this means that a “parent” component will need to specify the props for its children.
- This creates a one-directional data flow—the data values are passed into the parent, which then passes data down to the children (not vice versa).

## Create vs. Render
- In order to effectively render a list (array) of data, you should define a Component that declares how to render a single element of that list (e.g., MessageItem). 
- This allows you to focus on only a single problem, developing a re-usable solution. Then you define another component that represents how to render a whole list of elements (e.g., MessageList). 
- And because including an array of Components as an inline expression in JSX will render those elements as siblings, it’s easy to render this list from within the parent:
- This kind of transformation is a mapping operation (each data value is mapped to a Component), and so can be done effecttively with the ```map()``` method:
```js
function MessageList(props) {
    let msgItems = props.messages.map((msgObject) => {
        //return a new MessageItem for each message object
        //attributes are listed on their own lines for readability
        return <MessageItem
                    message={msgObject.content}
                    key={msgObject.id.toString()} {/* pass in a key prop! */}
                    />;
    }) //end of .map()

    return (
        <div>
            <h1>Messages for you</h1>
            <ul>
                {msgItems}
            </ul>
        </div>
    ); //end of return
}

//Define and pass a prop to the parent comment when rendering it
ReactDOM.render(<MessageList messages={messageObjArray} />,
                document.getElementById('root'));
```
-  React requires you to specify an additional prop called key for each element in an array of components.
- React will use the key to keep track of those elements, so if they change over time (i.e., elements are added or removed from the array) React will be able to more efficiently modify the DOM.