# Chapter 15:  Interactive React
## Handling Events in React
- You can handle user interaction in React in the same way you would using the DOM or jQuery: you register an event listener and specify a callback function to execute when that event occurs.
- Register event listeners by specifying a React-specific attribute on an element. The attribute is generally named with the word on followed by the name of the event you want to respond to in camelCase format.
- For example, ```onClick``` registers a listener for click events, ```onMouseOver``` for mouseover events.
- Attribute should be assigned a value that is a reference to a callback function (specified as an inline expression).
```js
//A component representing a button that logs a message when clicked
function MyButton() {
    //A function to call when clicked. The name is conventional, but arbitrary.
    //The callback will be passed the DOM event (just like with DOM callbacks)
    const handleClick = (event) => {
        console.log('The button has been clicked');
    }

    //make a button with an `onClick` attribute!
    //this "registers" the listener and sets the callback
    return <button onClick={handleClick}>Click me!</button>;
}
```
- This component renders a ```<button>``` in the DOM with a registered click event. Clicking on that DOM element will cause the handleClick function to be executed.
> You can only register events on React elements (HTML elements like ```<button>```, that are named with lowercase letters), not on Components. If you tried to specify a ```<MyButton onClick={callback}>```, you would be passing a prop that just happened to be called onClick, but otherwise has no special meaning!

