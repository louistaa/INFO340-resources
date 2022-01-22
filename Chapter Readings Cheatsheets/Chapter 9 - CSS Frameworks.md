# Chapter 9 CSS Frameworks
- CSS becomes tedious quickly as your website scales.
- Instead of specifying your own rules, perhaps you want a have a set of "standard" rules and then style those rules to your liking. 
- That is why CSS frameworks became a thing.
- A CSS Framework is a stylesheet (a .css file!) that contains a large list of pre-defined rules that you can apply to your page.
    - To gain access to the styling that someone else wrote, you just have to apply the class names to your HTML elements.
- [Bootstrap](https://getbootstrap.com/): most commonly used CSS framework built by Twitter. Popularity makes it well tested, documented and supported amongst browsers. However, its so popular that it makes your website look cliche.

## Using a Framework
- You must realize that a CSS framework is just a stylesheet with a bunch of rules that someone else wrote for you.
> If you don't understand this, then you won't know what you are coding!
- Because a CSS framework is just a CSS file, you include one in your page using a ```<link>``` element just like with any other stylesheet:
```html
<head>
  <!--... other elements here...-->

  <link rel="stylesheet"
        href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.css">
  <link rel="stylesheet" href="css/my-style.css">
</head>
```
- Note that you link the CSS framework before you link your own stylesheet. 
- Remember that CSS is read top-to-bottom, and that the last rule on the page wins. 
- By putting your stylesheet second, any rules you define will override the rules specified in the framework, thereby allowing you to continue to customize the appearance.
- It is most common to include the minified versions of CSS frameworks: these are usually named as .min.css files (e.g., bootstrap.min.css). 
    -  A minified file is one that has extra comments and white space removed, creating a file with a much smaller size.

### CDNs
- A content delivery network (CDN) is a web service that serves files commonly used by multiple websites.
- Provide the URL for the file on the CDN serves as the ```href``` of your link.
- Using a CDN with Bootstrap:
```html
  <link rel="stylesheet"
        href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.css">
```

## Bootstrap
> Note: this class only goes over a very very small amount of Bootstrap. Read the [documentation](https://getbootstrap.com/) to fill in the gaps and use it to it's full potential!
- To use Bootstrap CSS and its components, link its ```.css`` file to your HTML file using a CDN.
- Latest version is on the Bootstrap [home page](https://getbootstrap.com/).
- It'll look something like this:
```html
<link rel="stylesheet" 
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css" 
      integrity="sha384-9gVQ4dYFwwWSjIDZnLEWnxCjeSWFphJiwGPXr1jddIhOegiu1FwO5qRGvFXOdJZ4" 
      crossorigin="anonymous">
```
- ```integrity``` gives a cryptographic hash of the source code so the browser can make sure you didn’t download a malicious file by mistake.
- ```crossorigin ``` says that no credentials are sent to the remote server.

### Utility Classes
- Bootstrap has ultility classes (styling you can apply to your HTML elements via ```class```) to quickly style elements without having to write your own CSS code.
- See full explanation and examples here: https://www.w3schools.com/bootstrap4/bootstrap_utilities.asp.
- There are a TON of utility classes for different components like buttons, texts, images, etc.
- For example, Bootstrap already has utility classes so you can easily align your text to the left, right, center, etc. so you don't have to write that CSS code yourself.
- Full list of utility classes [here](https://getbootstrap.com/docs/4.0/utilities/text/).
- “Stacking” utility classes common in Bootstrap; it is not unusual for an element to have 4 or 5 different utility classes to fully specify its appearance.

### Responsive Design
- Bootstrap supports mobile-first responsive webpages.
- Utility classes were designed to respond to device screen size.
- See the responsive breakpoints [here](https://getbootstrap.com/docs/4.0/layout/overview/#responsive-breakpoints).
- Note that size specifications, ```sm```, ```md```, etc. are "greater than or equal". So a responsive utility that applies to a ```md``` also applies to a ```lg``` screen.
- For example: ```float-left ``` class will cause an element to float to the left on any sized screen (it has no size specification). On the other hand, the ```float-md-left``` class will cause the element to float only on medium or larger screens.

### The Grid
- [Bootstrap Grid System](https://getbootstrap.com/docs/4.0/layout/grid/) allows you to specify complex multi-column layouts to add more structure to your website without having to implement your own Flexbox code.
- A typical Boostrap grid has this structure:
```html
<div class="container"> <!-- container for the grid -->
    <div class="row"> <!-- a row of items -->
        <div class="col-6">Item 1</div>
        <div class="col-4">Item 2</div>
        <div class="col">Item 3</div>
    </div>
</div>
```
> Note: you have to match class names exactly since you are using Bootstrap's CSS file to gain access to styling!
- A ```container``` houses ```row```s which houses ```col```s that have yout HTML elements.
- There can only be 12 columns in any row.
- So you if you had an HTML element that is 6 columns wide and had a second HTML element that is 7 columns wide, the second one would wrap under the first HTML element.

### Components
- Bootstrap provides a number of CSS classes that let you easily create more complex components or widgets: alerts, cards, navbars, collapsible boxes, image carousels, pop-up modals, and more. 
- Explore the documentation [here](https://getbootstrap.com/docs/4.0/components/buttons/) to see full list of components you can use!
- Most components have some sort of interactivity - which requires JavaScript.
- You will need to import the Bootsrap JavaScript library as well its two depedencies in your HTML:
```html
<!-- dependency: jQuery -->
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"></script>
<!-- dependency: popper -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.0/umd/popper.min.js"></script>

<!-- the Bootstrap JavaScript library -->
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/js/bootstrap.min.js"></script>
```