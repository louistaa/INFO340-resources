# Chapter 10 JavaScript Fundamentals
- HTML and CSS are just used to give a website its meaning and appearance.
- You will need JavaScript to make them interactive.

## Programming with JavaScript
- Nothing substanial in this section, but just note that the most commonly supported version of JavaScript is ES6.

## Running JavaScript
- Include a link to your JavaScript file using a ```<script>``` tag in your HTML file, specifying a relative path to the file:
```html
<!DOCTYPE html>
<html>
<head>
  <!-- include here to run before the page appears -->
  <script src="js/script.js"></script>
</head>
<body>
   ... content ...

   <!-- include here to run "after" html appears -->
   <!-- we will usually do this -->
   <script src="js/script.js"></script>
</body>
<html>
```
- The ```<script>``` tag can be included anywhere in an HTML page. 
- Most commonly it is either placed in the ```<head>``` in order for the script to be executed before the page content loads, or at the very end of the ```<body>``` in order for the script to be executed after the page content loads.
> For this class, put your ```<script>``` tag at the end of the ```<body>```.

## Writing Scripts
- JavaScript has no ```main()``` method that is the starting point of the program.
- A ```.js``` file contains a sequence of statements that the interpreter executes one at a time from top to bottom.
```js
/* script.js */
/* This is the ENTIRE contents of the file! */
console.log("Hello world!");  //this is executed first
console.log("I'm doing JavaScript!");  //this is executed second
```
- ```console.log()``` is how you print values.
- Each statement should end with a semicolon marking the end of that statement.

## Strict Mode
- Strict mode is more “strict” about how the interpreter understands the syntax: it is less likely to assume that certain programmer mistakes were intentional.
- For example, in strict mode the interpreter will produce an Error if you try and use a variable that has not yet been defined, while without strict mode the code will just use an undefined value. 
- Thus working in strict mode can help catch a lot of silly mistakes.
- You declare that a script or function should be executed in strict mode by putting an interpreter declaration at the top:
```js
'use strict';
```
> ALWAYS USE STRICT MODE! It will help avoid typo-based bugs, as well as enable your code to run more efficiently.

## Variables
- Variables are dynamically typed. 
- This means that variables are not declared as a particular type (e.g., int or String).
- JavaScript variables are declared using the ```let``` keyword:
```js
let message = 'Hello World';  //a String
console.log(typeof message);  //=> `string`

let shoeSize = 7;  //a Number
console.log(typeof shoeSize);  //=> 'number'
```
> The ```typeof``` operator will return the data type of a variable. It is not widely used outside of debugging
- JavaScript variables should be given descriptive names using camelCase.
- Declared variables have a default value of undefined—a value representing that the variable has no value:
```js
//create a variable (not assigned)
let hoursSlept;
console.log(hoursSlept);  //=> undefined
```
- ```let``` was introduced in ES6. There is another way of intializing variables using ```var```.
- Difference is that variables declared with ```let``` are “block scoped”, meaning they are only available within the block (the {}) in which they are defined. 
- This is the same way variables are scoped in Java. 
- Variables declared with ```var```, on the other hand, are “functionally scoped” so are available anywhere within the function in which they are defined.
> Use ```let for this class```
- Along with let, JavaScript variables can also be declared using the ```const``` keyword to indicate that they are constant:
```js
const ISCHOOL_URL = 'https://ischool.uw.edu'; //declare constant
ISCHOOL_URL = 'https://example.com'; //TypeError: Assignment to constant variable.
```
### Basic Data Types
- JavaScript supports many of the same basic data types as Java and other languages:
1. Numbers: represent numeric data.
2. Strings: can be written in single or double quotes, but please use single.
3. Booleans: logical true or false.

