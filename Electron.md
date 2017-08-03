# Setting up the Electron Environment #

First thing is first, make sure NodeJS and NPM is latest version, you can do this by checking the [documentation here](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04) or see the NodeNPM.md file.

### [electron-react-boilerplate](https://github.com/chentsulin/electron-react-boilerplate) ###

Because the setup is so comprehensive, this boilerplate solution fills in all the gaps automatically. Though, intensive knowledge regarding the packages is still required see link.

Here is how the generated package.json will look:

    {
      "name": "electron-react-boilerplate",
      "productName": "ElectronReact",
      "version": "0.10.0",
      "description": "Electron application boilerplate based on React, React Router, Webpack, React Hot Loader for rapid application development",
      "main": "main.js",
      "scripts": {
        "test": "cross-env NODE_ENV=test BABEL_DISABLE_CACHE=1 mocha --retries 2 --compilers js:babel-register --recursive --require ./test/setup.js test/**/*.spec.js",
        "test-watch": "npm test -- --watch",
        "test-e2e": "cross-env NODE_ENV=test BABEL_DISABLE_CACHE=1 mocha --retries 2 --compilers js:babel-register --require ./test/setup.js ./test/e2e.js",
        "lint": "eslint --format=node_modules/eslint-formatter-pretty app test *.js",
        "hot-server": "cross-env NODE_ENV=development node -r babel-register server.js",
        "build-main": "cross-env NODE_ENV=production node -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.electron.js --progress --profile --colors",
        "build-renderer": "cross-env NODE_ENV=production node -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.production.js --progress --profile --colors",
        "build": "npm run build-main && npm run build-renderer",
        "start": "cross-env NODE_ENV=production electron ./",
        "start-hot": "cross-env HOT=1 NODE_ENV=development electron -r babel-register -r babel-polyfill ./main.development",
        "package": "cross-env NODE_ENV=production node -r babel-register -r babel-polyfill package.js",
        "package-all": "npm run package -- --all",
        "postinstall": "node node_modules/fbjs-scripts/node/check-dev-engines.js package.json",
        "dev": "concurrently --kill-others \"npm run hot-server\" \"npm run start-hot\"",
        "cleanup": "mop -v"
      },
      "bin": {
        "electron": "./node_modules/.bin/electron"
      },
      "repository": {
        "type": "git",
        "url": "git+https://github.com/chentsulin/electron-react-boilerplate.git"
      },
      "author": {
        "name": "C. T. Lin",
        "email": "chentsulin@gmail.com",
        "url": "https://github.com/chentsulin"
      },
      "license": "MIT",
      "bugs": {
        "url": "https://github.com/chentsulin/electron-react-boilerplate/issues"
      },
      "keywords": [
        "electron",
        "boilerplate",
        "react",
        "react-router",
        "flux",
        "webpack",
        "react-hot"
      ],
      "homepage": "https://github.com/chentsulin/electron-react-boilerplate#readme",
      "devDependencies": {
        "asar": "^0.12.3",
        "babel-core": "^6.17.0",
        "babel-eslint": "^7.0.0",
        "babel-loader": "^6.2.5",
        "babel-plugin-add-module-exports": "^0.2.1",
        "babel-plugin-dev-expression": "^0.2.1",
        "babel-plugin-tcomb": "^0.3.19",
        "babel-plugin-webpack-loaders": "^0.8.0",
        "babel-polyfill": "^6.16.0",
        "babel-preset-es2015": "^6.16.0",
        "babel-preset-react": "^6.16.0",
        "babel-preset-react-hmre": "^1.1.1",
        "babel-preset-react-optimize": "^1.0.1",
        "babel-preset-stage-0": "^6.16.0",
        "babel-register": "^6.16.3",
        "boiler-room-custodian": "^0.4.2",
        "chai": "^3.5.0",
        "concurrently": "^3.1.0",
        "cross-env": "^3.1.3",
        "css-loader": "^0.25.0",
        "del": "^2.2.2",
        "devtron": "^1.4.0",
        "electron": "^1.4.4",
        "electron-debug": "^1.0.1",
        "electron-devtools-installer": "^2.0.1",
        "electron-packager": "^8.1.0",
        "electron-rebuild": "^1.3.0",
        "enzyme": "^2.5.1",
        "eslint": "^3.8.1",
        "eslint-config-airbnb": "^12.0.0",
        "eslint-formatter-pretty": "^1.1.0",
        "eslint-import-resolver-webpack": "^0.6.0",
        "eslint-loader": "^1.6.0",
        "eslint-plugin-flowtype-errors": "^1.4.1",
        "eslint-plugin-import": "^2.0.1",
        "eslint-plugin-jsx-a11y": "^2.2.3",
        "eslint-plugin-mocha": "^4.7.0",
        "eslint-plugin-promise": "^3.3.0",
        "eslint-plugin-react": "^6.4.1",
        "express": "^4.14.0",
        "extract-text-webpack-plugin": "^1.0.1",
        "fbjs-scripts": "^0.7.1",
        "jsdom": "^9.8.0",
        "json-loader": "^0.5.4",
        "minimist": "^1.2.0",
        "mocha": "^3.1.2",
        "node-libs-browser": "^1.0.0",
        "react-addons-test-utils": "^15.3.2",
        "redux-logger": "^2.7.0",
        "sinon": "^1.17.6",
        "spectron": "^3.4.0",
        "style-loader": "^0.13.1",
        "tcomb": "^3.2.15",
        "webpack": "^1.13.2",
        "webpack-dev-middleware": "^1.8.4",
        "webpack-hot-middleware": "^2.13.0",
        "webpack-merge": "^0.15.0",
        "webpack-validator": "^2.2.9"
      },
      "dependencies": {
        "css-modules-require-hook": "^4.0.5",
        "electron-debug": "^1.0.1",
        "font-awesome": "^4.6.3",
        "postcss": "^5.2.5",
        "react": "^15.3.2",
        "react-dom": "^15.3.2",
        "react-redux": "^4.4.5",
        "react-router": "^3.0.0",
        "react-router-redux": "^4.0.6",
        "redux": "^3.6.0",
        "redux-thunk": "^2.1.0",
        "source-map-support": "^0.4.5"
      },
      "devEngines": {
        "node": ">=4.x",
        "npm": ">=3.x"
      }
    }

