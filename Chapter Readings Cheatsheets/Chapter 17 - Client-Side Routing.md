# Chapter 17 Client-Side Routing
- Single Page Applications (SPA) are web applications that are located on a single web page (HTML file), but DOM manipulation (and often AJAX requests) to produce the appearance of multiple “web pages”.
- This structure is facilitated by the use of the client-side routing library ```react-router```.

## Single-Page Applications
- With client-side routing, determining which View to display based on the URL (how to “route”, or map that URL to the correct resource) is performed on the client-side by JavaScript code.
> Google Drive is a good example of a Single-Page Application. Notice how if you navigate to a new folder, the URL changes (so you can link to individual folders), but only a single “pane” of the page changes.

## React-Router
- Install this library:
```bash
npm install react-router-dom
```
- You will then need to import any Components you wish to use into the .js files containing your React code:
```js
import { BrowserRouter, Routes, Route, Link} from 'react-router-dom'
```
- The ```<BrowserRouter>``` Component ) is the “base” Component used by React Router.
- The BrowserRouter “listens” for changes to the URL, and then passes information about the current route (called the path) to its child components. This allows each child to always know what route is currently shown in the URL, without needing to access the URL directly.
- With React Router, a “route” is defined by the path portion of a URI.
-  This is the part that comes after the protocol and domain (e.g., after the ```https://mydomain.com/```). Thus the /home route would refer to the URI ```https://mydomain.com/home```, while the /about route would refer to the URI ```https://mydomain.com/about```.
- Your app will only ever have a single ```<BrowserRouter>``` component in it–usually at the “top level” of your application (so it would contain ```<App>``` as a child). Thus the ```<BrowserRouter>``` is usually rendered in the index.html file:
```js
import { BrowserRouter } from 'react-router-dom'
import App from './components/App.js'

//render the App *inside* of the BrowserRouter
ReactDOM.render(<BrowserRouter><App /></BrowserRouter>, document.getElementById('root'));
```
- Inside the <BrowserRouter> (usually inside of the <App>), you will define the routes for your application—the collection of supported paths and which View to show at each.
- You can specify route-based views using the ```<Route>``` Component.
- This component will render its element only when the current URL matches a specified ```path```.
- The Route Component handles checking ```if``` the current URL matches the specified path, and if so renders its element.
```js
function App() {
    return (
        <Routes> {/* the collection of routes to match */}
            {/* if currentUrlPath === "home" */}
            <Route path="home" element={<HomePage />} />

            {/* if currentUrlPath ===  "about" */}
            <Route path="about" element={<AboutPage />} />
        </Routes>
    );
}
```
- The path ```prop``` is used to indicate the route that you wish to match—in particular, matching to the path part of the URL (after the domain). You do not include ```http``` or ```domain.com``` in the path.
- The “root” segment ```"/"``` is used to match to a URL without a path (e.g., what to show at ```http://domain.com```). Using a wildcard ```*``` in the path will match to “anything”, and is good for rendering “Page Not Found” elements.
- The Component (View) to render is passed in as the element prop. You instantiate the component using ```<Component/>``` syntax, and then that is passed as the inline expression (inside the ```{}```).
- You can of course pass additional props to the rendered component as normal:
```js
<Route path="profile" element={<ProfilePage user={userData} />} />
```
- All ```<Route>``` elements are made children of a single element called ```<Routes>```.
- The ```<Routes>``` element represents the “collection” of Routes that the Router needs choose between when deciding what Component to render (if any). You can think of it as acting like a ```switch``` statement.
- Note that a ```<Routes>``` can only have ```<Route>``` elements as children, and a ```<Route>``` element can only be the child of a ```<Routes>```. They go together, and nothing else (no other ```<div>```, etc. elements) can come between them.

## Nesting Routes
```js
<Routes>
    <Route path="user" element={<UserLayout />} >
        <Route path="profile" element={<UserProfile />} />
        <Route path="favorites" element={<FavoriteItems />} />
    </Route>
    <Route path="items" element={ <ItemList />} />
</Routes>
```
- When the <Routes> element goes to match a URL and determine which element to render, it will start with with the first segment of the path, rendering that element. For example, if the path starts with /user, then the Router will render the <UserLayout> element. But it will then continue checking further segments of the path.

- /user/profile renders ```<UserLayout><UserProfile/></UserLayout>```
- /user/favorites renders ```<UserLayout><UserFavorites/></UserLayout>```
- /user renders ```<UserLayout></UserLayout>``` (no child)
- /items renders ```<ItemList />```
> (You can think of each “nested child” step as a / in the path)

### Outlet
- You specify where in the parent element the child element will render using the ```<Outlet>``` Component.
- This component will be replaced by the element of whichever child route matches the URL segment:
```js
function UserLayout(props) {
    render (
        <div className="user-layout">
            <h1>User Page</h1>
            {/* will be replaced with <UserProfile>, <UserFavorites>, or null */}
            <Outlet />
        </div>
    )
}
```
## URL Parameters
- Written using :param syntax (a colon : followed by the parameter name). For example, the URI
```code
https://api.github.com/users/:username
```
- from the Github API refers to a particular user—you can replace :username with any value you want: ```https://api.github.com/users/joelwross``` refers to the joelwross user (so username = 'joelwross'), while ```https://api.github.com/users/mkfreeman``` refers to the mkfreeman user (so username = 'mkfreeman').
- React Router supports a similar syntax when specifying Route paths:
```js
<Route path='posts/:postId' element={<BlogPost />} />
```
The above will match a path that starts with ```posts/``` and is followed by any other path segment. The ```:postId``` (because it starts with the leading :) will be treated as a parameter which will be assigned whatever value is part of the URI in that spot—so ```post/hello``` would have ```'hello'``` as the ```postId```, and ```post/2017-10-31``` would have ```'2017-10-31'``` as the ```postId```.
- You can access the values assigned to the URL parameters by using the ```useParams``` hook provided by ```react-router```. This hook returns an object whose keys are the parameter names and whose values are the param values:

```js
import { useParams } from 'react-router-dom';

function BlogPost(props) {
    //access the URL params as an object
    //it's also common to use object destructuring here
    const urlParams = useParams();

    return (
        {/* postId was the URL parameter from the above example! */}
        <h1>You are looking at blog post {urlParams.postId}</h1>
    )
}
```
## Linking
- While specifying ```<Route>``` elements will allow you to show different “pages” at different URLs, in order for a Single Page Application to function you need to be able to navigate between routes without causing the page to reload. Thus you can’t just use normal ```<a>``` elements to link between “pages”—browsers interpret clicking on ```<a>``` elements as a command to send a new HTTP request, and you instead just want to change the URL and re-render the App.
-  React Router provides a ```<Link>``` element that you can use to create a hyperlink to another route within the application. This component takes a to prop that you use to specify the route that it links to:
```js 
<Link to="about">Click to visit the About Page</Link>
```
- The component will render as an ```<a>``` element with a special onClick handler that keeps the browser from loading a new page.
-  Importantly: a ```<Link>``` is a replacement for an ```<a>``` element
- A to property that is relative path (so doesn’t have a starting ```/```) will resolve relative to its parent route.
- React Router also provides a ```<NavLink>``` Component. This works exactly like the ```<Link>``` component, except if the to route matches the current route, then the element will have the active CSS class added to it. This is used for example to have a navigation section “highlight” the link to the page you’re currently on, helping the user understand where they are on the page.