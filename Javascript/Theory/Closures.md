### Explanation of Closures

A **closure** in JavaScript is a function that retains access to variables from its lexical scope, even after the outer function has finished executing. This allows the inner function to "close over" the environment in which it was created, hence the name.


---
Title: What is a closure in JavaScript, and how/why would you use one?
---

## TL;DR

In the book ["You Don't Know JS"](https://github.com/getify/You-Dont-Know-JS/tree/2nd-ed/scope-closures) (YDKJS) by Kyle Simpson, a closure is defined as follows:

> Closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope

In simple terms, functions have access to variables that were in their scope at the time of their creation. This is what we call the function's lexical scope. A closure is a function that retains access to these variables even after the outer function has finished executing. This is like the function has a memory of its original environment.

```js
function outerFunction() {
  const outerVar = 'I am outside of innerFunction';

  function innerFunction() {
    console.log(outerVar); // `innerFunction` can still access `outerVar`.
  }

  return innerFunction;
}

const inner = outerFunction(); // `inner` now holds a reference to `innerFunction`.

inner(); // "I am outside of innerFunction"
// Even though `outerFunction` has completed execution, `inner` still has access to variables defined inside `outerFunction`.
```

Key points to remember:

- Closure occurs when an inner function has access to variables in its outer (lexical) scope, even when the outer function has finished executing.
- Closure allows a function to **remember** the environment in which it was created, even if that environment is no longer present.
- Closures are used extensively in JavaScript, such as in callbacks, event handlers, and asynchronous functions.

---

## Understanding JavaScript closures

In JavaScript, a closure is a function that captures the lexical scope in which it was declared, allowing it to access and manipulate variables from an outer scope even after that scope has been closed.

Here's how closures work:

1. **Lexical scoping**: JavaScript uses lexical scoping, meaning a function's access to variables is determined by its actual location within the source code.
2. **Function creation**: When a function is created, it keeps a reference to its lexical scope. This scope contains all the local variables that were in-scope at the time the closure was created.
3. **Maintaining state**: Closures are often used to maintain state in a secure way because the variables captured by the closure are not accessible outside the function.

## ES6 syntax and closures

With ES6, closures can be created using arrow functions, which provide a more concise syntax and lexically bind the `this` value. Here's an example:

```js
const createCounter = () => {
  let count = 0;
  return () => {
    count += 1;
    return count;
  };
};

const counter = createCounter();
console.log(counter()); // Outputs: 1
console.log(counter()); // Outputs: 2
```

## Closures in React

Closures are everywhere. Below code shows a simple example of increasing a counter on a button click. In this code, `handleClick` forms a closure. It has access to it's outer scope variable `count` and `setCount`

```jsx
import React, { useState } from 'react';

function Counter() {
  // Define a state variable using the useState hook
  const [count, setCount] = useState(0);

  // This handleClick function is a closure
  function handleClick() {
    // It can access the 'count' state variable
    setCount(count + 1);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}

function App() {
  return (
    <div>
      <h1>Counter App</h1>
      <Counter />
    </div>
  );
}

export default App;
```

## Why use closures?

Using closures provide the following benefits:

4. **Data encapsulation**: Closures provide a way to create private variables and functions that can't be accessed from outside the closure. This is useful for hiding implementation details and maintaining state in an encapsulated way.
5. **Functional programming**: Closures are fundamental in functional programming paradigms, where they are used to create functions that can be passed around and invoked later, retaining access to the scope in which they were created, e.g. [partial applications or currying](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.l4b6l1i3x).
6. **Event handlers and callbacks**: In JavaScript, closures are often used in event handlers and callbacks to maintain state or access variables that were in scope when the handler or callback was defined.
7. **Module patterns**: Closures enable the [module pattern](https://www.patterns.dev/vanilla/module-pattern) in JavaScript, allowing the creation of modules with private and public parts.

## Further reading

- [Closures - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [Closures - Javascript.info](https://javascript.info/closure)
- [Closure - Eloquent Javascript](https://eloquentjavascript.net/03_functions.html)
- [You Don't Know JS Yet: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/tree/2nd-ed/scope-closures)
- 