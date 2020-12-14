---
title: "Javascript Refresher"
date: 2020-12-13T00:33:04-08:00
draft: true
---

# `let` and `const`

* `var` was the old way to create variable
* `let` and `const` are introduced in ES6
* `let` is the new `var` to create a variables
* `const` creates a constant variable; the value cannot be assigned

# Arrow functions 

* Normal function looks like
```javascript
function myFunc() {
    ...
}
```
arrow function looks like
```javascript
const myfunc = () => {
    ...
}
```
No more issues with the `this` keyword.
* Lambda function 
```javascript
const multiply = number => number * 2;
```

# Exports and imports (Modules)

* `export` keyword; `export default` can be named differently. When importing, `import person from './person.js'`.
* use named import, e.g., `import {baseData} from './utils.js'

# Classes

* `constructor()` function
* `extends` keyword to inherit from another class

# Classes, properties & methods

* ES7 way (no `this` issue)
  * set a property
  ```javascript
    myProperty = 'value';
  ```
  * set a method 
  ```javascript
    myMethod = () => {...}
  ```

# Spread & rest operators

* operator `...`
* spread - used to split up array elements OR object properties
```javascript
const newArray = [..oldArray, 1, 2];
const newObject = {...oldObject, newProp: 5}
```
* rest - used to merge a list of function arguments into an array
```javascript
function sortArgs(...args) {
    return args.sort();
}
```











 