# Chapter 6 CSS Options
- More details about additional selectors and properties to use when defining CSS rules.

## Compound Selectors
- You can combine element, class and id selectors to specify more complex styling rules.

### Group Selector
- Group selector allows for a single rule to apply to multiple elements that are matched by many different selectors.
- Separate each selector with a comma.
    - You can use any selector in the comma-separated list.
- For example:
```css
/* applies to h1, h2, AND h3 tags */
h1, h2, h3 {
    font-family: Helvetica;
    color: #4b2e83; /* UW purple */
}
```
- Above code will style all ```h1```,```h2```,```h3``` tags to the same ```font-family``` and ```color```.

### Combined Selectors
- You can combine element, class and id selectors to be more specific about what rule applies.
- You do this by putting one selector immediately after the previous selector, with no spaces.
- Some examples include the following:
```css
/* Selects only p elements that have class="alert"
   Other p elements and "alert" classed elements not affected */
p.alert {
  color: red;
}

/* Selects only h1 elements that have id="title" */
/* Note that this is redundant, since only one element can have the id! */
h1#title {
  color: purple;
}

/* Selects elements that have class "alert" AND class "success" */
.alert.success {
  color: green;
  font-size: larger;
}

/* And can combine with group selector */
/* applies to <p class="highlighted"> and <li class="selected"> */
p.highlighted, li.marked {
  background-color: yellow;
}
```
### Descendant Selector
- The descendant selector is a way to select elements that are located anywhere underneath other elements.
    - The element doesn't have to be a direct child.
- Written using a blank space in between selectors.
- For example consider the following HTML code:
```html
<header>
   <h1>Welcome to the page</h1>
   <p>I am a special paragraph</p>
</header>
<section>
   <p>some other paragraph</p>
</section>
```
- Then consider the following CSS code:
```css
/*
  Selects p elements that exist within header elements
  Other p elements will not be affected
 */
header p {
    /* ... */
}
```
- Above will only style the ```<p>```s that are a descendant (children element) of a ```<header>```.
- If you only want to select direct children, you can use the ```>``` instead of the blank space.
```css
body > p {
  color: blue;
}
```
- The above will only style the ```<p>``` that is directly below the ```<body>``` element.

### Pseudo-classes
- Pseudo-classes select elements based on what the state the element is in.
    - For example: if the element is being hovered on, or if the link is active etc.
