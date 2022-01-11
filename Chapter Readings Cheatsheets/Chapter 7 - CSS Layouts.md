# Chapter 7 CSS Layouts
- How to use CSS to declare where HTML elements should appear on the webpage.
> This is suprisingly difficult.
- Elements are arranged from the top left corner of the page.
- Three facets control the position of an HTML element:
    1. Display: determines how elements share horizontal space.
    2. Position: allows you to specify the type of positioning method used for an element
    3. Box-model: describes the amount of 2D space taken up by an element.

## Display
- You can force an element to be either ```block``` or ```inline``` by declaring the ```display``` CSS property:
```css
.inlined {
  display: inline;
}
```
- You can set this property to ```none``` to remove the element from the page.
- ```display``` documentation [here](https://developer.mozilla.org/en-US/docs/Web/CSS/display).

> Primary use of ```display``` is to set whether an element is treated as a block or inline element, and the layout used for its children elements in flexbox (more details in a sec).

## The Box Model
- The CSS box model is essentially a box that wraps around every HTML element.
- The box consists of:
    1. Margins: clears an area outside the border.
        - This is the space between boxes.
    2. Borders: border that goes aroudn the padding and content.
    3. Padding: clears an area around the content.
        - This is the space between the content and the border.
    4. Content: where text and images appear.

### Padding
- You can specify padding for an element in a few ways:
```css
/* specify each side individually */
div {
  padding-top: 1em;
  padding-bottom: 1em;
  padding-left: 2em;
  padding-right: 0; /* no units needed on 0 */
}

/* specify one value for all sides at once */
div {
  padding: 1.5em;
}

/* specify one value for top/bottom (first)
   and one for left/right (second) */
div {
  padding: 1em 2em;
}
```

### Border
- You can style the border in a few ways:
```css
.boxed {
   border: 2px dashed black; /* border on all sides */
}

.underlined {
   border-bottom: 1px solid red; /* border one side */
}

.something { /* control border properties separately */
   border-top-width: 4px;
   border-top-color: blue;
   border-top-style: dotted;
   border-radius: 4px; /* rounded corners! */
}
```
> Margin and padding will be your bestfriend in spacing out content!

### Box-Sizing
- The ```box-sizing``` CSS property sets how the total width and height of an element is calculated.
- By default, the ```width``` and ```height``` you assign to an element is applied only to the element's content box.
- If the element has any ```border``` or ```padding```, this is then added to the ```width``` and ```height``` to arrive at the size of the box that's rendered on the screen.
- This means that when you set ```width``` and ```height```, you have to adjust the value you give to allow for any border or padding that may be added.
- For example, if you have four boxes with ```width: 25%;```, if any has left or right padding or a left or right border, they will not by default fit on one line within the constraints of the parent container.
- ```box-sizing: border-box;```: tells the browser to account for any border and padding in the values you specify for an element's width and height. 
    - If you set an element's width to 100 pixels, that 100 pixels will include any border or padding you added, and the content box will shrink to absorb that extra width. 
    - This typically makes it much easier to size elements!
- This property is so common that you want to apply to all elements of the page and you should include the following line in all your CSS files going forward:
```css
* {
    box-sizing: border-box; /* all elements include border and padding in size */
}
```
- More content about box-sizing [here](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing).

### Position
- Depending on the ```position``` property, you can shift the location of elements using the ```top```, ```bottom```, ```left```, and ```right``` properties. There are five (book says four) values that the position property can be set to.

#### static
- HTML elements are positioned static by default.
- Any element positioned this way is always positioned according to the normal flow of the page.
```css
/* This <div> has no special positioning */
div.static {
  position: static;
}
```

#### relative
- Positioned relative to its normal position.
- Setting the ```top```, ```bottom```, ```left```, and ```right``` properties of a relatively-positioned element will cause it to be adjusted away from its normal position.
```css
/* This <div> will be shifted 30px relative to its normal positioning */
div.relative {
  position: relative;
  left: 30px;
}
```
#### fixed
- Positioned relative to the viewport, meaning it will always stay in the same place even if the page is scrolled.
- The ```top```, ```bottom```, ```left```, and ```right``` properties are used to position a ```fixed``` element.
```css
/* This <div> will be fixed to the bottom right */
div.fixed {
  position: fixed;
  bottom: 0;
  right: 0;
}
```

> Most common use case for this is a footer!

#### absolute
- Positioned relative to the first positioned (non-static) ancestor.
- Allows you to specify where within a parent element you want an element to be positioned. 

```css
/* This <div> will be styled relative to its parent */
div.absolute {
  position: absolute;
  top: 80px;
  right: 0;
}
```

#### sticky
- Positioned based on the user's scroll position
- A sticky element toggles between ```relative``` and ```fixed```, depending on the scroll position. It is positioned ```relative``` until a given offset position is met in the viewport - then it "sticks" in place.

> Sticky elements aren't very common, to the point where Internet Explorer doesn't support them altogether. Probably why the book doesn't mention this.
- More on all the types of positioning [here](https://www.w3schools.com/css/css_positioning.asp).

## Floating
- CSS ```float``` property specifies where an element should float on the screen.

The float property can have one of the following values:
1. left: The element floats to the left of its container.
2. right: The element floats to the right of its container.
3. none: The element does not float (will be displayed just where it occurs in the text). This is default.
4. inherit: The element inherits the float value of its parent.
- More on ```float``` [here](https://www.w3schools.com/css/css_float.asp).

## Flexbox
- Great resource on Flexbox [here](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
- Flexbox allows you to lay out elements inside a container so that the space is flexibly distributed amongst your HTML elements.
- To get started, you'll need to create two CSS classes: one of the container (parent element) and one of the child elements (the items in the container).
- Below demostrates the common naming convention for the parent and child elements:
```html
<div class="flex-container"> <!-- Parent -->
  <div class="flex-item">Child 1</div>
  <div class="flex-item">Child 2</div>
  <div class="flex-item">Child 3</div>
</div>
```
> You can call these classes whatever you want, as long as it has the neccessary styling rules below.
- Then, give the parent element the following property:
```css
/* parent element only */
.flex-container { /* my flexbox container class */
    display: flex;
}
```
- This will cause the contents of the container (the parent element) to be layed out according to a "flex flow".
    - A flex flow will lay out items horizontally.
- Then we can use multiple properties to decide how the items in the container (child HTML elements) should be layed out within the container.

```css
* { box-sizing: border-box; } /* recommended for item sizing */

/* child elements only */
.flex-item {
    flex-grow: 1; /* get 1 share of extra space */
    flex-shrink: 0; /* do not shrink if items overflow container */
    flex-basis: 33%; /* take up 33% of parent initially */
}
```
- ```flex-grow``` specifies what “share” or ratio of any extra space in the container the item should take up.
    - You can give each item a property ```flex-grow: 1``` to have them take up an equal amount of space in the container.
- ```flex-shrink``` works similar to flex-grow, but in reverse. It takes as a value a number (default to 1), which determine what “share” or ratio it should shrink by in order to accommodate any overflow space.
- ```flex-basis``` allows you to specify the “initial” dimensions of a particular item.

> Honestly, you just practice adjusting values to learn how Flexbox works. You'll faster this way than reading the book / documentation!
- There is also a shortcut property ```flex``` that allows you to specify all three values at once: give the ```flex-grow```, ```flex-shrink```, and ```flex-basis``` values separated by spaces (the second two being optional if you want to use the default values).