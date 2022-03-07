# JS CHEATSHEAT

## Variables in JS

JS is a loosely-typed language. You don't have to state the type of variable. You can just declare it, and JS will figure it out on its own.

In JavaScript we have 3 ways to declare variables: `var`, `let`, and `const`.

#### Differences!

| `var`                           | `let`                                | `const`                              |
| ------------------------------- | ------------------------------------ | ------------------------------------ |
| globally or functionally scoped | block scoped                         | block scoped                         |
| can be redeclared               | can't be redeclared within its scope | can't be redeclared within its scope |
| can be updated                  | can be updated                       | can't be updated                     |

Lets show some examples!

```js
var a = 3;
var a = 4;
console.log(a); // 4 as var variables can be redeclared + updated

let b = 3;
let b = 4;
console.log(b); // Syntax Error as let variables cannot be redeclared
b = 4;
// If we just do, it will work because it can be updated

const c = 3;
const c = 4;
console.log(c); // Syntax Error as const variables cannot be redeclared or updated
```

## Value types (data types) in JS

The set of types in the JavaScript language consists of **primitive** values and **objects**.

- Primitive values (immutable datum represented directly at the lowest level of the language)
  - Boolean type
  - Null type
  - Undefined type
  - Number type
  - BigInt type
  - String type
  - Symbol type
- Objects (collections of properties)

