# Chapter 11 Functional Programming
## Functions ARE Variables
- Just how variables can be type ```int``` or ```string```, variables can be type ```function```.
- IMPORTANT: We refer to a function by it’s name without the parentheses.
    - Referring to a function with parentheses will execute it.
- How to assign a variable to a function:
```js
let sayHello = function(person) {
    console.log("Hello, "+person);
}
```

## Anonymous Functions
- An unnamed data scructure or function is anonymous
```js
//named function (normal)
function sayHello(person){
    console.log("Hello, "+person);
}

//an anonymous function (with no name!)
//(We can't reference this without a name, so writing an anonymous function is
//not a valid statement)
function(person) {
    console.log("Hello, "+person);
}

```
- Anonymous functions are used as callback functions
## Callback Functions
> This is where JavaScript gets confusing, so make sure to understand this concept!
- Since functions are variables, they can be passed as parameters to other functions.
```js
//create a function `sayHello`
function sayHello(name){
    console.log("Hello, "+name);
}

//a function that takes ANOTHER FUNCTION as an argument
//this function will call the argument function, passing it "world"
function doWithWorld(funcToCall){
    //call the given function with an argument of "world"
    funcToCall("world");
}

doWithWorld(sayHello);  //logs "Hello world";
```
- When you pass a function as an arguement, you don't put any parenthesis after it.
- You want to reference the function by its name.
```js
function greet() {  //version with no args for clarity
    return "Hello";
}

//log out the function value itself
console.log(greet);  //logs e.g., [Function: greet], the function

console.log(greet());  //logs "Hello", which is what `sayHello()` resolves to
```
- A function that is passed into another is commonly referred to as a callback function: it is an argument that the other function will “call back to” and execute when needed.
- If you understand the following lines of code you will understand callback functions:
```js
function doTogether(firstCallback, secondCallback){
    firstCallback();  //execute the first function
    secondCallback();  //execute the second function
    console.log('at the same time!');
}

function patHead() {
    console.log('pat your head');
}

function rubBelly() {
    console.log('rub your belly');
}

//pass in the callbacks to do them together
doTogether(patHead, rubBelly);
```

### Anonymous Callback Functions
- Often a callback function will be defined just to be passed into a single other function. 
- This makes naming the callback unncessary, and so it is more common to utilize anonymous callback functions:
- Instead of this:
```js
//name anonymous function by assigning to variable
let sayHello = function(name){
    console.log("Hello, "+name);
}

function doWithWorld(funcToCall){
    funcToCall("world");
}

//pass the named function by name
doWithWorld(sayHello);
```
- We can write this:
```js
//pass in anonymous version of the function
doWithWorld(function(name){
    console.log("Hello, "+name);
});
```

## Functional Looping
- Consider the following for-loop:
```js
let array = [{...}, {...}, {...}];

for(let i=0; i<array.length; i++){
    let currentItem = array[i]; //convenience variable for current item

    //do something with current item
    console.log(currentItem);
}
```
- While this loop may be familiar and fast, it does require extra work to manage the loop control variable (the ```i```), which can get especially confusing when dealing with nested loops (and nested data structures are very common in JavaScript).
### forEach method
- ```forEach()``` method goes through each item in the array and executes the given callback function, passing each item as the parameter to the callback.
- Method allows you to specify what to do with each element in the array as a separate function then apply it to all the elements.
- Implementation of the ```forEach()``` looks like this:
```js
Array.forEach = function(callback) { //define the Array's forEach method
    for(let i=0; i<this.length; i++) {
        callback(this[i], i, this);
    }
}
```
- Method does the job of managing the loop and the loop control variable for you, allowing you to just focus on what you want to do for each item.
- Most common to use this method with an anonymous callback function.
```js
//print each item in the array
array.forEach(function(item){
    console.log(item);
})
```
- This code can almost be read as: “take the array and ```forEach``` thing execute the ```function``` on that ```item```”.

## Map
- Mapping: take an original array and produces a new array with each of the original elements transformed in a certain way.
- The array’s ```map()``` function produces a new array with each of the elements transformed. 
- The ```map()``` function takes as an argument a callback function that will do the transformation. 
- Also written using anonymous callback syntax:
```js
let numbers = [1,2,3,4,5];  //an initial array
let squares = numbers.map(function(item){
    return n*n;
});
```
> Note: the major difference between the ```.forEach``` method and the ```.map``` method is that the ```.map``` method will return each element. If you need to create a new array, you should use ```.map```. If you simply need to do something for each element in an array, use ```.forEach```.

## Filter
- Filter a list of elements, removing elements that we don’t want (or more accurately: only keeping elements that we DO want).
- The array’s ```filter()``` function produces a new array that contains only the elements that do match a specific criteria. 
- The ```filter()``` function takes as an argument a callback function that will make this decision.
```js
let numbers = [2,7,1,8,3];  //an initial array
let evens = numbers.filter(function(n) { return (n%2)==0; }); //one-liner!
```