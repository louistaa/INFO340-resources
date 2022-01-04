# Chapter 3 HTML Fundamentals
## Introduction
- HTML is the standard [markup language](https://www.computerhope.com/jargon/m/markup-language.html) for creating web pages.
- HTML describes the structure and content of a web page.
- Browsers read/interpret HTML code to know how to display web page elements.
- HTML content is written in .html files.
- The average website includes several different HTML files: one file for the home page, another file for the about page, etc.
    - The index.html file is where a website's home page typically lives.

> HTML is not considered a programming language as it can’t create dynamic functionality.

## HTML Elements
- All HTML pages have HTML elements which consists of 3 parts:
    1. Opening tag: used to state where an element starts to take effect. Denoted by the opening and closing angle brackets. For example: ```<p>``` denotes the start of a paragraph element.
    2. Content: Whatever you want to show on the web page.
    3. Closing tag: used to state where an element ends. Same annotation as the opening tag but a slash before the element name. For example: ```</p>``` denotes the end of a paragraph element.

Example HTML elements:
```html
<p>This is a paragraph</p>

<h1>This is a first-level heading</h1>

<h2>This is a second-level heading</h2>
```

- HTML tags are not case sensitive, but they should always be lowercase.
- Line breaks are white spaces around tags are ignored, but make sure to use them for easier code readability.
- Comprehensive list of all HTML elements [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element). 

## Comments
- Its pretty hard to type so use the cmd + / (or ctrl + / on Windows) short cut on the line of code you want to comment out.
```html
<!-- <p>This is commented out hehe </p> -->
<p>This is not commented out, and thus the world can see it.</p>
```

## Attributes
- The opening tag of a HTML element can optionally contain one or more attributes.
- Attributes add additional meaning to an element, similiar to how you pass in parameters to methods in previous coding courses.
- Syntax of attributes: ```attributeName=value```, with no spaces around the ```=```.
- Value are almost always strings.
- If an element is taking more than one attribute, separate them with a space:

```html
<tag attributeA="value" attributeB="value">
   content
</tag>
```
- Some some HTML elements have mandatory attributes. For example, the ```<img>``` element requires a ```src``` attribute. Or else it won't know where to look for the image you want to display.
- Some attributes can be used with all HTML elements, called Global Attributes.
- Comprehensive list of Global Attributes [here](https://www.w3schools.com/tags/ref_standardattributes.asp).
    - Most common Global Attributes you'll use are ```id``` and ```class```.
- ```id``` attribute gives your HTML element a unique identifier so you can refer to it in your CSS/JavaScript code.
- Comprehensive list of HTML element attributes [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes).

## Empty Elements
- A few HTML elements don’t require a closing tag because they can’t contain any content (the middle section between the closing and opening brackets).
- So you can leave off the closing tag entirely.
- Comprehensive list of Empty Elements [here](https://developer.mozilla.org/en-US/docs/Glossary/Empty_element).

## Nesting Elements
- Your typical website is made of up hundreds or thousands of HTML elements.
- Hence, elements becoming nested within each other. Meaning the content of an HTML element can contain HTML elements inside of it.
- This creates a tree-like structure to websites, which in front end development, we called the DOM or Document Object Model.
- For example:
```html
<h1><em>Hello world!</em></h1>
```
- The above line of code will create a level-one heading of the emphasized text.

## Block vs. Inline Elements
- All HTML elements fall into two categories:
    1. Block elements form a visible “block” on a page. They will be on a new line from the previous content, and any content after it will also be on a new line
        - The ```<div>``` tag (short for Content Division) is used as a container for HTML elements and is the most basic block element. Anything you put inside a ```<div>``` will be on its own line.
    2. Inline elements are contained on the same line of content. Meaning, they will not have a line break after them.
        - The ```<span>``` tag (short for Content Span) is also used a container for HTML elements and is the most basic inline element. Anything you put inside a ```<span>``` will be on the same line as other content.

## Web Page Structure
- All HTML files start with a document type declaration, commonly referred to as the “Doctype.”
- The document type declaration tells the browser what format and syntax your document is using.

## The ```<head>``` Section
- The ```<head>``` element contains metadata about the document.
- A few common elements you should always inside in the ```<head>```:
    1. ```<title>```: This will be the tab name of your website. This is also used by search indexers (Google, Bing, etc.) and screen readers so it should be informative and reflective of the content.
    2. ```<meta>```: short for "metadata", it takes in two attributes called ```"name"``` and ```"content"``` (like parameters) to describe information about the page's data. - The ```content``` attribute takes in a string of whatever is applicable to your project.

> Something a bit tricky is that the ```"name"``` attribute takes in a precise value string. There are six which can be found [here](https://www.w3schools.com/tags/tag_meta.asp). You'll only ever need to worry about ```author```, ```description``` and ```viewport``` for this class.

## Web Page Template
- Put this in your own personal cheat sheet!
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="author" content="your name">
    <meta name="description" content="description of your page">
    <title>My Page Title</title>
</head>
<body>
    ...
    Content goes here!
    ...
</body>
</html>
```
- You can use the VS Code shortcut of writing an exclamation point (!) then hitting the ```tab``` key to create a similar page skeleton.
    - This only works in .html files.

## More reading for my overachievers
1. https://www.hostinger.com/tutorials/what-is-html
2. https://www.w3schools.com/html/html_attributes.asp