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