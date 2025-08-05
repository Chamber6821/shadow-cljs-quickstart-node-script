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

This runs `shadow-cljs watch :script` and `node ./build/index.js` via [concurrently](https://www.npmjs.com/package/concurrently)

# Live reload

To see the live reload in action you can edit the src/index.cljs. Some output will be printed in the terminal.

# nREPL

[Guide for Conjure](https://github.com/Olical/conjure/wiki/Quick-start:-ClojureScript-(shadow-cljs)#connect-and-select)

# Update JS state without reloading JS Runtime

## Example with handlers

```clj
(ns index)

(js/process.stdin.on "data" prn)
```

When you save your script, hot-reload will execute the file again.
The old handler will not be deleted and a new handler will be created.
Example of interaction (`npm run dev`):

```
[1] [:script] Configuring build.
[1] [:script] Compiling ...
[1] [:script] Build completed. (87 files, 0 compiled, 0 warnings, 1.52s)
[0] shadow-cljs - #3 ready!
first load
[0] #object[Buffer first load
[0] ]
[1] [:script] Compiling ...
[1] [:script] Build completed. (87 files, 1 compiled, 0 warnings, 0.08s)
code reloaded
[0] #object[Buffer code reloaded
[0] ]
[0] #object[Buffer code reloaded
[0] ]
```

To solve the problem with incorrect JS state updating,
it is worth doing all subscriptions inside the `-main` function

```clj
(ns index)

(defn -main []
  (js/process.stdin.on "data" prn))
```

But what if you should change handler?

```clj
(ns index)

(defn on-input [buffer]
  (prn buffer))

(defn -main []
  (js/process.stdin.on "data" #(on-input %)))
```

Why you should call `on-input` via lambda?
Because JS Runtime save reference to handler and CLJS runtime can't change this references.
But references from CLJS (from lambda) to CLJS (to `on-input`) can be updated by CLJS runtime and it's works! 
