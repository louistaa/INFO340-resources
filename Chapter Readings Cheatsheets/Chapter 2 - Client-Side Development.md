# Chapter 2 Client-Side Development
- Honestly, nothing too substantial in this chapter.

## Development Servers
- As you are working on your problem sets and project, you should use a local development server (live server extension).
- A local development server is a server that you run from your own computer. Your machine acts as a web server, and you use the browser to have your computer send a request to itself for the webpage.
- Main benefit is that your browser will automatically reload the web page when the source code changes.
- The address 127.0.0.1 is the IP address for localhost which is the domain of your local machine (the “local host”).
- Make sure to start the local development server in the root directory.

## live-server
- https://github.com/tapio/live-server
- A VERY useful package to speed up the development of your problem sets and project is live-server.
- To install: ```npm install -g live-server```
    - Notice how we are installing globally because we want to use this package across multiple projects.
- To run the local server, ```cd``` into the root directory of your project then type ```live-server```. A browser tab should appear up with the localhost address.
- To stop the server, use the ```crtl + c``` command in the terminal.