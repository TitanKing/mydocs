# Redux.js module to obtain functional programming #

Redux provides a state container for JavaScript applications that will help your applications behave consistently.

[Read Notes](https://github.com/tayiorbeii/egghead.io_redux_course_notes)
[See Documentation](http://redux.js.org/docs/introduction/Motivation.html)

## Notes & Motivation ##

### The application state ###

* State can include server responses and cached data, as well as locally created data that has not yet been persisted to the server.
* UI State is also included in the state.

### The three principles ###

Redux can be described in three fundamental principles:

#### Single source of truth ####

The state of your whole application is stored in an object tree within a single store.

    console.log(store.getState())
    /* Prints
    {
      visibilityFilter: 'SHOW_ALL',
      todos: [
        {
          text: 'Consider using Redux',
          completed: true,
        },
        {
          text: 'Keep all state in a single tree',
          completed: false
        }
      ]
    }
    */

#### State is read-only ####

The only way to change the state is to emit an action, an object describing what happened.

    store.dispatch({
      type: 'COMPLETE_TODO',
      index: 1
    })

    store.dispatch({
      type: 'SET_VISIBILITY_FILTER',
      filter: 'SHOW_COMPLETED'
    })

#### Changes are made with pure functions ####

To specify how the state tree is transformed by actions, you write pure reducers.

Reducers are just pure functions that take the previous state and an action, and return the next state. Remember to return new state objects, instead of mutating the previous state. You can start with a single reducer, and as your app grows, split it off into smaller reducers that manage specific parts of the state tree.    
    
    function visibilityFilter(state = 'SHOW_ALL', action) {
      switch (action.type) {
        case 'SET_VISIBILITY_FILTER':
          return action.filter
        default:
          return state
      }
    }

    function todos(state = [], action) {
      switch (action.type) {
        case 'ADD_TODO':
          return [
            ...state,
            {
              text: action.text,
              completed: false
            }
          ]
        case 'COMPLETE_TODO':
          return state.map((todo, index) => {
            if (index === action.index) {
              return Object.assign({}, todo, {
                completed: true
              })
            }
            return todo
          })
        default:
          return state
      }
    }

    import { combineReducers, createStore } from 'redux'
    let reducer = combineReducers({ visibilityFilter, todos })
    let store = createStore(reducer)

## Describing state changes by actions ##

Your whole applications state will be contained in the state tree.
The state tree is redundant you cannot change it nor write to it. 

When you want to change the state you need to dispatch an object.

The action has a type property:

    {
        type: "INCREMENT/DECREMENT/SAVE/ADD_SOMETHING"
    }

An action is a plain javascript object describing in a minimum way what changed in the application.

Nothing can happen without an action.

## Some interesting javascript gotchas ##

    (function someFunc(val) {
        console.log(val); // Will run and log // SomeValue
    })('SomeValue');

    
# 01. The Single Immutable State Tree
[Video Link](https://egghead.io/lessons/javascript-redux-the-single-immutable-state-tree?series=getting-started-with-redux)

The first principle of Redux (no matter the complexity):

**The entire state of the application will be represented by one JavaScript object.**

All changes and mutations to the application are explicit.
These mutations, which include the data and the UI state, are contained in a single object we call the **state**. 

Since the entire state is represented in a single object, we are able to keep track of changes over time 

# 02. Describing State Changes with Actions
[Video Link](https://egghead.io/lessons/javascript-redux-describing-state-changes-with-actions?series=getting-started-with-redux)

The second principle of Redux is that **the *state tree* is read only**.
Any time you want to change the state, you have to dispatch an **action**. An action is a plain JS object describing the change. Just like the state is the minimal representation of the data, the action is the minimal representation of the change to that data.

The only requirement for an action is that it has a type property (conventionally a String). 

For example, in a counter app, there are `INCREMENT` and `DECREMENT` actions. In the case of a ToDo app, the display components don't know how an item was added to the list-- all they know is that an `ADD_TODO` action was dispatched, with `text` content "hey" and a sequential `id`.

The overall principle here is that the state is read only, and can only be modified by dispatching actions.

# 03. Pure and Impure Functions
[Video Link](https://egghead.io/lessons/javascript-redux-pure-and-impure-functions)

Before learning more about Redux, it's important to know the difference between "Pure" and "Impure" functions.

**Pure:**
```JavaScript
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square);
}
```
Pure functions are those whose return values depend only upon the values of their arguments. Pure functions don't have side effects like network or database calls. Pure functions also do not override the values of anything. In the above example, a new array is returned instead of modifying the `items` that was passed in.

**Impure:**
```JavaScript
function square(x) {
  updateXInDatabase(x);
  return x * x;
}
function squareAll(items) {
  for (let i = 0; i < items.length; i++) {
    items[i] = square(items[i]);
  }
}
```
Contrast the "Impure" function. A database is called, and values passed in are being overwritten. 

This distinction is important to understand, since Redux requires that certain functions are pure.

# 04. The Reducer Function
[Video Link](https://egghead.io/lessons/javascript-redux-the-reducer-function)

React introduced the idea that the UI layer is most predictable when it is described as a pure function of the application's state.

Redux compliments this approach by requiring that state mutations in your app need to be described by a pure function that takes the previous state and the action being dispatched, and returns the next state of your application.

**Inside a Redux application there is one particular function that takes the previous state and the action being dispatched, and returns the next state of the whole application**. It is important that the function is pure (i.e. the state being given to it isn't modified) because it has to return the new object representing the application's new state.

Even in large applications, there is still just a single function that calculates the new state of the application. It doesn't have to be slow-- if certain parts of the state haven't changed, their references can stay as-is. In the ToDo app example, when changing the visibility between "All/Completed/Active" the actual items themselves haven't changed, so the reference to the previous version of the `todos` array is left intact.

This is the 3rd and final principle of Redux: to describe state mutations you have to write a function that takes the previous state of the app and the action being dispatched, then returns the next state of the app. This function is called the **Reducer**.

# 05. Writing a Counter Reducer with Tests
[Video Link](https://egghead.io/lessons/javascript-redux-writing-a-counter-reducer-with-tests)

The first function we will write is the reducer for the counter example.
We will also use the `expect` library to make assertions.

```JavaScript
function counter(state, action) {
  if (typeof state === 'undefined') {
    return 0; // If state is undefined, return the initial application state
  }

  if (action.type === 'INCREMENT') {
    return state + 1;
  } else if (action.type === 'DECREMENT') {
    return state - 1;
  } else {
    return state; // In case an action is passed in we don't understand
  }
}

expect (
  counter(0, { type: 'INCREMENT' })
).toEqual(1);

expect (
  counter(1, { type: 'INCREMENT' })
).toEqual(2);

expect (
  counter(2, { type: 'DECREMENT' })
).toEqual(1);

expect (
  counter(1, { type: 'DECREMENT' })
).toEqual(0);

expect (
    counter(1, { type: 'SOMETHING_ELSE' })
).toEqual(1);
```
When writing a reducer, if `state` is not defined, return an object representing the initial state. In this counter example, we return `0` since our count will start from there. If the `action` being passed in isn't one the reducer recognizes, we just return the current `state`.

The above code can be rewritten more concisely using ES6 notation and a switch statement:

```JavaScript
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

// ... `expect` statements as above ...
```

# 06. Store Methods: `getState()`, `dispatch()`, and `subscribe()`
[Video Link](https://egghead.io/lessons/javascript-redux-store-methods-getstate-dispatch-and-subscribe)

This section makes use of functions built into Redux. We bring in `createStore` using the ES6 destructuring syntax.

```JavaScript
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

const { createStore } = Redux; // Redux CDN import syntax
// import { createStore } from 'redux' // npm module syntax

const store = createStore(counter);

```
The store binds together the 3 principles of Redux:
1. Holds the current application state object
2. Allows you to dispatch actions
3. When you create it, you need to specify the reducer that tells how state is updated with actions.

In this example, we call `createStore` with `counter` as the reducer that manages the `state` updates.

#### `store` has 3 important methods:
1. `getState()` retrieves the current state of the Redux store. If we ran `console.log(store.getState())` with the code above, we could get `0` since it is the initial state of our application.

2. `dispatch()` is the most commonly used. It is how we dispatch actions to change the state of the application. If we run `store.dispatch( { type: 'INCREMENT' });` followed by `console.log(store.getState());` we will get `1` since

3. `subscribe()` registers a callback that the redux store will call any time an action has been dispatched so you can update the UI of your application to reflect the current application state.

```JavaScript
// ... `counter` reducer as above ...

const { createStore } = Redux;
const store = createStore(counter);

store.subscribe(() => {
  document.body.innerText = store.getState();
});

document.addEventListener('click', () => {
    store.dispatch({ type : 'INCREMENT' })
});
```

The way the code is above, the initial state (`0`) is not rendered to the body, as the rendering occurs in the subscribe callback. This can be remedied by refactoring like so:

```JavaScript
const render = () => {
  document.body.innerText = store.getState();
};

store.subscribe(render);
render(); // calling once to render the initial state (0), then the subscribe will update subsequently

document.addEventListener('click', () => {
    store.dispatch({ type : 'INCREMENT' })
});
```
