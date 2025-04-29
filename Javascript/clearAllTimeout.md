```js
// Question
// Asked in Dream11
// Level ->> Medium

// Write a polyfill for clearAllTimeout that tracks and clears all timeouts set
// using setTimeout.

// // Test
// const timeout1 = setTimeout(() => console.log("Timeout 1"), 10000);
// const timeout2 = setTimeout(() => console.log("Timeout 2"), 3000);
// const timeout3 = setTimeout(() => console.log("Timeout 3"), 4000);

// setTimeout(() => {
//   console.log("Clearing all timeouts...");
//   clearAllTimeout();
// }, 5000); // This should clear all timeouts before they execute

// // Timeout 2
// // Timeout 3






//Solution
// we are storing original function in a variable and overriding setTimeOut
// with custom functionality

//Using IIFE
(function () {
  let timeouts = [];

  // set original setTimeout in a variable
  const originalSetTimeout = this.setTimeout;

  // modify original setTimeOut
  this.setTimeout = function (callback, delay, ...args) {
    const timeoutId = originalSetTimeout(callback, delay, ...args);
    timeouts.push(timeoutId); // Store the timeout ID
    return timeoutId;
  };

  // Define clearAllTimeout to clear all timeouts
  this.clearAllTimeout = function () {
    timeouts.forEach((value, timeoutId) => {
      this.clearTimeout(timeoutId); // Clear each timeout
    });
    timeouts = [];
  };
})();
```


Due to the concept of closure the timeouts variable will be accessible within both the functions which makes  doing the one below not required unless we need to have access to the array outside of this scope.

```js
// Write a polyfill for clearAllTimeout that tracks and clears all timeouts set
// using setTimeout.
(function() {
    const originalSetimeout = this.setTimeout;
    const timeouts = []
    this.setTimeout = function(func, delay, ...args) {
        let timeOut = originalSetimeout(() => func.apply(this, args), delay);
        timeouts.push(timeOut)
        return timeOut;
    }
    this.timeouts = timeouts;
    this.clearAllTimeout = function() {
        this.timeouts.forEach((item) => clearTimeout(item))
    }
})()
// // Test
const timeout1 = setTimeout(() => console.log("Timeout 1"), 10000);
const timeout2 = setTimeout(() => console.log("Timeout 2"), 3000);
const timeout3 = setTimeout(() => console.log("Timeout 3"), 4000);

setTimeout(() => {
  console.log("Clearing all timeouts...");
  clearAllTimeout();
}, 1000); // This should clear all timeouts before they execute
// // Timeout 2
// // Timeout 3

```




### Fluff 
Question 


If i do not save timeouts in the this object which can be global or window depending on env. Then how can timeouts be available inside of setTimeout and inside of clearTimeout
Yes, exactly. When you use an IIFE (Immediately Invoked Function Expression), it creates a new lexical scope. Variables like `timeouts` defined within that scope are accessible to all inner functions defined within the same IIFE—even after the IIFE has executed. This is due to JavaScript closures.

Since both the modified `setTimeout` and `clearAllTimeout` functions are defined inside that same IIFE, they capture the `timeouts` variable in their closures. This means they can both access and modify `timeouts` without needing it to be a property of the global object (or `this`).

To summarize:

- **IIFE and Lexical Scope:** The IIFE creates a local scope that holds the `timeouts` array.
- **Closures:** The functions defined within the IIFE (your custom `setTimeout` and `clearAllTimeout`) form closures over the `timeouts` variable, allowing them to access it even after the IIFE's initial execution.
- **No Need to Attach to `this`:** Since the `timeouts` variable is available in the closure, there's no need to attach it to the global object (`this` or `window`), unless you need to access it externally.

This is why both versions work, even though your version doesn't attach `timeouts` to `this` for later access.
