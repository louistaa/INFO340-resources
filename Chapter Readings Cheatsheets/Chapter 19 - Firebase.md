# Chapter 19 Firebase
- Firebase is a web service that provides tools and infrastructure for use in creating web and mobile apps that store data online in the cloud.

In particular, this chapter will discuss two features of Firebase V9:
1. The Firebase service also provide a number of “datbase” systems. This chapter describes how to use the realtime database, which provides a simple NoSql-style database: you can think of it as a single giant JSON object in the Cloud.
2. The Firebase service also offers a client-side based system for performing user authentication, or allowing users to “sign in” to your application and have particular information associated with them.

## Including Firebase in React
1. First, install and Firebase library using npm:
```bash
# Note: do this in your app's repo (the folder with the `package.json` file)

npm install firebase
```
- Then, copy the provided import statement, firebaseConfig variable, and ```initializeApp()``` function call into your index.js file. This will specify which Firebase project your web app should connect to whenver you call functions to access Firebase.
- Note that you will need to paste this code before the call ```ReactDOM.render()```.

## Data References
- To start working with your database, you will need to get a reference to that value in the database.

You begin by getting a reference to the database itself, using the ```getDatabase()``` function provided by Firebase’s database module ```firebase/database```:
```js
//import the function from the realtime database module
import { getDatabase } from 'firebase/database';

// Get a reference to the database service
const db = getDatabase();
```
- In order to modify any particular values in the database, you will need to get a reference to that value. This is done by using the ```ref()``` function, passing in the database reference and the “path” (a string) to the data value in the database’s JSON:

```js
import { getDatabase, ref } from 'firebase/database';

//get a reference to the database service
const db = getDatabase();

//get reference to the "people"" property in the database
const peopleRef = ref(db, "people")

//get reference to the "sarah" property inside the "people" property in the database
//similar to `database.people.sarah` using dot notation
const sarahRef = ref(db, "people/sarah");
```
- The “path” to nested values in the database are written in a URI-style “path notation”, where each nested key is indicated by a slash ```/``` (rather than the ```.``` in dot notation as you’d normally use).

## Writing Data
- You can modify values in the database by using the ```set()``` function. This function takes two arguments: a database reference, and then the new value you want to assign to that location in the database:

```js
//alias the `set` function as `firebaseSet`
import { ref, set as firebaseSet } from 'firebase/database'

//get a reference to where sarah's age is stored in the database
const sarahAgeRef = ref(db, "people/sarah/age");

//change Sarah's age to 43 (happy birthday!)
const newValueForSarahAge = 43;

//assign the new value in the database
firebaseSet(sarahRef, newValueForSarahAge);
```
- This will change the value in the database at ```"people/sarah/age"``` to ```43```.

> Note that in this example, I have use the as keyword to alias the ```set``` function when importing it, instead calling it ```firebaseSet```. This is for clarity, as “set” is an overly generic name for a function.
- Finally, note that the ```set()``` method returns a Promise. This you can use ```.then()``` (or ```await```) to execute statements after the database has updated, and you can thus catch any errors that may occur when attempting to update a value.

## Listening for Data Changes
- You register a database change listener by using the ```onValue()``` function. This function takes as arguments a database reference (which value you want to listen for changes to) and a callback function that will be executed in response to the event (similar to the DOM’s ```addEventListener()``` function):
```js
import { ref, onValue } from "firebase/database"

//get a reference to a particular value location in the database
const amitRef = ref(db, 'people/amit');

//register a listener for changes to that value location
onValue(amitRef, (snapshot) => {
    const amitValue = snapshot.val();
    console.log(amitValue); //=> e.g., { age: 35, petName: "Spot" }
    //can do something else with amitValue (e.g., assign to a state variable)
});
```
- The callback function will be passed as a parameter the latest snapshot of the data value at the listening location.
- You will want to convert the snapshot into an actual JavaScript object by calling the ```.val()``` method on it.
- You will need to register the listener inside an effect hook.
- The effect hook’s “cleanup function” will also need to remove the listener by calling the .off() method on the database reference—otherwise you will have a memory leak and errors if your component gets removed.

```js
function MyComponent(props) {
  //effect hook
  useEffect(() => {
    const db = getDatabase();
    const amitRef = ref(db, "people/amit");

    onValue(amitRef, (snapshot) => {
      const amitValue = snapshot.val();
      //...set state variable, etc...
    })

    //cleanup function for when component is removed
    function cleanup() {
      amitRef.off(); //turn off all listeners
    }
    return cleanup; //effect hook callback returns the cleanup function
  })
}
```

