# ES6 Development Notes #

My own personal notes regarding the ES6 changes and things that one should at least understand.

## Shorthand properties ##

Easily construct objects;

    let firstName = "John";
    let lastName = "Peterson";

    let person = {firstName, lastName};
    console.log(person); // {firstName: John, lastName: "Peterson"}

Even functions;

    let color = "red"
    let speed = 10;
    function go() {
        console.log("Wroom!");
    }

    let car = {
        color,
        speed,
        go
    }

    car.go(); // Wroom!

Or even;

    let car = {
        color,
        speed,
        go() {
            //code
        }
    }

Or even computed properties;

    let car = {
        color,
        speed,
        ["go"] => () {
            //code
        }
    }

## Let and constants ##

* Use `var` at the top level (sparingly use for global).
* Default to using `let` for the rest for block scope.
* Use `const` where you assume value should never change (although it can).

Let is strict;

    let message = "hi";
    {
        let message = "world";
    }

    console.log(message); // hi

const is not immutable;

    const VALUE = { test: 'World' };
    VALUE.test = 'new world' // will still allow to assign.

const also adheres to blockscope;

    if (true) {
        const foo = 'bar';
    }
    console.log(foo); // nope, undefined.

### TERM: hoisted ###

variables in js if declared anywhere gets hoisted to the top of the scope, giving undefined if it is called where it does not have access. If it were not declared anywhere it will give a reference error instead.

NOTE: Its good practice to define variables at the top.

## Arrow functions ##

Shorthand:

    function someTask (var1, var2) {
        console.log('Some Task');
    }

Becomes (with other examples):

    (var1, var2) => console.log('Some Task');
    var1 => console.log('Some Task');
    () => console.log('Some Task');
    var 1 => {
        console.log('Some Task');
    }

* Note that with `this` keyword in arrow functions is not scope bound as with functions.
* `return` keyword is implicit on arrow functions.

For empty function simply do:

    () => console.log('Hello World');

Notice the scope;

    this.handleSomething((message) => {
        console.log(message + this.name); // this would refer to the outer scope, unlike when you would use an anonymous function.
    });

## Default parameters ##

    function (cost, discount=10) {
    }

**NOTE:** default params can also be a function.

## Rest and spread ##

* Solves the issue where want would want to assign any number of arguments. *
* Or where you want to apply to arguments for spreading. *

Spreading and rest;

    let first = [1,2,3,4]
    console.log(...first); // 1 2 3 4 (not array)

    // rest
    function sum(...numbers) {
        // [1,2,3,4]
    }
    sum(1,2,3,4);

    // spread
    function sum(x, y) {
        return x+y;
    }
    let numbers = [1, 2];
    sum(...numbers);

## Strings templates ##

* Solves the mess with concatenation. *

Example;

    let template = `
        <div>
            <span>${foobar}</span>
        </div>    
    `;

Note, you can do expressions inside templates;

    let x = 10;
    let y = 15;

    let equation = `${ x } + ${ y } = ${ x + y }`;

Convert templates to data;

    function anyThing(string, ...values) => {
        console.log(string);
        console.log(values);
    }
    let message = anyThing`It is ${new Date().getHours()} I am sleepy`;
    Will console log: ['It', 'is', 'I', 'am', 'sleepy'] and [ 15 ]

You can also reassign strings;

## Objects ##

    function getPerson () {
        let name = 'John';
        let age = 25;
        return {
            name: name,
            age: age
        }
    }

instead write;

    function getPerson () {
        let name = 'John';
        let age = 25;
        return {name,age}
    }


Or this is also cool:

    return {
        name,
        age,
        greet() {
            return `Hello, ${this.name}`
        }
    }

### Object Destruct ###

    let person = {
        name: 'Karen',
        age: 32,
        results: ['foo', 'bar'],
        count: 30    
    }

becomes;

    let {results, count} = person;
    console.log(results) // ['foo', 'bar']

Another Example example;

    function generateObj() {
        return {
            color: "blue",
            name: "John",
            state: "New York",
            position: "Forward"
        }
    }
    let {name:firstName, state} = generateObj();
    console.log(firstName);
    console.log(state);

**Even Cooler**

    // eg. want only results
    function filterData(data) {
        return data.results;
    }

    filterData ({
        name: 'Karen',
        age: 32,
        results: ['foo', 'bar'],
        count: 30   
    });

becomes;

    function filterData({results}) {
        return results;
    }

How about arrays?

    let [first,,,,,fifth] = ["red","yellow","green","blue","orange"];
    console.log(first); // red
    console.log(fifth); // orange

