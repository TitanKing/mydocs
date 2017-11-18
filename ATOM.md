# The Awesome Atom Editor #

Atom editor is a free open source replacement for advanced development in Javascript, Node and many other languages. It shines due to its excellent plugins and customization capabilities.

## Basic Setup Guidelines ##

Here is is a list of recommended changes and tips to make before you get started.

### Tips ###

- Try and keep your node modules local to the project.
- [Level Up Tutorials](https://www.youtube.com/watch?v=ZnzLPIhMJnws)
- Double Click on open tab to create new file.

### Settings ###

In Editor Settings change:

- Preferred Line Length: 120
- Tabs Type: soft
- Tab Length: 4

### Shortcuts ###

Context Menu [M1] `ctrl+shift+h`
Duplicate Line `ctrl+shift+d`
Find files Quickly `ctrl+t`
Jump to line `ctrl+g`
Multicursor... WOW `ctrl+click`
Comment Out `ctrl+/`

**emmet plugin**

[Example Video](https://www.youtube.com/watch?v=BQurqKG6nGY)
[Cheatsheet](http://docs.emmet.io/cheat-sheet/)

### Installing JS Linter ##

You would first need to install jshint node package;

    npm install --save-dev eslint 

Set the basic linter in your project up with:

    ./node_modules/.bin/eslint --init

Install the base linter with;

    apm install linter

Then install eslinter with;

    apm install linter-eslint

### Look and Feel ###

You cant go without this brilliant ligatures font (changes the way the arrows etc looks):

[FiraCode](https://github.com/tonsky/FiraCode)

- In Editor Settings -> Change Font Family to `Fira Code` 

## Plugins ##

Here is a list of nice to have [plugins](http://www.hongkiat.com/blog/useful-atom-packages/)

### git-plus ###

Allows to run git tasks quickly from the tasker.

### autocomplete-modules ###

Helps to auto complete import modules.

### atom-beautify ###

Beautify will turn your messy code neater and more readable. It has great support for programming languages, such as HTML, CSS, JavaScript, PHP, Python, Ruby, Java, C, C ++, C #, Objective-C, CoffeeScript, typescript, and SQL. After installing this package, to run it, just right-click and choose ‘Beautify editor contents’, or via Packages > Atom Beautify > Beautify.

### file-icons ###

Adds nice icons to file types.

### emmet ###

Expand abbreviations by Tab key.

### highlight-selected ###

Highlight text of the same word.

### open-recent ###

Opens recently files from the Files menu.

### git-diff ###

Allows you to see git changes in editor gutter.

### javascript-snippets ###

Like emmet but for javascript, write many repetitive code easily.

### pigments ###

Shows the correct color bgs for css color declarations.

### seti-ui ###

Nice looking theme.

### toggle-quotes ###

Easily convert quotes to single or double with `shift+ctrl+'`

### docblockr ###

Adds block comments to functions etc.

### atom-ternjs ###

TernJS provides code intelligence for Atom, with intelligent autocomplete with type information.

### sync-settings ###

You spent lots of time customizing Atom. What if you want to do the same on a new machine? Or reinstall your system may be? This plugin saves your customizations in a Github Gist so that you don’t have to do it all over again.

### local-history ###

Maintaining local history of files (history of your changes to the code files).

### git-time-machine ###

View git history visually in atom.

### autocomplete-plus ###

Build in autocomplete with the ability to enhance [providers](https://github.com/atom/autocomplete-plus/wiki/Autocomplete-Providers).

### autocomplete-flow ###

Autocomplete for flow.

### es6-javascript ###

A collection of commands and ES6 focused snippets for optimizing modern Javascript development productivity. It aims to be compliant with AirBnB's mostly reasonable approach to Javascript.

### goto-definitions ###

Goto declarations and other.

First install:

[rust](https://www.rust-lang.org/en-US/install.html)
`cargo install ripgreg`