## State and Hooks
- In order for the page to be interactive you need to be able to manipulate its rendered content when that event occurs.
- a component will need to keep track of its state or situation—the number on the counter, how the table is sorted, or which “page” is being shown. 
- In React, a component’s state represents internal, dynamic information about how that Component should be rendered. 
- The state contains data that changes over time (and only such information—if the value won’t change for that instance of a component, it shouldn’t be part of the state).
- whenever the state is changed, a React component will automatically “rerender”—the component will be “rerun” and the new, updated DOM elements returned will be displayed on the screen.
- State can be specified for a function component by using a state [hook](https://reactjs.org/docs/hooks-intro.html).
- The state hook in particular lets you hook into the state of a component, specifying what values should be “tracked” and should cause the component to rerender.
- Hooks were introduced with React v16.8 (October 2018), and thus are the “new” current way of handling state.
    - The older syntax of managing state is using class components. If you ever stumble upon a tutorial that has weird syntax, is it probably not using hooks!
- The state hook is a function provided by React called ```useState()```. This function will need to be imported from the React library (note that it is a named export so should be imported as such):
```js
//import the state hook function
import React, { useState } from 'react';
```
- Calling the useState() function creates a “state variable”—a value that will be tracked and stored between calls to render/rerender the component.
- The ```useState()``` function is passed the initial starting value for the state variable. In above example, the count state variable will be initialized as ```0```.
- The ```useState()``` function returns an array of two values: the first is the current value of the state (e.g., what it was initialized as), and the second is a function used to modify that particular state variable (a “setter” or mutator).
```js
function CountingButton() {
    //Define a `count` state variable, initially 0
    const [count, setCount] = useState(0);

    //an event handling callback
    const handleClick = (event) => {
        setCount(count+1); //update the state to be a new value
    }

    return (
        { /* a button with the event handler that displays the state variable */}
        <button onClick={handleClick}>You clicked me {count} times</button>
    );
}
```
- Above is equal to:
```js
const hookArray = useState(0); //the function returns an array of 2 values
const count = hookArray[0]; //assign the 1st elem (a value) to `count`
const setCount = hookArray[1]; //assign the 2nd elem (a function) to `setCount`
```
- Importantly, there is nothing magical about the names of the variables that the useState() result is assigned to. It could just as well have been written:
```js
const [countVariable, functionToUpdateCount] = useState(0)
```
> Because the function is a “setter” it’s usually named as such (setVARIABLE), but this is not required. It’s just a function; you can name it whatever you want.
- Note that if the value isn’t actually used in the rendered DOM in any way (directly or indirectly), it probably shouldn’t be part of the state.

## Updating State
- It’s not possible to change the value of a state variable directly (e.g,. you can’t do count = count +1)—that’s why the variable is declared as ```const```.
- Instead, you need to use the “set state” function that was created (e.g., setCount() in the above example). This function will take as an argument the new value to assign to the state variable (overwriting the previous value).
- When the set state function is called, not only will it change the value of the state variable, but it will also “rerender” the component—it will cause the component function to be called again, returning a new set of DOM elements to be shown on the screen. These DOM elements will replace the previously rendered version of the component.
- React merges these changes into the page’s DOM in a highly efficiency manner, changing only the elements that have actually updated—this is what makes React so effective for large scale systems.

> Fun fact: React was built for Facebook as there are so many components to manage!

- This is one of the trickier parts to remember in React: when you call a set state function, it will cause your component function to “re-run”—which means that any logic will execute for a second time.
- Hence, never call a set state funcction inside your return. It will create an infinite loop.
- Moreover, set state functions are asynchronous. Calling the function only sends a “request” to update the state; it doesn’t happen immediately. This is because React will “batch” multiple requests to update the state of components (and so to rerender them) together—that way if your app needs to make lots of small changes at the same time, React only needs to regenerate the DOM once, providing a significant performance boost.
- It is possible to have multiple state variables, each declared with a different all to ```useState()```:
```js
//Example from React documentation
function ExampleWithManyStates() {
    //Declare multiple state variables!
    const [age, setAge] = useState(42);
    const [fruit, setFruit] = useState('banana');
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
}
```
- While it’s possible for a single state variable to contain complex values (objects and arrays, as in the todos variable above), it’s often cleaner to use multiple different state variables—that way React needs to change as little data as possible when you wish to update a variable.
- You need to pass a new value into the set state function in order for it to actually update the state and rerender the component. Just changing a value inside of an existing object won’t work.
- You'll need to create a new copy of the array or object, and then pass that new value into the set state function:
```js
function TodoList() {
    //a state value that is an array of objects
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);

    const handleClick = (event) => {
        //create a copy of the array using the `map()` function
        const todosCopy = todos.map((todoObject, index) => {
            if(index == 0) { //transform objects if needed
                todoObject.text = "Fix bugs"
            }
            return todoObject; //return object to go into new array
        })
        setTodos(todosCopy) //This works!
    }
}
```
- The ```.map()``` function is usually the easiest way to copy an array, though other techniques exist as well. If you wish to copy an object, you can do this easily using the spread operator to create a new object using the properties of the first:

```js
//an original object
const original = {a: 1, b: 2};

//Create a copy, taking the property of `original` and assigning them into
//a fresh object
const copy = { ...original } //using the spread operator
console.log(copy) //{a: 1, b: 2}
console.log(copy == original) //false, different objects
```
## State vs. Props
- Props are the “inputs” into a component, the values that someone else tells the Component.
- State is “internal” to the Component, and is (only) for values that change over time. If the value doesn’t change over the life of the Component (e.g., in response to a user event), it shouldn’t be part of the state.

## Lifting Up State
- A component state is purely internal to that component—neither the component’s parent element nor its children have access to (or are even aware of) that state. State represents only information about that particular component (and that particular instance of the component).
- While passing state data to a child (as a prop) is easy, communicating state data to a parent or sibling is more complicated. For example, you may want to have a ```SearchForm``` component that is able to search for data, but want to then have a sibling ```ResultsList``` component that is able to display the rendered results:
```js
<App>
  <SearchForm /> {/* has the data */}
  <ResultsList /> {/* needs the data */}
</App>
```
- When confronted with this problem, the best practice in React is to lift the state up to the the closest common ancestor. This means that instead of having the data be stored in the state of one of the children, you instead store the data in the state of the parent.
- But with the state stored in the parent, the children elements (e.g., the SearchForm) may still need a way to interact with that parent and tell it to change its state. To do this, you can have the parent define a function that changes its state, and then pass the child that callback function as a prop. The child will then be able to execute that callback prop, thereby telling the parent to do something (such as update its state).
- In the following example, the parent component (VotingApp) stores state data about how many times each button has been pressed, passing a callback function (countClick) to its child Components (CandidateButton). The CandidateButton will then execute that callback when it is clicked. Executing this function causes the VotingApp to update its state and re-render the buttons, which show updated text based on the props given to them:

```js
function VotingApp(props) {
    //initialize the state counts, one for each color
    //using a single state value so that there is only one "update" function
    const [counts, setCounts] = useState({red: 0, blue: 0})

    //a function to update the state
    //expects a "color" for which button was clicked
    const handleCount = function(color) {
        console.log(color + " got a vote!");

        const newCounts = { ...counts } //make a duplicate of the object
        newCounts[color]++; //update the local copy

        setCounts(newCounts) //update the state with the changed copy
    }

    //render based on current state
    let winner = "tie"; 
    if(counts.red > counts.blue) winner = "red"
    else if(counts.blue > counts.red) winner = "blue"
    return (
        <div>
            <p>Current winner is: {winner}</p>
            {/* Pass the callback to each button as a prop */}
            <CandidateButton color="red" winner={winner} callback={handleCount} />
            <CandidateButton color="blue" winner={winner} callback={handleCount} />
        </div>
    );
}

function CandidateButton() {
    const handleClick = () => {
        //On click, execute the given callback function (passing in own name)
        props.callback(props.color)
    }

    //render based on current props
    let label = "I am not winning";
    if(props.winner === props.color)
        label = "I am winning!"

    return (
        <button className={props.color} onClick={handleClick}>
            {label}
        </button>
    );
}
```
- If you can understand this example, congrats! You are a master of React now :).

## Specific Interactions:
- In normal HTML, form elements such as ```<input>``` keep track of their own “state”. For example, whatever the user has typed into a text input will be stored in that input’s value property.
- In React, you need to save the ```<input>```'s value in a state variable so you can control it.
```js
function MyInput(props) {
    const [inputValue, setInputValue] = useState('')//initialize as empty string

    //respond to input changes
    const handleChange = (event) => {
        //get the value that the <input> now has
        let newValue = event.target.value

        //update the state to use that new value, rendering the component
        setInputValue(newValue);
    }

    return (
        <div>
            {/* The input will be rendered with the React-controlled value */} 
            <input type="text" onChange={handleChange} value={inputValue} />
            <p>You typed: {inputValue}</p>
        </div>
    );
}
```
- When the user enters a different value into the ```<input>``` element, the handleChange() callback is executed. This grabs that updated value and saves it in the component’s inputValue state variable. Updating that state variable also causes the component to re-render, which recreates a brand new version of the ```<input>``` element, but now with the React-controlled value for its value attribute.
- And of course, a controlled form might render multiple ```<input>``` elements, tracking the values of each one in a separate variable in the state.