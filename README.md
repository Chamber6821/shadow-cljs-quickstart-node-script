# shadow-cljs - node-script quickstart

This is a minimal template that can be used as a basis for CLJS projects designed to develop NodeJS applications.

# Required Software

- [node.js (v20.19.3 for me)](https://nodejs.org/en/download)
- [Open JDK (v21.0.8 for me)](https://openjdk.org/projects/jdk/)

# User Guide

This repository only shows a basic example of how to get a basic NodeJS build.

Please refer to the full [User Guide](https://shadow-cljs.github.io/docs/UsersGuide.html) for more information.

# Running the Example

```shell
git clone git@github.com:shadow-cljs/quickstart-browser.git quickstart
cd quickstart
npm install
npm run dev
````

This runs `shadow-cljs watch :script` and `nodemon ./build/index.js` via [concurrently](https://www.npmjs.com/package/concurrently)

# Live reload

To see the live reload in action you can edit the src/index.cljs. Some output will be printed in the terminal.

> [!NOTE]
> You may need to reload the JS Runtime, for which you can use [manual nodemon reload](https://github.com/remy/nodemon#manual-restarting)


# nREPL

[Guide for Conjure](https://github.com/Olical/conjure/wiki/Quick-start:-ClojureScript-(shadow-cljs)#connect-and-select)