Looping...

    let people = [
        {
            "firstName": "James",
            "lastName": "Small"
        },
        {
            "firstName": "Peter",
            "lastName": "Bennet"
        },
        {
            "firstName": "Nadia",
            "lastName": "Silano"
        }
    ];
    people.foreach({firstName} => console.log(firstName));
    // or
    let [,SecondUser] = people;
    function() logEmail({lastName}) {
        console.log(lastName); // Bennet
    }
    
Combining destructuring...

    const companies = [
      { name: 'Google', location: 'Mountain View' },
      { name: 'Facebook', location: 'Menlo Park' },
      { name: 'Uber', location: 'San Francisco' }
    ];
    
    const [{location}] = companies; // Mountain View 

### Parameter Object Destructuring with Required Values ###

Take this example;

    function ajax({
        type = "get",
        url = requiredParameter("url"),
        data = {},
        success = requiredParameter("success"),
        error => () => {},
        isAsync = true} = {}) {
            // ...
        }
    });
    function requiredParameter(name) {
        throw new Error(`Missing parameter "${name}"`);
    }
    try {
        ajax({
            url: 'http://some...'
        }); // This will throw Missing parameter "url"
    }

## Classes ##

    class User {
        constructor(username, email) {
            this.username = username;
            this.email = email;
        }

        static register(username, email) {
            return new User(username, email);          
        }

        static registerFancy(...args) { // rest
            return new User(...args);   // spread       
        }

        changeEmail(newEmail) {
            this.email = newEmail;
        }

        get foo() {
            return 'foo';
        }

        // set accessor
        set foo() {
            return 'foo';
        }
    }

    let user = new User('Jason', 'some@email.com');
    user.changeEmail('another@email.com');
    User.register('Jason', 'some@email.com');
    user.foo(); // get accessor


### Other classes notes ###

Classes are first class citizens;

    function log(strategy) {
        strategy. handle();
    }

    log (new class { // anonymous class
        handle() {
            alert('Using the alert strategy to log.');
        }
    }); 

## ES6 Modules ##

    //TaskCollection.js
    export class TaskCollection {
        constructor(tasks=[]) {
            this.tasks = tasks;
        }
        dump() {
            console.log(this.tasks)
        }
    }
    export let foo = 'bar';
    // You could also do...
    export default TaskCollection;
    // And calling it will be as...
    import TaskCollection from './TaskCollection';
    // Or...
    // someOtherFile.js
    import { TaskCollection, foo } from './TaskCollection';

You can also use alias;

    import { TaskCollection as TskC, foo } from './TaskCollection'; 

Import everything into an object;

    import * as addition from './TaskCollection';
    // is now used as;
    addition.TaskCollection();

Importing packages is even easier;
If you installed lodash for example with npm; Now just do;

    import * as _ from 'lodash';

## More usage examples of modules ##

    import React, { Component, PropTypes } from 'react';

This says:

> Import the **default** export under the name `React` and import the **named** exports `Component` and `PropTypes` under the same names.

This combines the two common syntaxes which you've probably seen

    import React from 'react';
    import { Component, PropTypes } from 'react';

The first being used to import and name the default export, the second to import the specified named exports.

As a general rule, most modules will either provide a single, default export, or a list of named exports. It is slightly less usual for a module to provide both a default export **and** named exports. However, in the case where there is one feature which is most commonly imported, but also additional sub-features, it is a valid design to export the first as the default, and the remaining ones as named exports. It is in such cases you would use the `import` syntax you refer to.

## Promises ##

a Holding spot for an operation that has not yet taken place. Its a promise to perform the action.

    let some_promise = new Promise(function(resolve, reject) {
        if (true) {
            resolve();
        } else {
            reject();
        }
    });

    some_promise
    .then(console.log('It was resolved...'))
    .catch(console.log('It was rejected :('));

Or do it this way...

    let timer = function(length) {
        return new Promise((resolve, reject) => {
            setTimeout(function() {
                resolve()
            }, length);
        });
    }

    timer(400).then(() => alert('All Done'));

## String Additions ##

Some new additions to the string API.

    let title = 'Red Rising';

Does string have red?

    if (title.includes('Red')) {
        // Is true...
    }

Does string starts with red?

    if (title.startsWith('Red')) {
        // Is true...
    }

    // Also endsWith...
    // Also title.startsWith('Red', 5) // Offsets with 5

Repeating somethings... pretty darn cool.

    let str = 'lol';
    str.repeat(10) // lolololololol....
    
## Array Additions ##

[See Array Additions](ES6-arrays.md)

## Class Helpers... ##

    class User {
        constructor (name, isAdmin) {
            this.name = name;
            this.isAdmin = isAdmin;
        }
    }

    let users = {
        new User('Jason', false),
        new User('Peter', false),
        new User('Susan', true)
    }

    users.find(user => user.isAdmin); // Will return the Susan object.

