# Chapter 8 Responsive CSS
- Today, people are accessing websites from many different devices: phones, tablets, laptops, desktops, etc.
- All of these devices have different screen sizes.
- **Q:** How do you build one site that looks good and works well on both tiny phones and gigantic desktop monitors?
- **A:** Responsive Web Design, which uses CSS to specify flexible layouts that will adjust to the size of the display.

## Mobile-First Design
- Websites are more likely to be visited on mobile devices nowadays.
- Mobile-first design: developing a website for mobile devices first.
    - Mobile screens are the most restricted in terms of screen size, capabailites, etc.
    - Only once a primary mobile version of your website has been built out, you can add features so it looks good on larger devices.

> Rather than viewing mobile devices as "losing" features, look at desktops as "gaining" features.

- Using 'toggle device tool bar' in your Developer Tools will allow you to see what a website looks on different devices.

### Mobile-First Design Principles
1. Layout: Blocks of content should on stack of each other. As device widths increase, you can put content side by side to help with readability.
2. Media: Small screens don't have enough space for very high-resolution media nor do phones typically have high bandwidth to do so either. Save your higher-resolution media for desktops, which usually have higher bandwidth available for downloading (i.e. user is at home connected to the internet vs. on LTE or 5G).
3. Fonts: Make sure to use a large enough font that is it readable on small screens, but don't make font too big so that you lose space for content.
    - Make sure to use relative units!
4. Navigation: Site navigation links (typically on the top) take up a lot of room on small screens so you'll notice majority of mobile versions of websites have a [hamburger menu](https://techcrunch.com/2014/05/24/before-the-hamburger-button-kills-you/).
5. Input and Interaction: Tap/click targets need to be large-enough on mobile to select using a finger. Tiny icons or one-word hyperlinks are difficult to selected accurately.
6. Content: You may even consider adjusting what content is shown to mobile users. Some text that would normally be on desktops may be an icon for smaller devices.

### Specifying Viewport
- Mobile web browsers will do some work on their own to adjust the web page in response to screen size—primarily by “shrinking” the content to fit. 
    - This often produces the effect of the website being “zoomed out” (which doesn't look good).
-  While it may “work” it is not an ideal user interaction.
- To fix this you'll need to explicitly state the viewport size and scale by adding the following ```<meta>``` tag:

```html
<head>
  <meta charset="utf-8"> <!-- always need this -->
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <!-- more head elements, including <link> ... -->
</head>
```
- ```content="width=device-width```: width of webpage will match width of device.
- ```initial-scale=1```: initial zoom on page is 100% (not zoomed in or zoomed out).
- ```shrink-to-fit=no```: do not shrink content to fit.

## Media Queries
- To create a webpage with responsive appearance, you'll need to conditionally change the applied style rules depending on the size of the screen/browser.
- Media queries: conditionally apply CSS rul    es.
    - Like an ```if``` statement for CSS: specifies rules that should apply when a condition is true.

### Syntax
```css
/* A normal CSS rule, will apply to all screen sizes */
body {
    font-size: 14px;
}

/* A Media Query */
@media (min-width: 768px)
{
    /* these rules apply ONLY on screens 768px and wider */

    /* a normal CSS rule */
    body {
        font-size: 18px;
        background-color: beige;
    }
    /* another CSS rule */
    .mobile-call-icon {
        display: none; /* don't show on large displays */
    }
}
```
- Written started with ```@media``` followed by an expression that must be true inside ```( )```.
- Inside the expression, you specify either:
    1. ```min-width``` to represent if ```width > x```.
    2. ```max-width``` to represent if ```width < x```.
- ```min-width: 1000px``` can be read as “width greater than or equal to 1000px”.
- ```@media``` is followed by ```{ }``` which contain CSS rules.
- These rules will only be applied if ```@media``` rule is true.
- Media queries follow the same ordering behavior as other CSS rules: the last rule on the page wins. 
- This means that media queries can be used to specify conditional rules that will override more “general rules”.
- Following a mobile-first approach, this means that your “normal” CSS should define the styling for a the page on a mobile device. 
- Media queries can then be used to add successive sets of rules that will “replace” the mobile styling with properties specific to larger displays:
```css
/* on small mobile devices, the header has a purple background */
header {
    font-size: 1.2rem;
    background-color: mediumpurple;
}

/* on 768px OR LARGER displays */
@media (min-width: 768px) {
    header {
        font-size: 1.5rem; /* make the header larger font on larger displays */
    }
}

/* on 992px OR LARGER displays */
@media (min-width: 992px) {
    header {
        background-image: url('../img/banner.png') /* use background image */
    }
}
```