### Arrays
- Arrays are ordered, 1-D sequence of values.
- JavaScript Arrays are written as literals inside square brackets ```[]```.
- Use 0-based indexing and bracket notation to access values.
```js
//an array of names
let names = ['John', 'Paul', 'George', 'Ringo'];

//an array of numbers (can contain "duplicate" values)
let numbers = [1, 2, 2, 3, 5, 8];

//arrays can contain different types (including other arrays!)
let things = ['raindrops', 2.5, true, [3, 4, 3]];

//arrays can be empty (contain no elements)
let empty = [];

//access using bracket notation
console.log( names[1] );  // "Paul"
console.log( things[3][2] );  // 3

numbers[0] = '340';  //assign new value at index 0
console.log( numbers );  // [340, 2, 2, 3, 5, 8]
```
- There are bunch of methods you can use on your arrays to modify its elements [here](https://www.w3schools.com/jsref/jsref_obj_array.asp).
- Use dot notation to call a method on an array:
```js
//Make a new array
let array = ['i','n','f','o'];

//add item to end of the array
array.push('340');
console.log(array); //=> ['i','n','f','o','340']

//combine elements into a string
let str = array.join('-');
console.log(str); //=> "i-n-f-o-340"

//get index of an element (first occurrence)
let oIndex = array.indexOf('o'); //=> 3

//remove 1 element starting at oIndex
array.splice(oIndex, 1);
console.log(array); //=> ['i','n','f','340']
```

### Objects
- Objects are unordered sequences of key-value pairs, where the keys (called “properties”) are arbitrary Strings and the values are any data type—each property can be used to look up (reference) the value associated with it.
- Objects are written as literals inside curly braces {}. Property-value pairs are written with a colon (:) between the property name and the value, and each element (pair) in the Object is separated by a comma (,). 
- Note that the property names do not need to be written in quotes if they are a single word (the quotes are implied—properties are always Strings):
```js
//an object of ages (explicit Strings for keys)
//The `ages` object has a `sarah` property (with a value of 42)
let ages = {
    'sarah': 42,
    'amit': 35,
    'zhang': 13
};

//different properties can have the same values
//property names with non-letter characters must be in quotes
let meals = {
    breakfast: 'coffee', 
    lunch: 'coffee', 
    'afternoon tea': 'coffee'
}

//values can be of different types (including arrays or other objects!)
let typeExamples = {
    number: 12, 
    string: 'dog', 
    array: [1,2,3]
};

//objects can be empty (contains no properties)
let empty = {}
```
- Objects are an unordered collection of key-value pairs: you reference a value by its property name and not by its position.
- When you ```console.log()``` an object, make sure to not concatenate it with a string:
```js
//convert object to string, won't log nicely
console.log("My object: " + myObject); //=> My object: [object Object]

//log the object directly
console.log("My object ", myObject); //=> My object {a: 1, b: 2}
```
#### Accessing Objects
- Object values can be access via bracket notation, specifying the property name as the index.
```js
let favorites = {music: 'jazz', food: 'pizza', numbers: [12, 42]};

//access variable
console.log( favorites['music'] ); //'jazz'
```
- Additionally, Object values can also be accessed via dot notation, as if the properties were public attributes of a class instance.
```js
let favorites = {music: 'jazz', food: 'pizza', numbers: [12, 42]};

//access variable
console.log( favorites.music ); //'jazz'
```
> IMPORTANT: The only advantage to using bracket notation is that you can specify property names as variables or the results of an expression. But overall, the recommendation is to use dot notation unless the property you wish to access is dynamically determined.
- It is possible to get an array of an object’s keys calling the ```Object.keys()``` method and passing in the object you wish to get the keys of.

#### Arrays of Objects
- Nesting data structures allows us to define arbitrarily complex information schemas.
- One of the most common forms of nesting you’ll see is to have an array of objects where each object has the same properties (but different values):
```js
//an arbitrary list of people's names, heights, and weights
let people = [
    {name: 'Ada', height: 58, 'weight': 115},
    {name: 'Bob', height: 59, 'weight': 117},
    {name: 'Chris', height: 60, 'weight': 120},
    {name: 'Diya', height: 61, 'weight': 123},
    {name: 'Emma', height: 62, 'weight': 126}
]
```
- Each object (record) acts as a “row” in the table, and each property (feature) acts as a “column”. As long as all of the objects share the same keys, this array of objects is a table.

### Control Structures
- Same exact control structures you've seen in Java:
```js
if(condition){
  //statements
}
else if(alternativeCondition) {
  //statements
}
else {
  //statements
}
```
## Functions
- The following sytnax:
```js
function nameOfFunction(parameterOne, parameterTwo) {
    // do something here

    return something;
}

// call the function
let savedValue = nameOfFunction(parameterOne, parameterTwo);
```
- If a function lacks a return value, then that function returns the value ```undefined```.