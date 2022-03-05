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