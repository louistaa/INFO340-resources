# AJAX Requests
- JSON (JavaScript Object Notation) is a data format that can be directly parsed into JavaScript objects and arrays.
- JSON format uses a syntax that is almost identical to that for defining Object literals in JavaScript, with a few key differences:
1. JSON always defines an Object {} at the “top level”.
2. JSON object keys (which must be strings) must be written in double-quotes.
3. JSON values can only be strings, numbers, booleans (true or false), arrays ([]), or other objects. You cannot include a function in JSON.
4. JSON objects and arrays can’t have trailing commas or other extraneous symbols—no comments!

## Fetching Data
- We will utilize the ```fetch()``` API to easily send AJAX requests for data.
- The fetch() function makes it easy to send a request: simply call it and pass in the URL of the data you wish to download:
```fetch('https://domain.com/data');```.
- You can also fetch a local file, making sure its relative to the ```.html``` not ```.js``` file.

## Asynchronous Programming
- ```fetch()``` function does NOT directly return the data you want to download! Downloading data off the internet can take a long time: the network connection may be slow and the amount of data to download may be quite large.
- Because fetching data may take time, AJAX requests are made asynchronously.
- The download will occur at the same time that the rest of the code is being executed: it is best to think of fetch() as a function that will just “start to download data.
- fetch() is an asynchronous function (it’s code is run asynchronously), it returns what is called a ```Promise```. 
- A ```Promise``` is object that holds a value which may not be available yet.
- Promises have three possible states: 
1. Pending: the data is downloading
2. Fulfilled: the data has finished downloading
3. Rejected: the data failed to download and the promise was “broken”. 
- We are able to specify callback functions (similar to event listeners) that occur when a pending Promise is either successfully fulfilled or has been rejected.
- The “on success” callback function is specified by calling the .then() function on the Promise object, and passing the “on success callback” as a parameter.
- The “on success” callback will be passed a single parameter: the data value that the Promise was made for (e.g., the data that will eventually be downloaded from ```fetch()```). So when the callback is executed, you will have access to the data.
- This response object does have a body property that represents the “body” (data content) of the HTTP response.
- In order to get the body into a format you can use, you will need to “encode” it into a JavaScript object by calling the ```.json()``` method on it.

## Chaining Promises
- But there’s a catch: the “encoding” process performed by the .json() might take some time (particularly for a large amount of data). So instead of blocking (pausing) the rest of your program while that encoding occurs, the ```.json()``` method returns another Promise.
- So you will then need to specify a ```.then()``` callback for that Promise as well.
-  since the ```.json()``` encoding function returns a Promise, you can simply return that Promise from the ```.then()``` callback in order to make it available to subsequent ```.then()``` calls.
```js
fetch(url)  //start the download
    .then(function(response) {  //when done downloading
        let dataPromise = response.json();  //start encoding into an object
        return dataPromise;  //hand this Promise up
    })
    .then(function(data) {  //when done encoding
        //do something with the data!!
        console.log(data); //will now be encoded as a JavaScript object!
    });
```

## Handling Errors
- When downloading data from the internet, it is always possible that the HTTP request may fail.
- In order to deal with inevitable errors, Promises provide a .catch() method that is used to specify a callback that should occur if the Promise is rejected (an error occurs). This callback function will be passed an ```Error``` object that contains details about the error.
```js
fetch(url)
    .then(function(response) {  //when done downloading
        return response.json();  //second promise is anonymous
    })
    .then(function(data) {  //when done encoding
        //do something with the data!!
        console.log(data); //will now be encoded as a JavaScript object!
    })
    .catch(function(err) {
        //do something with the error
        console.error(err);  //e.g., show in the console
    });
```
- Importantly, the ```.catch()``` method will “catch” errors from all previous Promises in a .then() chain! This means that the above ```.catch()``` will show both errors in the downloading (```.fetch()```), and errors in the body encoding (```.json()```).

## AJAX with React
- APIs—including ```fetch()``` are not “built-in” to React like they are with a modern browser. As discussed in Chapter 14, in order to support these “other” browsers, you will need to load a polyfill. You can do that with React by installing the ```whatwg-fetch``` library, and then importing that polyfill in your React code:
```bash
# On command line, install the polyfill
npm install whatwg-fetch
```
- In your ```index.js```:
```js
//In your JavaScript, import the polyfill (loading it "globally")
//This will make the `fetch()` function available
import 'whatwg-fetch';
```
- Thus the best practice is to send the fetch() request for data, and then when the data has been downloaded, call the a set state function to update the component with the downloaded data.
- An effect hook lets you hook into the lifecycle of a component, specifying some code (a function) that should be run after the component finishes rendering.
- They are called effect hooks because they define a side effect to the component rendering.

```js
//import the hooks used
import React, { useState, useEffect } from 'react';

function MyComponent() {
    //store the data in a state variable, initialized as an empty array
    const [data, setData] = useState([]);

    //specify the effect hook function
    useEffect(() => {
        fetch(dataUri) //send AJAX request
          .then((res) => res.json())
          .then((data) => {
            let processedData = data.filter(...).map(...) //do desired processing
            setData(processedData) //change the state and re-render
          })
    }, []) //empty array is the second argument to the `useEffect()` function. 
           //It says to only run this effect on first render

    //Map the data values into DOM elements
    //Note that this works even before data is loaded (when the array is empty!)
    let dataItems = data.map((item) => {
        return <li key={item.id}>{item.value}</li>; //return DOM version of datum
    })

    //render the data items (e.g., as a list)
    return <ul>{dataItems}</ul>; 
  }
}
```
- Calling the ```useEffect()``` function specifies a callback function that will be run after the component renders.
- It takes as an argument the callback function to run after the component renders.
- Inside the ```useEffect()``` callback goes the normal ```fetch()``` call. Notice that the downloaded data is then assigned to the component’s state variable by calling the set state function.
- While technically it means the component is rendering twice (once without data, then once with), React can batch these requests together so that if the data downloads fast enough, the user will not notice.
- By default, the effect callback will be executed after each time the component renders. That means that if the component needed to re-render (because a prop changed for example), then the data would be downloaded a second time.
- To avoid this, you can pass the useEffect() function an optional second argument.
- This argument should be an array of values that the effect “depends on”—the effect will only be re-run if one of these variables changes between renders:
```js
//an effect that only re-runs if the `count` variable changes
useEffect(() => {
    //...
}, [count])
```
- By passing an empty array as a second argument, you tell the effect that it should only re-run if one of those (non-existent) variables updates—and since there are no variables listed, it will never run a second time.