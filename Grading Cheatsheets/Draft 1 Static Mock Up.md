# Project: Draft 1 (Static Mock-Up)
- What I am looking for in each section of the rubric and what you will lose points for.

## Content and HTML Structure: 2 points possible
### Checklist point breakdown:
1. Inclues index.html file (named correctly, in the root folder): .1 point
2. index.html file is the "main page": .1 point
3. Includes second page: .2 points
4. Includes hyperlinks between two pages (in both directions!): .2 points
5. Both pages link in a single CSS file: .1 point
6. Includes meta elements in html head: author (main only), description (main only), favicon, title: .2 point
7. Includes header element (with app name) and footer (with copyright) elements: .1 point
8. Includes two separate and meaningful views of the data: .5 points
9. Includes 3+ images or media content: .3 points
10. Includes a form element: .2 points

### Common deduductions: 
- No favicon: -.1 point
- You want your meta description to describe what your page is about, not that it's the main page of your app -.1 point

## Site Style and CSS Structure: 3 points possible
### Checklist point breakdown:
1. Loads an external CSS style sheet: .1 point
2. Stylesheet includes sufficient number of rules (20+): .4 points 
3. CSS changes, colors, fonts/sizes, margins/padding: .5 points
4. Uses flexbox or grid for non-standard layout (via Bootstrap is fine): .5 points
5. Has a polished appearance: readable & navigable, consistent, clean: 1 points

### Common deduductions: 
- Overlapping HTML elements: -.4 points
- Incongruent sizes for like-elements (buttons, cards, pictures, etc.): -.5 points
- Incorrect use of flexbox/grid: -.3 points

## Accessibility: 1.5 points possible
### Checklist point breakdown:
1. Uses elements semantically (no ```<i>```, ```<a>``` for links, etc): .2 points
2. Correctly uses sectioning elements (```<section>```, etc); not needed if no sections: .2 points
3. Uses Hierarchical headings; doesn't skip levels: .1 points
4. Includes alt attributes on all images: .5 points
5. Form includes ```<label>``` elements (with for attribute): .3 points
6. Includes aria-label and role attributes when necessary (and only then): .2 points

### Common deduductions: 
- Just follow the checklist, then you are good.

## Responsive Design: 2 points possible
- Probably the hardest one to get right
- Grading starts at 375px wide (iPhone SE)

### Checklist point breakdown:
1. Specifies a viewport meta: .1 points
2. Includes media queries (2+ to handle 3 sizes): .1 points
3. Mobile-first CSS: media queries at the bottom (modify the small-size default): .4 points
4. Styling changes on media and large screens: .4 points
5. Layout is noticeably and meaningfully different on different screen sizes: .5 points
6. Page content is polished on all screen sizes: .5 points

### Common deduductions: 
- Media queries not on bottom -.2 points
- Lack of complexity in media queries. Consider changing text sizes and positioning of elements -.2 points
- Webite does not respond to very small viewports: everything gets squished to the left -.5 points
- HTML cut off on smaller viewports, HTML elements start overlapping -.3 points
- Under utilized whitespace -.1 points
- Website structure does not change very much on different viewports -.5 points
- Content gets cut off as viewport gets smaller (content doesn't resize) -.3 points
- HTML elements/text gets way too small on smaller viewports -.2 points, multiple elements: -.4 points

## Cleaning Coding Style (HTML/CSS): 1 point possible
- Remember to format ALL your files!

### Checklist point breakdown:
1. Organized files in repo: .1 points
2. Valid HTML: No invalid usage, No redundant elements, Clean and consistent indentation: .2 points
3. Well-designed CSS: Informative class names, Avoids id selectors, No inappropriate duplication of rules, Organized in file, with comments to "group" sets of rules: .2 points
4. Code passes included jest lint tests: .5 points

### Common deduductions: 
- CSS file is name something other than 'style.css' -.1 point
- Inconsistent spacing / identenation: -.1 point, -.2 points if both
- No / not enough comments on HTML/CSS: -.1 point / -.2 points if both
- Extraneous whitepsace on files -.1

## Published Site: .5 points possible
### Checklist point breakdown:
- Site is deployed to GitHub Pages: .5 points
