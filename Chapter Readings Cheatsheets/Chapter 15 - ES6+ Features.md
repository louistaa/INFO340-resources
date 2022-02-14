# Chapter 15 ES6+ Features
- ECMAScript specification for the JavaScript language has gone through several different versions, each of which adds new syntax and features to try and make the language more powerful or easier to work with. In 2015, a new version of the language was released—officially called “ECMAScript 2015”, most developers refer to it by the working name “ES6” (e.g., version 6 of the language).

## ES6 Class Syntax
```js
//class declaration
class Person {

    //a Constructor method
    //this is called when the class is instantiated (with `new`)
    //and has the job of initializing the attributes
    constructor(newName, newAge) {
        //assign parameters to the attributes
        this.firstName = newName;
        this.age = newAge;
    }

    //return this Person's name
    getName() {
        return this.firstName; //return own attribute
    }

    //grow a year
    haveBirthday() {
        this.age++; //increase this person's age (accessing own attribute)
    }

    //a method that takes in a Person type as a parameter
    sayHello(otherPerson) {
        //call method on parameter object for printing
        console.log("Hello, " + otherPerson.getName());

        //access own attribute for printing
        console.log("I am " + this.age +  " years old");
    }
}
```
- How you would use the class:
```js
//instantiate two new People objects
let aliceObj = new Person("Alice", 21);
let bobObj = new Person("Bob", 42);

//call method on Alice (changing her attributes)
aliceObj.haveBirthday();

//call the method ON Alice, and PASS Bob as a param to it
aliceObj.sayHello(bobObj);
```

## Arrow Functions
- Anonymous values:
```js
let sayHello = function(name) {
  return 'Hello '+name;
}
```
- This synax is so common, especially in anonymous callbacks, so ES6 made a more concise syntax: arrow functions.
```js
//normal function syntax
let printHello = function() {
    console.log('Hello world');
}

//arrow syntax
let printHello = () => {
    console.log('Hello world');
}

//concise body
let printHello = () => console.log('Hello world');
```
- So then code can be simplified:
```js
let array = [1,2,3]; //an array to work with

//normal function
array.map(function(num) {
  return num*2; //multiply each item by 2
});

//arrow syntax
array.map(num => {
  return num*2; //multiply each item by 2
});

//concise body
array.map(num => num*2);
```
> Always use arrow functions for anonymous callbacks going forward.

## Modules
- If you want to make a variable available from one module to use in another, you will need to export it using the ```export``` keyword in front of a variable.
- You write the keyword ```import```, following by a set of braces { } containing a comma-separated sequence of variables you wish to “import” from a particular module.

```js
/*** my-module.js ***/
export let question = "Why'd the chicken cross the road?";
export let answer = "To get to the other side";
export function laugh() {
    console.log("hahaha");
}

/*** index.js ***/
import { question, answer, laugh } from './my-module';

console.log(question); //=> "Why'd the chicken cross the road?"
console.log(answer); //=> "To get to the other side"
laugh(); //"hahaha"
```
> Note that you can export functions as well as variables, since functions are values!

- Different ways to export/import:
```js
/*** my-module.js ***/
export function foo() { return 'foo'; } //make available (as above)

function bar() { return 'bar'; }
export bar; //export previously defined variable

export { bar as barFunction }; //provide an "alias" (consumer name) for value

//will not be available (a "private" function)
function baz() { return 'baz'; }

/*** index.js ***/
import {foo, barFunction} from './my-module'; //import multiple values
foo() //=> 'foo'
barFunction() //=> 'bar'

import {foo as myFoo} from './my-module'; //provide an "alias" for value
myFoo(); //=> 'foo'

import * as theModule from './my-module'; //import everything that was exported
                                          //loads as a single object with values
                                          //as properties
theModule.foo(); //=> 'foo'
theModule.barFunction(); //=> 'bar'
```
- You can use the as keyword to “alias” a variable either when it is exported (so it is shared with a different name) or when it is imported (so it is loaded and assigned a different name). This is particularly useful when trying to produce a clean API for a module (so you export values with consistent names, even if you don’t use those internally), or when you want to import a variable with a very long name.
- It is possible to just import everything that was exported by a module using the import * as syntax. You specify an object name that will represent the values exported module (e.g., theModule in the example), and each exported variable will be a property of that object. This is particularly useful when you may be adding extra exports to a module during development, but don’t want to keep adjusting the import statement.

## Default Exports
- Each module can also export a single (just one!) default variable.
- You specify the default export by including the ```default``` keyword immediately after export:
```js
/*** my-module.js ***/
//this function is the "default" export
export default function sayHello() {
    return 'Hello world!';
}

/*** index.js ***/
import greet from './my-module'; //import the default value giving it any name

greet(); //=> "Hello world!"
```
- When importing a default export, you just provide the variable name (“alias”) you wish to refer to that exported value by.