## devDependencies ##

### asar ###

**Creating Electron app packages**

Asar is a simple extensive archive format, it works like tar that concatenates all files together without compression, while having random access support.

### babel-core ###

Babel is a compiler for writing next generation JavaScript.

### babel-eslint ###

babel-eslint allows you to lint ALL valid Babel code with the fantastic ESLint.

### babel-loader ###

This package allows transpiling JavaScript files using Babel and webpack.

### babel-plugin-add-module-exports ###

Allows default export behavior.

### babel-plugin-dev-expression ###

This plugin reduces or eliminates development checks from production code.
`__DEV__` becomes `process.env.NODE_ENV !== 'production'`

### babel-plugin-tcomb ###

Flow is a static type checker for JavaScript.

tcomb is a library for Node.js and the browser which allows you to check the types of JavaScript values at runtime with a simple and concise syntax. It's great for Domain Driven Design and for adding safety to your internal code.

### babel-plugin-webpack-loaders ###

This Babel 6 plugin allows you to use webpack loaders in Babel.

### babel-polyfill ###

Provides polyfills necessary for a full ES2015+ environment

### babel-preset-es2015 ###
### babel-preset-react ###
### babel-preset-react-optimize (OLD) ###
### babel-preset-react-hmre (OLD) ###
### babel-preset-stage-0 ###
### babel-register ###

### boiler-room-custodian ###

Simple 🌝 There are lots of amazing boilerplates out there that do a great job of giving us what we need. They also often include minimal sample app code just so we can "see it run". What boiler-plate-custodian aims to do is have a way to use configuration to clean that all up when ready to start development on the project.

### chai ###

Chai is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework.

### concurrently ###

Run multiple commands concurrently. Like npm run watch-js & npm run watch-less but better.

### cross-env ###

Run commands that set environment variables across platforms. This micro-lib allows you to provide a script which sets an environment using unix style and have it work on windows too

### css-loader ###

    var css = require("css!./file.css");
    // => returns css code from file.css, resolves imports and url(...) 

@import and url(...) are interpreted like require() and will be resolved by the css-loader. Good loaders for requiring your assets are the file-loader and the url-loader which you should specify in your config (see below).

### del ###

Delete files and folders
Pretty much rimraf with a Promise API and support for multiple files and globbing. It also protects you against deleting the current working directory and above.

### devtron ###

Electron DevTools Extension
An Electron DevTools extension to help you inspect, monitor, and debug your app.

### electron ###

Electron is a JavaScript runtime that bundles Node.js and Chromium. You use it similar to the node command on the command line for executing JavaScript programs. For more info you can read this intro blog post or dive into the Electron documentation.