## Firebase Arrays
- Firebase does not directly support support arrays: the JSON object in the sky only contains objects, not arrays!
- Firebase does offer a way that you can treat Objects as arrays, in the form of a ```push()``` function that will add a value to an object with an auto-generated key.

```js
import { getDatabase, ref, push as firebasePush } from 'firebase/database';

const db = getDatabase;
const tasksRef = ref(db, "tasks"); //an object of tasks

tasksRef.push( {description:'First things first'} ) //add one task
tasksRef.push( {description:'Next things next'} ) //add another task
```
This will produce a database with a structure:
```js
{
  "tasks" : {
    "-KyxgJhKOVeAj2ibPxrO" : {
      "description" : "First things first"
    },
    "-KyxgMDJueu17348NxDF" : {
      "description" : "Next things next"
    }
  }
}
```
## FirebaseUI
- There are different FirebaseUI libraries for different platforms; for React you would use ```firebaseui-web-react```.
```bash
npm install react-firebaseui
```
- The React FirebaseUI library provides a Component called ```<StyledFirebaseAuth>```, which you can render in your page like any other Component.

```js
//import auth functions and variables from Firebase
import { getAuth, EmailAuthProvider, GoogleAuthProvider } from 'firebase/auth'

//import the component
import StyledFirebaseAuth from 'react-firebaseui/StyledFirebaseAuth';

//an object of configuration values
const firebaseUIConfig = {
  signInOptions: [ //array of sign in options supported
    //array can include just "Provider IDs", or objects with the IDs and options
    GoogleAuthProvider.PROVIDER_ID,
    { provider: EmailAuthProvider.PROVIDER_ID, requiredDisplayName: true },
  ],
  signInFlow: 'popup', //don't redirect to authenticate
  credentialHelper: 'none', //don't show the email account chooser
  callbacks: { //"lifecycle" callbacks
    signInSuccessWithAuthResult: () => {
      return false; //don't redirect after authentication
    }
  }
}

//the React compnent to render
function MySignInScreen() {

  const auth = getAuth(); //access the "authenticator"

  return (
    <div>
      <h1>My App</h1>
      <p>Please sign-in:</p>
      <StyledFirebaseAuth uiConfig={firebaseUIConfig} firebaseAuth={auth} />
    </div>
  );
}
```
- The ```<StyledFirebaseAuth>``` requires a uiConfig prop, which is an object containing configuration values for that login form.
- The most important configuration option is the signInOptions, listing the different authentication providers supported.
- See full list [here](https://github.com/firebase/firebaseui-web#configuration).
- The ```<StyledFirebaseAuth>``` also requires a firebaseAuth prop, which is a reference to the “authenticator” service—what will handle the process of the user logging in and out. You can get access to this value via the ```getAuth()``` function provided by ```'firebase/auth'```.
> Pro-tip: You don’t need to come up with real email addresses for testing. Try using ```a@a.com```, ```b@a.com```, ```c@a.com```, etc. Similarly, password works fine for testing passwords (though you should never do that in real life!).
- In order to sign out a user, you will need to use a built-in Firebase function: ```signOut()```:
```js
import { getAuth, signOut } from 'firebase/auth';

const auth = getAuth();

signOut(auth)
    .catch(err => console.log(err)); //log any errors for debugging
```
- Note that the ```signOut()``` method returns a Promise, so you can ```.catch()``` and display any errors.

## Managing the User
- The recommended way to determine who is currently logged in is to register an event listener to listen for events that occur with the “state” of the authentication changes (e.g., a user logs in or logs out).
- You can register this listener by using the ```onAuthStateChanged()``` function inside an effect hook.
- The function takes in two arguments: the authenticator, and a callback function that will be executed whenever the “authentication state” changes (e.g., whenever the user logs in or out). The callback function will be passed an object representing the “Firebase User”. This object contains properties about the user, including:
1. ```uid```, which is the unique id for the user.
2. ```displayName```, which is the user’s provider-independent displayable name.
- The most common practice is to take this passed in object and assign it to a more global variable, such as a state variable in a React function (e.g., ```setCurrentUser(firebaseUser)```).

```js
function MyComponent(props) {
  //effect hook
  useEffect(() => {
    const auth = getAuth();

    //returns a function that will "unregister" (turn off) the listener
    const unregisterFunction = onAuthStateChanged(auth, (firebaseUser) => {
      //handle user state change
      if(firebaseUser){
        //...
      }
    })

    //cleanup function for when component is removed
    function cleanup() {
      unregisterFunction(); //call the unregister function
    }
    return cleanup; //effect hook callback returns the cleanup function
  })
}
```