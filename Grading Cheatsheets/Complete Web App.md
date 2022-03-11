# Complete Web App
- 15 points possible
- Weights calculated on March 9th, 2022. Subject to change.

## App Content and HTML Structure (2.25 points)
1. Project built using create-react-app in the root of the repo. Cleaned up extraneous files: .15 points
2. Specified meta data in HTML (title, author, description, and own favicon): .1 point
3. Has sufficient content (about "2 web pages" worth): .4 points
4. Includes header element (with app name) and footer (with copyright) elements: .4 points
5. Includes multiple separate and meaningful views of the data: .4 points
6. Includes 2+ images or media content: .4 points
7. Includes a form element: .4 points

## React Components and Structure (2.25 points)
1. App is broken up into a meaningful component hierarchy; each component reflects a "part" of the page: .5 points
2. Components are appropriately sized/scoped (e.g., 2-3 DOM levels each): .5 points
3. Components are defined as self-contained entities: .25 points
4. Data is passed through the app via props to components; props and state are appropriately distinguished: .5 points
5. Content is only rendered on through components—no DOM calls!: .5 points
    - No use of ```document``` object or jQuery.

## React Interactivity (3.75 points)
1. App has 2+ interactive features (3+ for larger groups): 2 points
    - Features involve new, project-specific code
    - Features are complete user interactions
    - Features are unified
2. Features are interactive and state-based: .5 points
    - Has different user inputs (one of which is a form)
    - App respond to user actions/events
    - Interactions both read and write to state variables
    - Interactions are visible in the page (not just console log); they change displayed content depending on user input
3. State information is stored at appropriate levels (in the "lowest common ancestor"): .5 points
4. Interaction is pleasant and frictionless: .75 points
    - Interactions are discoverable (include instructions)
    - Interactions provide feedback, including on errors—particularly for Firebase

## Client-Side Routing and Navigation (.75 points)
1. Correctly integrates react-router (specifying ```<Route>```s, ```<Link>```s, etc): .15 points
2. Includes sufficient number of routes (3+): .2 points
3. Includes 1 route with a path parameter: .2 points
4. Handles incorrect URLs effectively: .2 points

## Integrates Another React Library (.75 points)
1. Project imports another library: .15 points
2. App imports external components: .2 points
3. App renders imported component: .2 points
4. App does not mix library and non-library versions of elements (e.g., mixing Bootstrap with reactstrap): .2 points

## Using External Data (.75 points)
1. App accesses external data using an event hook: .25 points
2. Sends an AJAX request for external data file: .1 points
3. Uses Promises to handle asynchronous data loading: .1 points
    - This includes writing to Firebase
4. Catches and manages (e.g., displays) errors from data loading: .1 points
    - Use ```console.error()```
5. Loaded data is used in some way: .1 points
6. Includes data source citation (if any): .1 points

## Site Style and CSS Structure (2.25 points)
1. Loads an external CSS style sheet: .25 points
2. Stylesheet includes 20+ rules: .4 points
3. CSS changes: colors, fonts/sizes, margins/padding: .4 points
4. Uses flexbox or bootstrap grid for non-standard layout: .4 points
5. Has a polished appearance: readable & navigable, consistent, clean: .4 points
6. CSS files and libraries are imported through JavaScript: .4 points

## Accessibility (.75 points)
1. Uses elements semantically (no ```<i>```; ```<a>``` for links, doesn't use ```<h1>``` for styling, etc.): .25 points
2. Correctly uses sectioning elements (```<main>```, ```<section>```, etc); not needed if no sections: .1 points
3. Uses hierarchical headings; doesn't skip levels: .1 points
4. Includes alt attributes on all images: .1 points
5. Form includes ```<label>``` elements (with for attribute): .1 points
6. Includes aria-label and role attributes when necessary (and only when necessary!): .1 points

## Responsive Design (.75 points)
1. Specifies a viewport meta: .1 points
    - In your HTML
2. Includes media queries to handle 2+ sizes: .1 points
3. Mobile-first CSS: media queries at the bottom (modify the small-size default): .05 points
4. Styling changes on media and large screens: .2 points
5. Layout is noticeably and meaningfully different on different screen sizes: .2 points
6. Page content is polished on all screen sizes: .1 points

## Clean Coding Style (.75 points)
1. Organized files in repo: .1 points
    - Extraneous files removed, all pictures in imgs/ folder, components organized in folders if necessary.
2. Valid HTML: .1 points
    - Uses ```.map()``` to create repeating DOM elements.
3. Well-designed CSS: .1 points
    - Informative class names.
    - Ccomments group sets of rules.
4. Well-written JavaScript: .1 points
    - Informative variable and function names.
    - Uses ```let``` and ```const``` instead of ```var```.
    - No ```console.log()``` statements.
5. Correct and idiomatic usage of React framework: .1 points
    - Well-scoped and informatively-named function components and hooks
    - No ```.map()```/```filter()```, etc. inside a ```return```
8. Well-commented code: .1 points
9. Running app doesn't produce any errors in the developer console: .25 points