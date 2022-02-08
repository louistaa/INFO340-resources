# Chapter 13 JavaScript Libraries
- Many web programmers encounter the same programming requirements as they develop interactive web sites.
- Since one of the main principles of software development is reuse, developers will often make the code solving these problems available for others to use in the form of libraries and frameworks.
- These are publicly release script files that you can download and include in your project, allowing you to more quickly and easily develop complex applications.
- This is the amazing thing about the open-source community: people solve problems and then make those solutions available to others.
- Modern web applications make extensive use of external libraries, whether by integrating many different libraries into a single app, or by relying on a particular framework (which may itself be comprised of many different libraries).

## Including a Library
- Just like you can include multiple CSS files in a page with multiple ```<link>``` elements, you can include multiple JavaScript scripts with multiple ```<script>``` elements.
```js
<script src="alpha.js"></script> <!-- run this script first -->
<script src="beta.js"></script> <!-- run this script second -->
```

- Script files are executed in the order in which they appear in the DOM. This matters because all scripts included via the ```<script>``` element are all run within the same namespace. This means variables and functions declared in one script file are also available in later scripts— it’s almost as if all the script files have been combined into a single file.
- You always want to load external libraries before your script, so that any variables and functions they define will be available to your code! If you put your script first, then those functions won’t be available yet!