Also see...

    [].fill();
    [].keys();
    [].values();
    [].entries();

Convert an array-like object into an Array with Array.from()

    Array.from(arrayLikeObject); // becomes an array.

## Maps and WeakMaps ##

The Map object is just a simple key, value map. Maps have the advantage of;

* By default, maps have keys.
* Maps can contain, function, strings, keys and other primitives.
* Maps have helper methods to keep size of objects etc.

Here are a some examples;

    let myMap = new Map();
    // API
    /*
    set()
    get()
    size
    clear()
    has()
    */
    // Setting
    myMap.set('foo', 'bar');
    myMap.set('hello', world);
    console.log(myMap.get('foo')); //bar
    myMap.has('foo'); //true
    // Iterators
    // keys()
    // entries()
    // values
    for (let key of myMap.keys()) {
        console.log(key); // foo, hello        
    }
    for (let [key, value] of myMap.entries()) {
        console.log(key + value); // as expected      
    }

Weakmaps (No references are held to the keys of the map (immutable));

    let myMap = new WeakMap();
    // Cannot iterate, not can strings be used as keys.

## Generators ##

It allows a function to exit or pause and then resume at a particular part. Use generators to iterate any data structure with "for of" loops.

    function* numbers() {
        console.log('Will show once');
        yield 1; // Then stop here.
        yield 2;
        yield 3;
    }

    let iterator = numbers();
    console.log(iterator.next()); // {value: 1, done: false} // Will show once
    console.log(iterator.next()); // {value: 2, done: false}
    console.log(iterator.next()); // {value: 3, done: false}

Another example...

    function* range(start, end) {
        while (start <= end) {
            yield start;
            start ++;
        }
    }

    let iterator = range(1, 5);

    console.log(iterator.next()); // {value: 1, done: false}
    console.log(iterator.next()); // {value: 2, done: false}
    ...
    console.log(iterator.next()); // {value: 5, done: false}
    console.log(iterator.next()); // {value: undefined, done: true}

Or 
    
    for (let i of iterator) console.log(i); // 1 - 5
    console.log([..range]);
    
Practical generator use

    const engineeringTeam = {
      size: 3,
      department: 'Engineering',
      lead: 'Jill',
      manager: 'Alex',
      engineering: 'Dave',
    };
    
    function* TeamIterator(team) {
      yield team.lead;
      yield team.manager;
      yield team.engineer;
    }
    
    const names = [];
    for (let name of TeamIterator(EngineeringTeam)) {
      names.push(name); // ["Jill", "Alex", "Dave"]
    }

Some notes:

`[Symbol.iterator]` can be used inside an object to iterate from, this also also you to call consecutive operators that follows.

## Sets ##

Sets are almost like dictionaries.

    let items = new Set(['one', 'two', 'three', 'two']); 
    console.log(items) // {'one', 'two', 'three'}

    items.size // 3
    items.add("four"); 
    items.delete("two");
    items.has("four");
    items.clear();

**Usage Example:**

* Unique items like tags.

# Guide to Currying in Functional JavaScript #

Currying is a functional programming concept that allows you to pass a arguments a function is expecting and get the result as a function, allowing you to pass the rest of the parameters to the second function returned building upon the first subset.