- Pseudo-classes are written by placing a colon (:) and the name of the pseudo-class immediately after.
- Some common pseudo-classes:
```css
/* style for unvisited links */
a:link { /*...*/ }

/* style for visited links */
a:visited { /*...*/ }

/* style for links the user is hovering over with the mouse */
a:hover { /*...*/ }

/* style for links that have keyboard focus */
a:focus { /*...*/ }

/* style for links as they are being 'activated' (clicked) */
a:active { /*...*/ }
```
- Comprehensive list of pseudo-classes [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

#### nth-* Selectors
- ```nth-child``` and ```nth-of-type``` selectors allow you to select specific elements based on their position in the DOM.
- For example, you may want each third ```<li>``` element in a list to have a certain style:
```css
/* Get third li element  */
li:nth-of-type(3) {
  color:red;
}
```

### Attribute Selectors
- Select elements with a particular matching HTML attribute.
- Uses square brackets right after the selector.
    - Inside the square brackets you put the attribute you want to match for.
```css
/* select all p elements whose "lang=sp" */
p[lang="sp"] {
    color: red;
    background-color: orange;
}
```
- You can also partially match values, see [this](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors) resource for more details.

## Property Values
- More on the possible values that may be assigned to properties in CSS.

### Units & Sizes
- Many CSS properties affect the size of your HTML elements and there exist many different units to specify those sizes.

#### Absolute Units
- Absolute units make HTML elements a fixed sized.

1. ```cm```: centimeters
2. ```mm```: millimeters
3. ```in```: inches (1in = 96px = 2.54cm)
4. ```px```: pixels (1px = 1/96th of 1in)
5. ```pt```: points (1pt = 1/72 of 1in)
6. ```pc```: picas (1pc = 12 pt)

> Absolute units are not recommended for use on screen because screen sizes vary so much. However, if the viewport size is known (like print layout), then absolute units would be appropriate.
- Absolute units are best for things that do not scale across devices (e.g., image sizes, or the maximum width of content).

#### Relative Units
- Relative units make HTML elements sized based on other elements.

1. ```em```: relative to the font-size of the element (2em means 2 times the size of the current font)
2. ```rem```: relative to font-size of the root element (the ```font-size``` of the root ```html``` or ```body``` element)
3. ```%```: relative to the parent element’s font-size or dimension
4. ```vw, vh```: relative to 1% of the width/height of the viewport

- Note that most browsers have a default font size of 16px, so 1em and 1rem will both be initially equivalent to 16px.
- You should specify font sizes using relative units as it supports accessibility.
- Vision-impaired users will be able to increase the default font-size of the browser and all your text will adjust appropriately.

> Relative units scale better across different screen sizes, hence it is always preferred to use them over absolute units.

> Font-sizes should always be relative; layout dimensions may be absolute (but relative units are best).
- More on absolute and relative units [here](https://www.w3schools.com/cssref/css_units.asp).

### Colors
- Colors in CSS can be specified in a few different ways.

#### Predefined Colors
- There exists 140 predefined color names you can use [here](https://www.w3schools.com/colors/colors_names.asp).
- Useful for placeholders and starting points for design.
- Example usage:
```css
p {
   color: mediumpurple;
}
```
#### red-green-blue(RGB)
- Way of representing color that results when specified amount of red, green and blue light are aimed at a white background. 
- The value option is a function that takes in three parameters, representing the amount of red, green and blue.
    - Each parameter ranges from 0 to 255.
- An optional forth parameter can specify the transparency.
- ```rbg``` function documentation [here](https://www.w3schools.com/css/css_colors_rgb.asp).
- Example usage:
```css
p {
   color: rgb(147, 112, 219); /* medium purple */
}
```
#### Hexcodes
- Most common way of expressing color is with a hexadecimal number.
- The color starts with a hashtag.
- The first two characters represent the red, the next two the green, and then the last two the blue.
```css
p {
   color: #9370db; /* medium purple */
}
```
- All you need to know is that hexcodes will always be a six digit value.
- More on hexcodes and hexadecimals [here](https://www.smashingmagazine.com/2012/10/the-code-side-of-color/).

## Fonts and Icons
- ```font-family``` takes in a comma-separated list of fonts to use.
- The browser will use the first one. If that one is not available (perhaps its new or obscure) then it will use the following one in the list. 
- The last font should always be a generic family name (a category of font).
- The most common generic families are serif and sans-serif font.

### External Resources
- You can import custom fonts easily from [Google Fonts](https://fonts.google.com/).
    - Directions on how to import a Google Font [here](https://www.freecodecamp.org/news/how-to-use-google-fonts-in-your-next-web-design-project-e1ad48f1adfa/).
- Most popular icon library/set is [Font Awesome](https://fontawesome.com/).
    - You'll need to load the icon set from a Content Delivery Network (CDN).
    - [Sign up](https://fontawesome.com/start) for a Font Awesome account to get access to your link to start using the icons!
- You'll notice that Font Awesome uses ```<i>``` tags.
    - Because the icon has no semantic meaning beyond an appearance, it is often included with a semantically-deficient (empty) ```<i>``` element. Remember to include an aria-hidden attribute so that a screen-reader won’t try to read the strange letter!

## Backgrounds and Images
- ```background-image```: allows you to set an image as the background of an element.
- Example usage:
```css
header {
    background-image: url('../img/page-banner.png');
}
```
- This property takes as a value a [url()](https://developer.mozilla.org/en-US/docs/Web/CSS/url()) data type, which is written like a function whose parameter is a string with the URI of the resource to load. 
    - These URIs can be absolute (e.g., http://...), or relative to the location of the **stylesheet**.
- Full list of background image properties [here](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders).
