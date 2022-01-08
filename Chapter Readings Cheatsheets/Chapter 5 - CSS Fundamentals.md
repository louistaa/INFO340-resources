# Chapter 5 CSS Fundamentals
- CSS (Cascading Style Sheets) is a declarative language used to alter the appearance or styling of a web page.

> A declarative programming lanugage instructs a program on what needs to be done, instead of telling it how to do it.

- CSS defines a set of formatting rules, which the browser applies when it displays your page.
- You can control every aspect of an HTML element's appearance, including its placement on the page.

## Why Two Different Languages?
- **Q:** Why there are two different languages: HTML for your page content and CSS for formatting rules?
- **A:** Keep data (content) separate from presentation (appearance).
- By separating content (the HTML) from its appearance (the CSS), you get a number of benefits:
    1. The same content can easily be presented in different ways. Allows the user to choose different “themes” for a site (i.e. dark mode).
    2. Your HTML files can share the same CSS stylesheet, allowing you to change the appearance of your entire website by editing one shared file.
    3. Users who don’t care about about the visual appearance can more quickly engage with the content without needing to determine what information is “content” and what is just “aesthetics”.
- In summary, keep your content (HTML) separate from the appearance (CSS).

## CSS Rules
- Possible to write CSS rules directly into HTML (and you'll see this a lot), the best practice is to create a separate CSS stylesheet file and connect it to your HTML content.
> You'll see people online use ```style``` attribute to create styling rules in HTML for individual elements. You'll see how quickly this makes HTML code unreadable in addition to making your webpage unaccessible. 
>
> You can can also include CSS code directly into your HTML using a ```<style>``` tag, but this is also bad practice.
- CSS files end with the ```.css``` extension and are put in a ```css/``` folder in your project directory.
- Your project directory should have the following structure:
```code
my-project/
|-- css/
   |-- style.css
|-- index.html
```
- Your ```.css``` file will be typically named: ```style.css```, ```main.css``` or ```index.css```.
- You connect your stylesheet to your HTML file by adding a <link> element to your page’s <head> element:
```html
<head>
  <!--... other metadata elements here...-->
  <link rel="stylesheet" href="css/style.css">
</head>
```
- The ```<link>``` element represents a connection to another resource.
- The ```rel``` attribute indicates the relation between the resources (i.e the linked file is a stylesheet).
- The ```href``` attribute takes in a relative path from the ```.html``` file to the ```.css``` file.
- ```<link>``` element is an empty element so it doesn't require a closing tag.

## Overall Syntax
- CSS uses the following synax:
```css
selector {
   property: value;
}
```
- The selector specifies which elements the rule applies to, followed by a pair of curly braces {}.
- Inside the curly braces are a set of formatting properties in a key-value pair format.
- Properties are made up of the property name (like ```color```), followed by a colon, followed by a value for that property (like ```purple```).
- Each name-value property pair must end with a semi-colon.
- Comments in CSS use block-comment syntax:
```css
/* This is a comment in CSS */
```
- Putting it all together:
```css
/* Any h1 will have Helvetica font, appear white and be on a dark gray background */
h1 {
  font-family: 'Helvetica';
  color: white;
  background-color: #333; /* dark gray */
}
```
## CSS Properties
- Comprehensive list of CSS properties [here](https://www.w3schools.com/cssref/default.asp).
    - All of them use the ```name:value``` syntax.

## CSS Selectors
- Selectors are used to pick which HTML elements the CSS rule should apply to.
- Comprehensive list of CSS Selectors [here](https://www.w3schools.com/cssref/css_selectors.asp).
- The three most common CSS Selectors are:
    1. Element Selector
    2. Class Selector
    3. Id Selector

### Element Selector
- The most basic selector, the element selector selects elements by their element (tag) name.
- You can apply formatting rules to the entire page by selecting the ```<body>``` element.

> Do not apply formatting to the ```<html>``` element for clarity and speed purposes.
- For example:
```css
p {
   color: purple;
}
```
- Would style all ```<p>``` elements to be the color purple.

### Class Selector
- The class selector selects elements with a matching ```class``` HTML attribute.
- In HTML, you can give any element a ```class``` attribute, which you can specify any name to classify that element as.
> I have only ever seen the ```class``` attribute be used for CSS reasons.
- Written using a period/single dot preceding the name of the class you specified.
- If you wanted to highlight some text, you could specify a ```class``` name of ```"highlighted"``` (or whatever is appropriate):
```html
<!-- HTML -->
<p class="highlighted">This text is highlighted!</p>
```
- And then create the styling link using CSS:
```css
/* CSS */
.highlighted {
   background-color: yellow;
}
```
- Notice how the ```"highlighted"``` class in HTML matches the ```"highlighted"``` selector in CSS.
> Again, ```class``` names are whatever you give it. Make sure they are precise and concise.

- Different elements can have the same class name, which allows for CSS code reuse.
```html
<h1 class="alert-flashing">I am a flashing alert!</h1>
<p class="alert-flashing">So am I!<p>
```
- HTML elements can have multiple class names seperated by a space:
```html
<p class="alert flashing">I have TWO classes: "alert" and "flashing"</p>
<p class="alert-flashing">I have ONE class: "alert-flashing"</p>
```
- So the first ```<p>``` will have styling rules specified by your ```alert``` and ```flashing``` CSS selectors.
- More information about the ```class``` attribute [here](https://www.w3schools.com/html/html_classes.asp).

### Id Selector
- The Id selector selects elements with a matching ```id``` HTML attribute.
- In HTML, you can give any element an ```id``` attribute, which you can specify any name to tag it.
    - But each ```id``` must be unique (unlike ```class```).
> No two elements can have the same value for their ```id``` attributes. 
```html
<div id="sidebar">
   This div contains the sidebar for the page
</div>
```
- Id selectors start with a hashtag, followed by the value of the id:
```css
#sidebar {
    background-color: lightgray;
}
```
- Notice how the ```"sidebar"``` id in HTML matches the ```"sidebar"``` selector in CSS.
> Again, ```id``` names are whatever you give it. Make sure they are precise and concise.
- Using ```id``` tags makes your CSS code harder to "reuse" (as only one rule can be applied for one element).
- Thus you should almost always use a class selector instead of an id selector!
- Only exception is unless you are referring to a single, specific element.
    - Example: Navigation bar or footer.

## The Cascade
- CSS is called Cascading Style Sheets because multiple rules can apply to the same element (in a “cascade” of style).
- CSS rules are additive, meaning if multiple rules apply to the same element, the browser will combine all of the styling properties.
- Considering the following CSS rules:
```css
/* CSS */
p { /* applies to all paragraphs */
  font-family: 'Helvetica'
}

.alert { /* applies to all elements with class="alert" */
  font-size: larger;
}

.success { /* applies to all elements with class="success" */
  color: #28a745; /* a pleasant green */
}
```
- Then consider the following HTML:
```html
<!-- HTML -->
<p class="alert success">
  This paragraph will be in Helvetica font, a larger font-size, and green color, because all 3 of the above rules apply to it.
</p>
```
### Inherited properties
- CSS styling applies to all content in an element.
- Since that content can be other HTML elements, those child elements may inherit styling rules.
- Considering the following:
```html
<div class="content"> <!-- has own styling -->
  <div class="sub-sec"> <!-- has own styling + .content styling -->
    <ol class="demo-list"> <!-- own styling (ol AND .demo-list rules) + .sub-sec + .content -->

      <!-- li styling + .demo-list + .sub-sec + .content -->
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ol>
  </div>
</div>
```
- In general, set CSS rules to the highest-level element you can to maximize code-reuse.
- More on inherited properties [here](https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance#inherited_properties).

## Rule Specificity
- Rules are applied in the order they are defined in the CSS file.
- If you link multiple CSS files from the same HTML page, the files are processed in order as they are linked in the HTML.
- When the browser is processing a CSS file, it selects elements that match the rule and applies the rule's property.
- If a later rule selects the same element and applies a different value to that property, the previous one is overriden.
> This is why if you ever link an external CSS file, you must link it before yours. Or else, your CSS rules may get overriden if you so happen to select the same elements.
For example:
```css
/* Two rules, both alike in specificity */
p { color: red; }
p { color: blue; }
```
```html
<p>This text will be blue, because that rule comes last!</p>
```
- In addition, more specific selectors take precedence specific ones.
    1. ```#id``` is the most specific
    2. ```.class``` is the second most specific
    3. ```tag``` is the least specfic
- Thus, the CSS rule that comes last and is most specfic will be the one to take effect.
- More on CSS specificity [here](https://css-tricks.com/specifics-on-css-specificity/).
> Precedence rules are not a reason to prefer #id selectors over .class selectors! Instead, you can utilize the [compound selectors](https://info340.github.io/css-options.html#compound-selectors) described in Chapter 6 to be able to create reusable rules and avoid duplicating property declarations.