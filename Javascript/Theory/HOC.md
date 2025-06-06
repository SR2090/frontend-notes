---
title: What is the definition of a higher-order function in JavaScript?
---

# Higher Order Functions

Write cleaner, more abstract, and maintainable code by encapsulating common patterns such as mapping, filtering, logging, and caching.

A **higher order function** is a function that either:

- Accepts one or more functions as arguments,
- Returns a function as its result,
- Or does both.

Their main purpose is to abstract common operations that occur repeatedly in code, leading to more modular and reusable logic.

## Key Characteristics

- **Abstraction:** They encapsulate recurring operations, making your code more concise.
- **Flexibility:** They allow functions to be composed and customized at runtime.
- **Modularity:** They separate concerns, isolating specific behaviors (like logging or caching) from the core logic.

## Common Examples

- **Array Methods:**
  - **`map`**: Accepts a function that transforms each element of an array and returns a new array with the transformed values.
  - **`forEach`**: Accepts a function to execute on each element of an array.
  - **`filter`**: Accepts a function that tests each element, returning a new array with only those elements that pass the test.

- **`bind`:**
  - While not as common as the array methods in the context of higher order functions, `bind` accepts a function and returns a new function with a preset `this` value and, optionally, preset arguments.

## Practical Use Cases

- **Logging:**  
  Wrap a function to automatically log its inputs (and potentially outputs) every time it is called.  
  *Example:*  
  ```js
  function withLogging(fn) {
    return function (...args) {
      console.log(`Calling ${fn.name} with arguments`, args);
      return fn.apply(this, args);
    };
  }

## TL;DR

A higher-order function is any function that takes one or more functions as arguments, which it uses to operate on some data, and/or returns a function as a result.

Higher-order functions are meant to abstract some operation that is performed repeatedly. The classic example of this is `Array.prototype.map()`, which takes an array and a function as arguments. `Array.prototype.map()` then uses this function to transform each item in the array, returning a new array with the transformed data. Other popular examples in JavaScript are `Array.prototype.forEach()`, `Array.prototype.filter()`, and `Array.prototype.reduce()`. A higher-order function doesn't just need to be manipulating arrays as there are many use cases for returning a function from another function. `Function.prototype.bind()` is an example that returns another function.

Imagine a scenario where we have an array of names that we need to transform to uppercase.

```js
const names = ['irish', 'daisy', 'anna'];
```

The imperative way will be as such:

```js
function transformNamesToUppercase(names) {
  const results = [];
  for (let i = 0; i < names.length; i++) {
    results.push(names[i].toUpperCase());
  }
  return results;
}

transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```

Using `Array.prototype.map(transformerFn)` makes the code shorter and more declarative.

```js
function transformNamesToUppercase(names) {
  return names.map((name) => name.toUpperCase());
}

transformNamesToUppercase(names); // ['IRISH', 'DAISY', 'ANNA']
```

---

## Higher order functions

A higher-order function is a function that takes another function as an argument or returns a function as its result.

### Functions as arguments

A higher-order function can take another function as an argument and execute it.

```js
function greet(name) {
  return `Hello, ${name}!`;
}

function greetName(greeter, name) {
  console.log(greeter(name));
}

greetName(greet, 'Alice'); // Output: Hello, Alice!
```

In this example, the `greetName` function takes another function `greet` as an argument and executes it with the name `Alice`. The `greet` function is a higher-order function because it is passed as an argument to another function.

### Functions as return values

A higher-order function can return another function.

```js
function multiplier(factor) {
  return function (num) {
    return num * factor;
  };
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5)); // Output: 10
console.log(triple(5)); // Output: 15
```

In this example, the `multiplier` function returns a new function that multiplies any number by the specified factor. The returned function is a closure that remembers the `factor` value from the outer function. The `multiplier` function is a higher-order function because it returns another function.

### Practical examples

1. **Logging decorator**: A higher-order function that adds logging functionality to another function:

```js
function withLogging(fn) {
  return function (...args) {
    console.log(`Calling ${fn.name} with arguments`, args);
    return fn.apply(this, args);
  };
}

function add(a, b) {
  return a + b;
}

const loggedAdd = withLogging(add);
console.log(loggedAdd(2, 3)); // Output: Calling add with arguments [2, 3] 5
```

The `withLogging` function is a higher-order function that takes a function fn as an argument and returns a new function that logs the function call before executing the original function

1. **Memoization**: A higher-order function that caches the results of a function to avoid redundant computations:

```js
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) {
      return cache.get(key);
    }
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

const memoizedFibonacci = memoize(fibonacci);
console.log(memoizedFibonacci(10)); // Output: 55
```

The `memoize` function is a higher-order function that takes a function `fn` as an argument and returns a new function that caches the results of the original function based on its arguments.

1. **Lodash**: Lodash is a utility library that provides a wide range of functions for working with arrays, objects, strings, and more, most of which are higher-order functions.

```js
import _ from 'lodash';

const numbers = [1, 2, 3, 4, 5];

// Filter array
const evenNumbers = _.filter(numbers, (n) => n % 2 === 0); // [2, 4]

// Map array
const doubledNumbers = _.map(numbers, (n) => n * 2); // [2, 4, 6, 8, 10]

// Find the maximum value
const maxValue = _.max(numbers); // 5

// Sum all values
const sum = _.sum(numbers); // 15
```



### HOC In react
A logging compoennt
```jsx
const HOC = (WrappedComponent) => {

  return (props) => {

    console.log(props)

    return <WrappedComponent {...props} />

  }

}
```


```js
const EnhancedTarget = HOC(TargetComponent);
// Then in your render method or component:
<EnhancedTarget prop1={val1} />

```

Usage of this component
## Further reading

- [Higher-Order Functions](https://eloquentjavascript.net/05_higher_order.html)
- [Understanding Higher-Order Functions in JavaScript](https://blog.bitsrc.io/understanding-higher-order-functions-in-javascript-75461803bad)
- [Higher Order Functions: How to Use Filter, Map and Reduce for More Maintainable Code](https://www.freecodecamp.org/news/higher-order-functions-in-javascript-d9101f9cf528/)