### electron-debug ###
### electron-devtools-installer ###

### electron-packager ###

Package and distribute your Electron app with OS-specific bundles (.app, .exe etc) via JS or CLI

### electron-rebuild ###

This executable rebuilds native Node.js modules against the version of Node.js that your Electron project is using. This allows you to use native Node.js modules in Electron apps without your system version of Node.js matching exactly (which is often not the case, and sometimes not even possible).

### enzyme ###

Enzyme is a JavaScript Testing utility for React that makes it easier to assert, manipulate, and traverse your React Components' output.

### eslint ###

Javascript linter and plugins...

### eslint-config-airbnb ###
### eslint-formatter-pretty ###
### eslint-import-resolver-webpack ###
### eslint-loader ###
### eslint-plugin-flowtype-errors ###
### eslint-plugin-import ###
### eslint-plugin-jsx-a11y ###
### eslint-plugin-mocha ###
### eslint-plugin-promise ###
### eslint-plugin-react ###

### express ###

Fast, unopinionated, minimalist web framework

### extract-text-webpack-plugin ###

Extract text from bundle into a file.

### fbjs-scripts ###

A bundle of helpful scripts used in projects consuming fbjs.
This is a collection of tools and scripts intended to be used in conjunction with fbjs. Previously these were shipped as a part of fbjs.

### jsdom ###

A JavaScript implementation of the DOM and HTML standards

    // Run some jQuery on a html fragment 
    var jsdom = require("jsdom");
     
    jsdom.env(
      '<p><a class="the-link" href="https://github.com/tmpvar/jsdom">jsdom!</a></p>',
      ["http://code.jquery.com/jquery.js"],
      function (err, window) {
        console.log("contents of a.the-link:", window.$("a.the-link").text());
      }
    );

### json-loader ###

json loader module for webpack

    var json = require("json!./file.json");
    // => returns file.json content as json parsed object 

### minimist ###

    $ node example/parse.js -a beep -b boop
    { _: [], a: 'beep', b: 'boop' }

### mocha ###

Mocha is a simple, flexible, fun JavaScript test framework for node.js and the browser.

### node-libs-browser ###

The node core libs for in browser usage.

### react-addons-test-utils ###

This package provides the React TestUtils add-on.

### redux-logger ###

Logs to console redux state.

### sinon ###

Standalone test spies, stubs and mocks for JavaScript.
No dependencies, works with any unit testing framework.

### spectron ###

Easily test your Electron apps using ChromeDriver and WebdriverIO.

WebDriver is an open source tool for automated testing of webapps across many browsers. It provides capabilities for navigating to web pages, user input, JavaScript execution, and more.  ChromeDriver is a standalone server which implements WebDriver's wire protocol for Chromium. ChromeDriver is available for Chrome on Android and Chrome on Desktop (Mac, Linux, Windows and ChromeOS).  
### style-loader ###

style loader module for webpack

### tcomb ###

tcomb is a library for Node.js and the browser which allows you to check the types of JavaScript values at runtime with a simple and concise syntax. It's great for Domain Driven Design and for adding safety to your internal code.

### webpack ###

Packs CommonJs/AMD modules for the browser. Allows to split your codebase into multiple bundles, which can be loaded on demand. Support loaders to preprocess files, i.e. json, jade, coffee, css, less, ... and your custom stuff.

### webpack-dev-middleware ###

Offers a dev middleware for webpack, which arguments a live bundle to a directory

### webpack-hot-middleware ###

Webpack hot reloading using only webpack-dev-middleware. This allows you to add hot reloading into an existing server without webpack-dev-server.

### webpack-merge ###

webpack-merge provides a merge function that concatenates arrays and merges objects. This behavior is particularly useful in configuring webpack. 

### webpack-validator ###

Writing webpack configs is brittle and error-prone. This package provides a joi object schema for webpack configs. This gets you a) static type safety, b) property spell checking and c) semantic validations such as "loader and loaders can not be used simultaneously" or "query can only be used with loader, not with loaders".

## dependencies ##

### css-modules-require-hook ###

A require hook to compile CSS Modules on the fly

### font-awesome ###
### postcss ###
### react ###
### react-dom ###
### react-redux ###
### react-router ###
### react-router-redux ###
### redux ###
### redux-thunk ###
### source-map-support ###

# Rollup Installation ##

This is still also an option, still deciding whether I should go this route rather.

Here is a list of rollup plugins;

https://github.com/rollup/rollup/wiki/Plugins