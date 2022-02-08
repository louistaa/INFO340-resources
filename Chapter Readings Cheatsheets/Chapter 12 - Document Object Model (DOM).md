# Chapter 12 Document Object Model (DOM)
- The programmatic representation of the HTML elements currently being shown by the browser is known as the Document Object Model (DOM)
- JavaScript code is used to modify the DOM (HTML elements) currently being shown by the browser in response to user input, thereby making the page interactve.

## The DOM API
- Considering a web page’s content to be a tree of HTML elements is one way to model (represent) the structure of that information. This particular model of a web document (as a tree of object nodes) is called the Document Object Model, or DOM.
- We refer to the web page’s content as “the DOM”, and an HTML element as a “DOM element”.
- DOM provides an Application Programming Interface (API) which allows you to access and manipulate the set of HTML elements via tge ```document``` global object.

## DOM Manipulation
- You access properties and call methods on the ```document``` object to manipulate the content displayed in the browser.

### Referencing HTML Elements
- In order to manipulate the DOM elements in a page, you first need to get a reference to the element you want to change
- You can get these variable references by using one of the document “selector” functions:
```js
//element with id="foo"
let fooElem = document.getElementById('foo');

//elements with class="row"
let rowElems = document.getElementsByClassName('row'); //note the plural!

//<li> elements
let liElems = document.getElementsByTagName('li'); //note the plural!

/*easiest to select by reusing CSS selectors! */
let cssSelector = 'header p, .title > p';  //a string of a CSS selector

//selects FIRST element that matches css selector
let elem = document.querySelector(cssSelector);

//matches ALL elements that match css selector
let elems = document.querySelectorAll(cssSelector);
```
- The ```document.querySelector()``` is by far the most flexible and easy to use of these methods: it can easily do the same as all the other methods (just put in an id, class, or element selector). You should always use ```querySelector()```.

### Modifying HTML Elements
- Once you have a reference to an element, you access properties and call methods on that object in order to modify its state in the DOM—which will in turn modify how it currently is displayed on the page.
> Note: setting these properties do not change the .html source code file! Instead, they just change the rendered DOM elements (think: the content stored in the computer’s memory rather than in a file). If you refresh the page, the content will go back to how the .html source code file specifies it should appear.

#### Changing Content
- ```textContent```: refer to all the text content in an element (ignoring HTML markup like ```<em>``` or ```<strong>```)
- ```innerHTML```: refer to all text content including any HTML markups.
```js
let text = elem.textContent; //the text content of the elem
elem.textContent = "This is different content!"; //change the content

let html = elem.innerHTML; //content including HTML
elem.innerHTML = "This is <em>different</em> content!"; //interpreted as HTML
```
- You can “clear” the content of an element by setting it’s content to be an empty string (''):
```js
let alertElem = document.querySelector('.alert');
alertElem.textContent = ''; //no more alert!
```
### Changing Attributes
- Each attribute defined in the HTML specification is typically exposed as a property of the element object:
```js
//get a reference to the `#picture` element
let imgElem = document.querySelector('#picture');

//access the attribute
console.log( imgElem.src ); //logs the source of the image

//modify the attribute
imgElem.src = 'my-picture.png';
```
- Can also use the ```getAttribute()``` or ```setAtribute()``` methods:

```js
let imgElem = document.querySelector('#picture');
imgElement.setAttribute('src', 'my-other-picture.png'); //set the src

console.log( imgElem.getAttribute('src') ); //=> 'my-other-picture.png'
```
### Changing Element CSS
- Use the ```classList``` property to add or remove class names from an element:
```js
//access list of classes
let classList = elem.classList;

//add a class
elem.classList.add('small'); //add a single class
elem.classList.add('alert','alert-warning'); //add multiples classes (not on IE)

//remove a class
elem.classList.remove('small');

//"toggle" (add if missing, remove if present)
elem.classList.toggle('small');
```
## Modifying the DOM Tree
- You can also call methods to create and add new HTML DOM elements to the tree. The ```document.createElement()``` function is used to create a new HTML element. However this element is not created a part of the tree (after all, you haven’t specified where it would put into the page)! Thus you need to also use a method such as ```appendChild``` to add that new element as a child of another element:
```js
//create a new <p> (not yet in the tree)
let newP = document.createElement('p');
newP.textContent = "I'm new!";

//create Node of textContent only (not an HTML element, just text)
let newText = document.createTextNode("I'm blank");

let main = document.querySelector('main');
main.appendChild(newP); //add element INSIDE (at end)
main.appendChild(newText); //add the text inside, AFTER the <p>

//add anonymous new node BEFORE element. Parameters are: (new, old)
main.insertBefore(document.createTextNode("First!"), newP);

//replace node. Parameters are: (new, old)
main.replaceChild(document.createTextNode('boo'), newText);

//remove node
main.removeChild(main.querySelector('p'));
```
## Listening for Events
- In order to make a page interactive, you need to be able to respond to user events.
- Whenever a user interacts with a computer, the operating system announces that interaction as an event—the event of a button being clicked, the event of the mouse being moved, the event of a keyboard key being pressed, etc.
- These events are broadcast to the entire system, allowing any application (including the browser) to “respond” the occurrence of the event, such as by executing a particular JavaScript function.
- Thus in order to respond to user actions (and the events those actions generate), we need to define a function that will be executed when the event occurs.
- The DOM API allows you to register an event listener by call the .addEventListener() on a selected element (e.g., on the element that you want to listen to). This method takes two arguments: a string representing what kind of event you want to listen for, and a callback function to execute when you hear that event:

```js
//a (named) callback function
function onClickCallback() {
    console.log("You clicked me!");
}

//get a reference to the element we want to "listen" to
let button = document.querySelector('button');

//register a listener for 'click' events
button.addEventListener('click', onClickCallback);
```
- When the button is clicked by the user, it will “shout” out a 'click' event (“I was clicked! I was clicked!”). Because you have set up a listener (an alert/notification) for such an occurrence, your script will be able to do something—and that something that it will do is run the specified callback function.
- It is much more common to use an anonymous function as the callback:
```js
let button = document.querySelect.select('button');
button.addEventListener('click', function() {
    console.log("You clicked me!");
});
```

#### Event
- The event callback will be passed in a single argument: an object representing the “event” that occurred.
- This event includes information such as where the event occurred (in x,y coordinates), what DOM element caused the event, and more:
```js
elem.addEventListener('click', function(event) {
   //get who was clicked;
   let clickedElem = event.target; //target property of the event
   console.log(clickedElem);
});
```
- Full list of types of events to listen for [here](https://developer.mozilla.org/en-US/docs/Web/Events).