[Check more here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#primitive_values)

## Arrays and Array Methods

Arrays are used for storing multiple values. It can contain multiple different types of values.

```js
let a = 4;
const b = 5;
var c = 'hello';

const array = [a, b, c];

// or like this
const arr = [4, 5, 'hello'];
```

There are a lot of methods that we can use on a array. The most frequently used are: `map`, `filter`, `reduce`, `find` and `forEach`.

If using React you'll mostly work with `map` and `reduce`.

**disclaimer** - `map`, `reduce` & `filter` create new array. `forEach` doesn't. `find` doesn't mutate array by default, bud provided callback can mutate it!

### The `map` array method

`map` iterates over the original array and takes a callback function as an argument. In the callback function, we tell it what to do with the elements.

```js
const a = [1, 2, 3, 4, 5];

// Create a new array which multiplies every element by 2
const d = a.map((item) => item * 2);

console.log(d); // [2,4,6,8,10]
```

### The `reduce` array method

The `reduce` method can combine the items of an array into a single value. When using `reduce`, we must declare the accumulator's beginning value (final result). Each iteration, we do some operation inside the callback, which is then added to the accumulator.

```js
var arr = [10, 20, 30];
var counter = 0;
let answer = arr.reduce((accumulator, value) => value + accumulator, counter);
console.log(answer); // answer = 10 + 20 + 30 = 60
```

### The `filter` array method

`filter` creates a new array with elements that meet the given condition(s).

```js
// Return the words with more than 6 letters
const words = ['react', 'script', 'interview', 'style', 'javascript'];

const ans = words.filter((word) => word.length > 6);

console.log(ans); // ['interview', 'javascript']
```

## `==` vs `===` in JS

Let's compare some variables. There are two ways you can do that.

`==` only checks for the value

`===` checks for value + type

```js
let a = 5; // number
let b = '5'; // string

console.log(a == b); // true

console.log(a === b); // false
```

## Function Scope in JavaScript

Scope determines from where the variables are accessible.

There are three types of scope:

- Global (declaration outside of any function)
- Function (declaration inside a function)
- Block (declaration inside a block)

```js
var a = 5; // we can access this a anywhere

function adder() {
  let b = 7;
  console.log(a + b);
}

console.log(adder());

console.log(b); // Error as b is not accessible outside the function

{
  const c = 10;
  console.log(c); // 10
}

console.log(c); // Error as c is not accessible outside the block
```

## JS objects

Just like arrays, objects are a way of storing data. We do so with the help of key-value pairs.

```js
const developer = {
  name: 'John',
  age: 25,
};
```

In this case name is the key and John is the value. Keys are generally the name of the properties of the object.

When trying to access a JS object property that has not been defined yet, the value of `undefined` will be returned by default. Important thing is that JavaScript objects are mutable, meaning their contents can be changed, even when they are declared as `const`. New properties can be added, and existing property values can be changed or deleted.

It is the reference to the object, bound to the variable, that cannot be changed.

```js
const student = {
  name: 'Sheldon',
  score: 100,
  grade: 'A',
};

console.log(student);
// { name: 'Sheldon', score: 100, grade: 'A' }

delete student.score;
student.grade = 'F';
console.log(student);
// { name: 'Sheldon', grade: 'F' }

student = {};
// TypeError: Assignment to constant variable.
```

### Passing objects as arguments

When JavaScript objects are passed as arguments to functions or methods, they are passed by reference, not by value. This means that the object itself (not a copy) is accessible and mutable (can be changed) inside that function.

```js
const origNum = 8;
const origObj = { color: 'blue' };

const changeItUp = (num, obj) => {
  num = 7;
  obj.color = 'red';
};

changeItUp(origNum, origObj);

// Will output 8 since integers are passed by value.
console.log(origNum);

// Will output 'red' since objects are passed
// by reference and are therefore mutable.
console.log(origObj.color);
```

All on Object type check [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

## What is `this` in JS?

In a program, at times, we need a way to point at stuff. Like saying this function right here belongs to this object. `this` helps us get this context. Lets go step by step.

In `.js` file add `console.log(this)`. It will point to a `window` object (because this is a global context).

Next, create new object.

```js
function myFunc() {
  console.log(this);
}

const obj = {
  bool: true,
  myFunc: myFunc,
};

obj.myFunc();
```

`this` will now point to this object. Why? Because you binded it to object `obj` and changed its context. In a case before we did **`implicit binding`**. There is another way to use `this`. Explicit binding is when you force a function to use a certain object as its `this`.

Why would you use explicit biding? Look at this:

```js
const quman_1 = {
  name: 'Quman1',
  displayName_1: function displayName() {
    console.log(this.name);
  },
};
const quman_2 = {
  name: 'Quman2',
  displayName_1: function displayName() {
    console.log(this.name);
  },
};

quman_1.displayName_1();
quman_2.displayName_2();
```

This is all good, but we added 5 lines of repeatable code, which is a big no-no. For this we can bind context to a object.

```js
quman_1.displayName_1.call(quman_2); // Quman2
```

### Ways of binding in JS

|           | call()        | apply()   | bind()            |
| --------- | ------------- | --------- | ----------------- |
| excution  | instantly     | instantly | assign, use after |
| parametar | list of items | array     | list              |

This works different in arrow functions (we will touch them later). For an arrow function, the value depends on the lexical scope – that is to say, the outer function where the arrow function is declared.

So, if we make the `displayName()` from above an arrow function, nothing will work.

Arrow functions basically inherit the parent's context which in the above case is the `window`.

### Prototypes and Prototypal Inheritance in JS

"Whenever we create anything (like an object or function) in JavaScript, the JS Engine automatically attaches that thing with some properties and methods."

All this comes via `prototypes`. `__proto__` is the object where JS is putting it all.

```js
let arr = ['val1', 'val2'];
console.log(arr.__proto__.forEach);
console.log(arr.__proto__); // same as Array.prototype
console.log(arr.__proto__.__proto__); // same as Object.prototype
```

In JS, behind the scenes, you will always find `Object.prototype`. That is why we say that everything in JS is an object. :smile:

Simply put, prototypical inheritance refers to the ability to access object properties from another object. We use a JavaScript prototype to add new properties and methods to an existing object constructor. We can then essentially tell our JS code to inherit properties from a prototype. Prototypical inheritance allows us to reuse the properties or methods from one JavaScript object to another through a reference pointer function.

All JavaScript objects inherit properties and methods from a prototype:

- `Date` objects inherit from `Date.prototype`.
- `Array` objects inherit from `Array.prototype`.

The `Object.prototype` is on top of the prototype inheritance chain. All object inherit from `Object.prototype`. Check this (don't modify prototypes this way. It is wrong, look here for ["true" and proper inheritance](https://javascript.plainenglish.io/how-prototypal-inheritance-works-in-javascript-and-how-to-convert-it-to-class-based-inheritance-632e31e6350d) )

```js
let object = {
  name: 'Qman',
  city: 'Zagreb',
  getIntro: function () {
    console.log(`${this.name}, ${this.city}`);
  },
};

let object2 = {
  name: 'Jenz',
};

object2.__proto__ = object;

console.log(object2.city);
```

By doing this, `object2` gets access to the object's properties so this will work. We inherited "Zagreb" from "object" (and overwrite name in `object2`)

## Arrow functions

**History lesson:**

The ES6 is the sixth edition of the language and was released on June 2015. It was initially known as ECMAScript 6 (ES6) and later renamed to ECMAScript 2015. This edition includes many new features like class, modules, iterators, for/of loop, arrow functions, typed arrays, promises, reflection.

Arrow functions are a short-hand notation for writing functions in ES6. The arrow function definition consists of a parameter list ( ... ), followed by the =>marker and a function body. For single-argument functions, the parentheses may be omitted.

```js
// classical function
function add(a, b) {
  return a + b;
}

//arrow function
const add = (a, b) => a + b;
```

If the arrow function is implemented with “concise body” (without {}), it does not need an explicit return statement. Note the omitted { } after the => (implicit return).

Now the biggest difference from classical functions is in `this`.

Each function in JavaScript defines its own `this` context but arrow functions capture the `this` value of the nearest enclosing context.

#### All of the diffs:

- They close over this, and do not have their own versions.
- They can have a concise body (without { }) rather than a verbose one (but they can have a verbose body as well).
- They cannot be used as constructors. E.g., you can’t use new with an arrow function. Hence arrow functions do not have a prototype property on them.
- There is no generator syntax for arrow functions. E.g., there is no arrow equivalent to function `*foo() { ... }`.

# Advanced JS and tips

## Functional Programming in JavaScript

Just like how we used variables to store values, we can use functions to store a piece of code which we can reuse.

Functional progra­mming is a declar­ative paradigm of building software by composing pure functions. What is a `Pure function`?

**A pure function is a function which:**

1. Given the same input, returns the same output.
2. Has no side-e­ffects.

What is a side-effect? By definition, any operation that is not directly related to the final output of the function is called a Side Effect.

Check [this](https://blog.greenroots.info/what-are-pure-functions-and-side-effects-in-javascript) for side-effect explenation in-depth.

## Closures in JS

By MDN, Closure is "A function bundled together with its lexical environment forms a closure."

A lexical environment is basically the scope or environment the engine is currently reading code in. A new lexical environment is created when curly brackets {} are used. Check this, it is pretty easy. :smile:

```js
function x() {
  var a = 7;
  function y() {
    console.log(a);
  }
  return y;
}

var z = x();
console.log(z); // [Function: y]
z();
//this is a closure
```

So what happened?. When we invoked `z` we basically called `y`. But we invoked its reference. Now, y has to `console.log a` so it first tries to find it in the local memory but it's not there. It goes to its parent function. It finds a there. function `y` remeber its lexical scope.

This is important in functional programing because we now have something called "Currying".

### Currying

Currying is a transf­orm­ation of functions that translates a function from callable as `f(a, b, c)` into callable as `f(a)(b­)(c)`.

```js
//Add 2 numbers
const add = (x) => (y) => x + y;

console.log(add(2)(3)); // 5

//Multiply with a number
const multiply = (m) => (n) => n * m;

console.log(multiply(2)(3)); // 6
```

### Hoisting

Hoisting is JavaScript's default behavior of moving declarations to the top of the program (also very popular theme to discuss while on a job interview :smile: ).

In JavaScript, functions are fully hoisted, `var` variables are hoisted and initialized to undefined, and `let` and `const` variables are hoisted but not initialized a value. `Var` variables are given a memory allocation and initialized a value of undefined until they are set to a value in line. So if a `var` variable is used in the code before it is initialized, then it will return undefined. However, a function can be called from anywhere in the code base because it is fully hoisted. If `let` and `const` are used before they are declared, then they will throw a reference error because they have not yet been initialized.

```js
console.log(sing()); //undefined

console.log(sing2()); // ohhhh la la la

// function expression gets hoisted as undefined
var sing = function () {
  console.log('uhhhh la la la');
};
// function declaration gets fully hoisted
function sing2() {
  console.log('ohhhh la la la');
}
```

Functions can get rewritten in memory.

```js
// function declaration gets hoisted
function a() {
  console.log('hi');
}

// function declaration get rewritten in memory
function a() {
  console.log('bye');
}

console.log(a());
// bye
```

## ASYNC <3

Async or Asynchronous JavaScript allows the program to be executed immediately where the synchronous code will block further execution of the remaining code until it finishes the current one.

So, JS is a single-threaded language. Things happen one at a time. Only after one thing is done can we move to the next thing.

But this creates problems in the real world, especially, when we are working with browsers.

For example, when we need to fetch data from the web - often times we don't know how long will it take to get it. And whether we will be able to get the data successfully.

### Promises

**The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.**

A promise can be in one of these three states:

- Pending: initial state, neither fulfilled nor rejected
- Fulfilled: operation was completed successfully
- Rejected: operation failed

```js
const promise = new Promise((resolve, reject) => {
  let value = true;
  if (value) {
    resolve('hey value is true');
  } else {
    reject('there was an error, value is false');
  }
});

promise
  .then((x) => {
    console.log(x);
  })
  .catch((err) => console.log(err));
```

Why are promises important? They give much more cleaner syntax, and of course, they solve hell issue called "callback". If you did something before introduction of Promises, you will know what I'm talking about :).

PS - resolve and reject are just naming convetion. Use anything you like.

And yes, `async/await` is just synthetic sugar.

```js
async function asyncCall() {
  const result = await promise;
  console.log(result);
}
asyncCall();
```

# JS Engine

And for the end, lets go over some abstract things in JS (like advanced advanced s\*\*\*) :smile:

## Storage

**localStorage**: Data persists even after closing your session

**sessionStorage**: You lose your data when your session is over, like when you close the browser on the tab.

```js
// save
localStorage.setItem('key', 'value');
// get saved data
let data = localStorage.getItem('key');
// remove saved data
localStorage.removeItem('key');
// Same for sessionStorage
```

## Event propagation

Event propagation is a technique that governs how events propagate or travel through the DOM tree to reach their destination, as well as what happens to them once they arrive. Consider the following scenario: you have been given a click event handler to a hyperlink (i.e. `<a>` element) that's nested inside a paragraph (i.e.`<p`> element). The handler will now be executed if you click on that link. However, if you set the click event handler to the paragraph containing the link instead of the link, the handler will be triggered regardless of whether the link is clicked. Because events go up and down the DOM tree to reach their target, they don't merely affect the target element that triggered the event. This is known as event propagation.

When an event is fired on an element with parent elements, the above picture shows how the event travels through the DOM tree at different stages of the event propagation. Event propagation in current browsers is divided into two phases: capturing and bubbling.

The Capturing Phase: In the capturing phase, events propagate from the Window down through the DOM tree to the target node. For example, if the user clicks a hyperlink, that click event would pass through the `<html>` element, the `<body>` element, and the `<p>` element containing the link. Also if any ancestor (i.e. parent, grandparent, etc.) of the target element and the target itself has a specially registered capturing event listener for that type of event, those listeners are executed during this phase.
The Bubbling Phase: From the target element up to the Window, the DOM tree visits all of the target element's ancestors one by one. When a user hits a hyperlink, the click event passes via the `<p>` element containing the link, the `<body>` element, the `<html>` element, and the document node, for example. Additionally, if the target element or any of its ancestors have event handlers for that sort of event, those handlers are run during this phase. By default, all event handlers in current browsers are registered at the bubbling phase.

## JavaScript Memory Allocation and Event Loop

In JavaScript, memory allocation is done in the following regions:

- **Heap memory**: Data is stored in random order and memory is allocated accordingly.
- **Stack memory**: Memory that is allocated in stacks. The majority of the time, it's employed for functions.

The function stack is a function that maintains track of all other functions that are running at the same time.

```js
function second() {
  console.log('Second');
}
function First() {
  second();
}
function foo() {
  first();
}
foo();
```

The order in which functions are executed, that is. when they are popped out of the stack once their purpose is completed, is as follows:

1. console.log()
2. second()
3. first()
4. foo()

Other example is related to webApi order. Take this:

```js
console.log('1');

setTimeout(() => {
  console.log('2');
}, 0);

Promise.resolve(() => console.log('3')).then((res) => res());

console.log('4');
```

So what is the order and why?

1
4
3
2

Why? Because of the **Event loop**. An event loop is something that pulls various things like methods, etc. out of the queue and places it onto the function execution stack whenever the function stack becomes empty. The event loop is the trick to making JavaScript appear multithreaded even if it is only single-threaded. The callback function in the event queue has not yet started and is waiting for its time to be added to the stack when SetTimeOut() is called and the Web API waits. The function is loaded onto the stack when the function stack becomes empty.

The event loop is used to take the first event from the Event Queue and place it on the stack, which in this case is the callback function. If this function is called from here, it will call other functions within it.

Also `Promise` is a Macro task (priority queue), and `setTimeout` is Micro task (task queue), so `Promise` gets priority. Check here for [detailed info](https://javascript.info/event-loop)

## Memoize expensive calculations

We should always strive for optimization. One of them i memoization of a process. That means that we don't want to do something that hasn't changed already, and that we just want to return old value.

In React, for example, you have `useMemo()`.

```js
const clumsyFunction = (num1, num2) => {
  for (let i = 1; i <= 10000000; i++);

  return num1 * num2;
};

console.time('first call');
console.log(clumsyFunction(3213, 2133));
console.timeEnd('first call');

console.time('second call');
console.log(clumsyFunction(3213, 2133));
console.timeEnd('second call');
```

This will result in expesive function to render the same result twice, which is a wast of memory and time.

```js
6853329
first call: 19.564697265625 ms
6853329
second call: 12.76708984375 ms
```

How to create your own memoization.

```js
function Memoizator(fn, context) {
  const res = {};

  return function (...args) {
    var cached = JSON.stringify(args); //var bcs we need to access it in other fun

    if (!res[cached]) {
      res[cached] = fn.call(context | this, ...args); // we bind this to the function context
    }

    return res[cached];
  };
}
```

Now memoize your function and check again :smile:

```js
const memoizedClumsyFunction = Memoizator(clumsyFunction);
//...
console.log(memoizedClumsyFunction(3213, 2133));
```

## Infinite Currying

Lets say that you need to create HOF that does infinite adds. Something like this:

```js
console.log(infiniteAdd(5)(15)(3)(12)()); /// 35
```

How to do this? With Currying it is pretty simple. We add Wrapper what will handle all of this.

```js
function infiniteAdd(a) {
  return function (b) {
    if (b) return infiniteAdd(a + b); //only if we have provided new value return calculation
    return a;
  };
}
```

## Advanced `this` usage

Lets do advanced `this` thing. Say that you need to create snippet as follows:

```js
const result = calc.add(10).mult(5).sub(15).add(5);
console.log(result.total); //40
```

So we are expecting to return an object with some props.

```js
const calc = {
  total: 0, // we define total for "this" context - block
  mult(a) {
    this.total = this.total * a; // or this.total *= a
    return this; // we need to return this as a context
  },
  add(a) {
    this.total += a;
    return this;
  },
  sub(a) {
    this.total -= a;
    return this;
  },
};
```
