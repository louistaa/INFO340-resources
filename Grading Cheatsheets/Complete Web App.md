# Complete Web App
- 15 points possible
- Weights calculated on March 9th, 2022. Subject to change.

## App Content and HTML Structure (2.25 points)
1. Project built using create-react-app in the root of the repo. Cleaned up extraneous files
2. Specified meta data in HTML (title, author, description, and own favicon)
3. Has sufficient content (about "2 web pages" worth)
4. Includes header element (with app name) and footer (with copyright) elements
5. Includes multiple separate and meaningful views of the data
6. Includes 2+ images or media content
7. Includes a form element

## React Components and Structure (2.25 points)
1. App is broken up into a meaningful component hierarchy; each component reflects a "part" of the page
2. Components are appropriately sized/scoped (e.g., 2-3 DOM levels each)
3. Components are defined as self-contained entities
4. Data is passed through the app via props to components; props and state are appropriately distinguished.
5. Content is only rendered on through components—no DOM calls!
    - No use of ```document``` object or jQuery.

## React Interactivity (3.75 points)
1. App has 2+ interactive features (3+ for larger groups).
    - Features involve new, project-specific code
    - Features are complete user interactions
    - Features are unified
2. Features are interactive and state-based.
    - Has different user inputs (one of which is a form)
    - App respond to user actions/events
    - Interactions both read and write to state variables
    - Interactions are visible in the page (not just console log); they change displayed content depending on user input
3. State information is stored at appropriate levels (in the "lowest common ancestor")
4. Interaction is pleasant and frictionless:
    - Interactions are discoverable (include instructions)
    - Interactions provide feedback, including on errors—particularly for Firebase

## Client-Side Routing and Navigation (.75 points)
1. Correctly integrates react-router (specifying ```<Route>```s, ```<Link>```s, etc)
2. Includes sufficient number of routes (3+)
3. Includes 1 route with a path parameter
4. Handles incorrect URLs effectively

## Integrates Another React Library (.75 points)
1. Project imports another library
2. App imports external components
3. App renders imported component
4. App does not mix library and non-library versions of elements (e.g., mixing Bootstrap with reactstrap).

## Using External Data (.75 points)
1. App accesses external data using an event hook
2. Sends an AJAX request for external data file
3. Uses Promises to handle asynchronous data loading
    - This includes writing to Firebase
4. Catches and manages (e.g., displays) errors from data loading
    - Use ```console.error()```
5. Loaded data is used in some way
6. Includes data source citation (if any)

## Site Style and CSS Structure (2.25 points)
1. Loads an external CSS style sheet
2. Stylesheet includes 20+ rules
3. CSS changes: colors, fonts/sizes, margins/padding
4. Uses flexbox or bootstrap grid for non-standard layout
5. Has a polished appearance: readable & navigable, consistent, clean
6. CSS files and libraries are imported through JavaScript

## Accessibility (.75 points)
1. Uses elements semantically (no ```<i>```; ```<a>``` for links, doesn't use ```<h1>``` for styling, etc.)
2. Correctly uses sectioning elements (```<main>```, ```<section>```, etc); not needed if no sections
3. Uses hierarchical headings; doesn't skip levels
4. Includes alt attributes on all images
5. Form includes ```<label>``` elements (with for attribute)
6. Includes aria-label and role attributes when necessary (and only when necessary!)

## Responsive Design (.75 points)
1. Specifies a viewport meta
    - In your HTML
2. Includes media queries to handle 2+ sizes
3. Mobile-first CSS: media queries at the bottom (modify the small-size default)
4. Styling changes on media and large screens
5. Layout is noticeably and meaningfully different on different screen sizes
6. Page content is polished on all screen sizes

## Clean Coding Style (.75 points)
1. Organized files in repo
    - Extraneous files removed, all pictures in imgs/ folder, components organized in folders if necessary.
2. Valid HTML
    - Uses ```.map()``` to create repeating DOM elements.
3. Well-designed CSS
    - Informative class names.
    - Ccomments group sets of rules.
4. Well-written JavaScript
    - Informative variable and function names.
    - Uses ```let``` and ```const``` instead of ```var```.
    - No ```console.log()``` statements.
5. Correct and idiomatic usage of React framework
    - Basically do you follow syntax?
6. Well-scoped and informatively-named function components and hooks
7. No ```.map()```/```filter()```, etc. inside a ```return```.
8. Well-commented code.
9. Running app doesn't produce any errors in the developer console. 