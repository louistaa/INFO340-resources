# Chapter 1 Getting Setup
## Web Browser
- Use Google Chrome.
- All browsers don't support every new front end technologies/frameworks.
    - For instance: a component library may be supported in lastest version of Chrome but not in the latest version of Edge.
- https://caniuse.com/ - a resource that shows which versions of each major browser supports the front end technology you search.

## Text Editors
- Use Visual Studio Code.
- Industry standard text-editor.
- Has many [extensions](https://code.visualstudio.com/docs/editor/extension-marketplace) built by the community that you can download to enhance your coding experience.
- Has a built-in feature called [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette), which houses feature shortcuts.
    - macOS: Command+Shift+P; Windows: Ctrl+Shift+P

### Extensions that I recommend
1. [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare): enables real-time coding collaboration - great for your group projects.

## Useful keyboard shortcuts
1. In a .html file type ```!``` then followed by ```tab``` to create the basic scaffolding of a HTML file.
2. Format your document (make spacing and whitespacing consistent on your html/css/js files):
    - On Windows Shift + Alt + F
    - On Mac Shift + Option + F

## Git and GitHub
- Test if git is working by running the following command in your terminal: ```git --version```. It should return a version number.
- If it doesn't work, your terminal will say something like ```git: command not found``` or ```'git' is not recognized as an internal or external command,
operable program or batch file.```

## Node and npm
- Node.js is a runtime environment that executes JavaScript code outside a web browser. 
- Test if node.js working by running the following command in your terminal: ```node --version```. It should return a version number.
- If it doesn't work, your terminal will say something like ```node: command not found```.
- npm is a package manager for the JavaScript programming language. In other words, it is like the Apple App Store or Google Play Store for JavaScript.
- Test if npm working by running the following command in your terminal: ```npm --version```. It should return a version number.
- If it doesn't work, your terminal will say something like ```npm: command not found```.

## Managing packages with npm
- npm is a text-based interface
- You'll install packages (like apps for your phone) through the terminal
- Two ways to install packages:
    1. Locally: ```npm install PACKAGE-NAME```.
    2. Globally: ```npm install -g PACKAGE-NAME```.
- Installing globally makes the package available across the entire computer.
    - You would want to do this when you know you will use a package across multiple projects. For example, Jest.
- Installing locally makes it available just in the particular folder you evoked the command in.
    - You would want to do this when your project requires a very niche package that you know you will not use in another project.
- ```npx``` command lets you install and execute the package at the same time(hence the x). I don't use this too often.

## package.json
- Dependencies are packages that must be installed in order for the program to work.
- As projects become large, it is common for them to build up many dependencies.
- You can find your project's list of dependencies in the ```package.json``` file.
- These dependencies don't come automatically installed, so you have to use npm (similiar how you have to patch a game after installing it for the first time).
- Using ```npm install``` will install all of the packages listed under in the package.json.
- 99% of projects in industry will have a package.json so make sure you install your dependencies whenever you download a project or checkout a repository. 