If you are frequently "refining" a high-level function by calling it with same configuration, you can curry (or use Resig's partial) the higher-level function to create simple, concise helper methods.

    var greetCurried = function(greeting) {
        return function(name) {
        console.log(greeting + ", " + name);
      };
    };

The way we wrote the function lets us create a new function for any type of greeting, and pass that new function the name of the person that we want to greet:

    var greetHello = greetCurried("Hello");
    greetHello("Heidi"); //"Hello, Heidi"
    greetHello("Eddie"); //"Hello, Eddie"

We can also call the original curried function directly, just by passing each of the parameters in a separate set of parentheses, one right after the other:

    greetCurried("Hi there")("Howard"); //"Hi there, Howard"

The cool thing is, now that we have learned how to modify our traditional function to use this approach for dealing with arguments, we can do this with as many arguments as we want:

    var greetDeeplyCurried = function(greeting) {
      return function(separator) {
        return function(emphasis) {
          return function(name) {
            console.log(greeting + separator + name + emphasis);
          };
        };
      };
    };

We have the same flexibility with four arguments as we have with two. No matter how far the nesting goes, we can create new custom functions to greet as many people as we choose in as many ways as suits our purposes:

    var greetAwkwardly = greetDeeplyCurried("Hello")("...")("?");
    greetAwkwardly("Heidi"); //"Hello...Heidi?"
    greetAwkwardly("Eddie"); //"Hello...Eddie?"

What’s more, we can pass as many parameters as we like when creating custom variations on our original curried function, creating new functions that are able to take the appropriate number of additional parameters, each passed separately in its own set of parentheses:

    var sayHello = greetDeeplyCurried("Hello")(", ");
    sayHello(".")("Heidi"); //"Hello, Heidi."
    sayHello(".")("Eddie"); //"Hello, Eddie."

And we can define subordinate variations just as easily:

    var askHello = sayHello("?");
    askHello("Heidi"); //"Hello, Heidi?"
    askHello("Eddie"); //"Hello, Eddie?"

[For more see this post.](https://www.sitepoint.com/currying-in-functional-javascript/)
[Also](https://medium.com/@kbrainwave/currying-in-javascript-ce6da2d324fe#.kh4vnxfa0)

# Tools and Helpful notes on Javascript Development #

Listing here is a list of usefullness to get you started in the right direct.
The *** will indicate the desired option, more starts means more desirable.

### IDEs ###

- PHPStorm**, Webstorm***, IntelliJ**
- Atom.io
- Sublime
- Brackets.io

### NPM ###

(Node Package Manager) This you will need to install all your js packages from.

    sudo apt-get install -y npm

Check for outdated packages with:

    sudo npm outdated -g --depth=0


### npm-check ###

Nice module to check all dependencies and newer versions of packages in your local npm package file.

// Some other useful commands:

    npm-check // Identify unused and dated packages.
    npm uninstall <module> --save
    npm install <module> --save
    npm install <module> --save // for development dependencies
    npm outdated // Will check for for outdated packages
    npm update --save <module>@1.0.0 // for latest...

## Module Bundling ##

Module bundling simply allows us to use es6 "import" functionality in current browsers. This will also allow us to handle dependencies in a single file.

Basically it takes all the functions, methods etc. you need and rolls it up into one file.

- rollup (lighter and easier than webpack) ***
- webpack ***

**Note:** React-Native has its own module bundler and compiler, and you do not have to worry about these things.

[Video](https://laracasts.com/series/es6-cliffsnotes/episodes/11?autoplay=true)

### Compilers ###

Compilers will convert ES6 to ES5 because not all browsers yet understand ES6. Note that the bundler (rollup, webpack) first needs to run then call the compiler.

- babel (The older most advanced compiler)
- buble (Cleaner output...)

To use with rollup for instance, you would install:

    npm install --save-dev rollup-plugin-buble

**AGAIN Note:** React-Native has its own module bundler and compiler, and you do not have to worry about these things.

## Immutable Prevention ##

These modules prevents objects from ever changes;

- deepFreeze.js
- Immutable.js

## React Framework Support ##

These tools make the frameworks like React.js complete. Below is a list of state management, to keep track of the application state.

- Mobx * (Small powerful, easy)
- Flux **
- Redux ***
- Relay ** (For very large applications)
- create-react-app (Gets you going quickly...)

## Unit Testing ##

To unit test your code.

- [Jest (from Facebook)](https://3sidedcube.com/blog/2016/05/react-native-unit-testing/)
- Mocha
- Jasmine
- Karma
- enzyme
- expect (michael jackson)

## Setting up ES6 for browser using Rollup ##

[See this tutorial](https://code.lengstorf.com/learn-rollup-js/)

    npm install --save-dev rollup buble rollup-plugin-buble rollup-plugin-eslint eslint rollup-plugin-node-resolve rollup-plugin-commonjs rollup-plugin-replace rollup-plugin-uglify

Setup eslint with this command;

    ./node_modules/.bin/eslint --init

Run with:

    NODE_ENV=production ./node_modules/.bin/rollup -c

Config at the end will look something like this:

    import buble from 'rollup-plugin-buble';
    import eslint from 'rollup-plugin-eslint';
    import resolve from 'rollup-plugin-node-resolve';
    import commonjs from 'rollup-plugin-commonjs';
    import replace from 'rollup-plugin-replace';
    import uglify from 'rollup-plugin-uglify';
    export default {
        entry: 'src/scripts/main.js',
        dest: 'build/js/main.min.js',
        format: 'iife',
        sourceMap: 'inline',
        plugins: [
            resolve({
                jsnext: true,
                main: true,
                browser: true
            }),
            commonjs(),
            eslint({
                exclude: 'src/styles/**'
            }),
            buble(),
            replace({
                ENV: JSON.stringify(process.env.NODE_ENV || 'development')
            }),
            (process.env.NODE_ENV == 'production' && uglify())
        ],
    };