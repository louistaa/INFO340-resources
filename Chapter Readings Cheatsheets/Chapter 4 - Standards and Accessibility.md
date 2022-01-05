# Chapter 4 Standards and Accessibility
- Accessibility: your web pages can be used by everyone, regardless of web browser or physical abilities.

## Web Standards
- Web Standards are agreed-upon specifications for how web page source code should be rendered by the browser.
- Standards details how the language should be written so that it can be understood by any browser that follows the respective standard.
- Since you want to have your webpage be able to render across all browsers, standards give your code requirements so that they render correctly.

### Current Standard Versions
- HTML5 is the current living standard for HTML code.
- CSS3 is the current living standard for CSS code.
- ES6 is the current living standard for JavaScript code.

> You'll notice that some browser versions (usually older) won't support newer standards. You can check a browser's compatability with web standards [here](https://caniuse.com/?search=es6).

## Why Accessibility
- Many different disabilities that affect whether a person can access a web page, including:
    1. Vision Impairments
    2. Motor Impairments
    3. Cognitive Impairments
- If you fail to make your website accessible, you are locking above users and more, reducing the availability and use of your site. 
- Supporting users with disabilities is the law.
- It is not uncommon for large companies to be sued for discrimination if their websites are not accessible or ADA compliant.
- Making your website more accessible will make it more usable for everyone.
    1. If you support people who can’t see, then you may also support people who can’t see right now (e.g., because of a bad glare on their screen).
    2. If you support people with motor impairments, then you may also support people trying to use your website without a mouse (e.g., from a laptop while on a bumpy bus).
    3. If you support people with cognitive impairments, then you may also support people who are temporarily impaired (e.g., inebriated or lacking sleep).
- If your web page is well-structured and navigable with screen readers, it will guarentee it will be navigable by other machines like search engine indexers.

## Supporting Accessibility
- A screen reader is a piece of software that reads content on a computer's screen outloud.

### Semantic HTML
- Make sure your use of HTML is to describe the meaning or form of content, not to give that content a visual appearance.
- For example, don't use a ```<h1>``` tag for its appearance - use CSS instead. It will not make your page accessible as you are suggesting something is a title when in fact it's not.
- If something is supposed to be a top-level heading, you need to tag it as such for the screen reader to understand that.
- If you ever need to italicize text, use ```<em>``` instead as it is more semantically meaningful.
    - ```<i>``` tag has no valuable semantic meaning (it just means “italic”, or “different”).

### ARIA
- [Accessible Rich Internet Applications](https://www.w3.org/TR/wai-aria/): web standard for supporting accessibility.
- ARIA defines additional HTML attributes that can be included in elements in order to provide additional support for screen readers.
- For example, the ```role``` attribute allows non-semantic elements, such as a ```<div>``` to specify their semantic purpose.
- For example, if you had a ```<div>``` styled to look like a button, you can tell the screen reader with the ```role``` attribute that it is a button.
    - Remember, ```role```s have a preset list. Full list can be found [here](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques).

## Page Structure (Navigable)
- Accessible pages need to be explicitly structured so content can be easily navigated.
- Use of heading elements (```<h1>, <h2>```) can achieve this.
- Screen readers automatically generate a “table of contents” based on these headings, allowing users to easily move through large amounts of content.
- In order to ensure that the headings are useful, they need to be:
    1. Meaningful (actually marking section headings).
    2. Hierarchical (they don’t skip levels: every ```<h3>```has an ```<h2>``` above it).

## Visual Information (Perceivable)
- To make web pages accessible, screen readers need a way to perceive and correctly interpret such content.
- In order to make images accessible, you should always include an ```alt``` attribute that gives alternate text for when the images cannot be displayed (e.g., on screen readers, but also if the image fails to load):
```html
<img src="baby_picture.jpg" alt="a cute baby">
```
- Your ```alt``` text should always be "a {name of object}", as screen readers will already report that something is an image.
- Some images (or other elements) are purely decorative: company logos, icons that accompany text descriptions on buttons, etc.
- You can cause a screen reader to “skip” these elements by using an ARIA attribute ```aria-hidden```. 
- The element will still appear on the page, it just will be ignored by screen readers.
```html
<!-- The image on the button will not be read, but still displayed -->
<button><img src="search_icon.png" aria-hidden="true">Search</button>
```
- If you want to provide an equivalent to an alt attribute for elements other than <img>, such as a <div> that is styled in a purely visual way, use the ```aria-label``` attribute.
- ```aria-label``` acts like the ```alt``` attribute for any element, specifying what text should be read in place of the normal content.
```html
<div class="green-rect" aria-label="a giant green rectangle"></div>
```