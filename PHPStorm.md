 
## PHPStorm Setup and Plugins ##
I find PHPStorm to be one of the best IDEs out there, following are a list of nice setups, shortcuts and plugins.

## Shortcuts (Default keys are assumed)
### Bookmarks
Bookmarks is used to jump between lines of code within a project, it is extremely useful if you code between two files etc.
`Ctrl+F11` Create Bookmark
`Shift+F11` View Bookmarks (Can delete from here too)
`Ctrl+Up/Down` Shift Bookmarks up or down

### General
`Ctrl+Tab` Jump to any of a list of opened files.
`Ctrl+E` Navigate to recent file.
`Ctrl+Space` Basic code completion.
`Ctrl+Alt+N` Refactor code (custom keys)
`ctrl+/` Comment/uncomment current line or selected block with line comments
`shift+ctrl+/` Comment/uncomment code with block comments
`ctrl+shift+t` Call code templates or surround code.
`ctrl+shift+n` Quick file search and open.

### AceJump
Jump to any part of the code without using the mouse.
`Ctrl+Semicolon` Then press a letter of the word you would want to jump to, it will then give you a lettered index to press next and it will then jump to that word.
`Hold-Shift+Indexed Letter` to highlight to that word.
`(While index shows)Enter` to further expand the indexes.

### Custom
`M1` Acejump
`M2` Quick file search and open.
`M3`
`M4`
`M5`

### Views
`Alt+G` Refactor Code
`Alt+F` Full Screen
`Alt+D` Distraction Free
`Alt+P` Presentation Mode

### Improving "Webstorm" with better React Native support ###

Install react native eslint help tools:

- [read-first](https://medium.com/the-react-native-log/getting-eslint-right-in-react-native-bd27524cc77b#.woash62ch)
- [install eslint and plugins](https://www.npmjs.com/package/eslint-plugin-react-native)
- [configure](http://eslint.org/docs/user-guide/configuring)

Here is a install shortcut:

    npm install -g babel-eslint eslint eslint-plugin-react eslint-plugin-react-native

Here is my eslint package.json entry in your project folder:

    "eslintConfig": {
        "parser": "babel-eslint",
        "env": {
          "browser": true,
          "node": true,
          "jquery": true,
          "jest": true,
          "mocha": true,
          "amd": true,
          "es6": true
        },
        "parserOptions": {
          "ecmaVersion": 6,
          "sourceType": "module",
          "ecmaFeatures": {
            "jsx": true,
            "experimentalObjectRestSpread": true,
            "impliedStrict": true
          }
        },
        "plugins": [
          "react",
          "react-native"
        ],
        "extends": [
          "eslint:recommended",
          "plugin:react/recommended"
        ],
        "globals": {
          "beforeEach": true,
          "describe": true,
          "expect": true,
          "it": true,
          "React": true,
          "xdescribe": true,
          "xit": true
        },
        "rules": {
          "react-native/no-unused-styles": 2,
          "react-native/split-platform-components": 2,
          "react-native/no-inline-styles": 2,
          "react-native/no-color-literals": 2
        }
    }

The `extends:` keyword is there to extend the default recommended settings as above.

For documentation about the rules that you can use, you can see the following links:

[eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react#list-of-supported-rules)
[eslint](http://eslint.org/docs/rules/)

**Note:** Remember to now set the eslinter up in PHPStorm/Webstorm Launguages and Frameworks -> Javascript -> Code Quality Tools

Also see [Webstorm Blog](https://blog.jetbrains.com/webstorm/2016/08/using-external-tools/)

## Nice color selections for the color codings ##

[Google Material](https://material.google.com/style/color.html)

## Font ##

I cannot state how nice font ligatures are:

- [FiraCode](https://github.com/tonsky/FiraCode)




