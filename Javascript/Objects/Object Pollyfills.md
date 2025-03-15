

## bind
```js
/** * Calls the function, substituting the specified object for the this value of the function, and the specified array for the arguments of the function. * @param thisArg The object to be used as the this object. * @param argArray A set of arguments to be passed to the function. * @return {any} */ Function.prototype.myApply = function (thisArg, argArray) { const wrappedObject = Object(thisArg); const uniqueIdentifier = Symbol() Object.defineProperty(wrappedObject, uniqueIdentifier, { value: this, enumerable: false }) return wrappedObject[uniqueIdentifier](...argArray); };
```


He deletes the context to get back the value.
### Answers
```js
// Question
// Asked in Jio and Expedia
// Level -> Easy

// Write custome polyfill for call, apply and bind method ?




//Solution

//Polyfill for Call
Function.prototype.myCall = function (context, ...args) {
    // Ensure arguments are correct
    if (typeof this !== "function") {
      throw new TypeError("myCall must be called on a function");
    }
  
    context = context !== null && context !== undefined ? Object(context) : globalThis;
  
    const uniqueSymbol = Symbol(); // it shoud be unique
    context[uniqueSymbol] = this;
  
    // Call the function with the provided arguments
    const result = context[uniqueSymbol](...args);
  
    // Remove the unique property to avoid side effects
    delete context[uniqueSymbol];
  
    return result;
  };
  
  // Testing myCall
  function greet(name) {
    return `Hello, ${name}`;
  }
  
  const person = { name: "John" };
  console.log(greet.myCall(person, "Alice"));  



  //Polyfill for Apply
Function.prototype.myApply = function (context, args) {
    if (typeof this !== "function") {
      throw new TypeError("myApply must be called on a function");
    }
  
    // Ensure context is an object
    context = context !== null && context !== undefined ? Object(context) : globalThis;
  
    // Ensure args is an array
    if (!Array.isArray(args)) {
      throw new TypeError("The second argument must be an array");
    }
  
    const uniqueSymbol = Symbol();
    context[uniqueSymbol] = this;
  
    // Call the function with arguments spread out (if any)
    const result = context[uniqueSymbol](...args);
  
    delete context[uniqueSymbol];
  
    return result;
  };
  
  function sum(a, b) {
    return a + b;
  }
  
  const context = {};
  console.log(sum.myApply(context, [5, 10])); 



  //Polyfill for Bind
Function.prototype.myBind = function (context, ...boundArgs) {
    if (typeof this !== "function") {
      throw new TypeError("myBind must be called on a function");
    }
  
    // Ensure context is an object
    context = context !== null && context !== undefined ? Object(context) : globalThis;
  
    const fn = this;
  
    return function (...args) {
      return fn.apply(context, [...boundArgs, ...args]);
    };
  };
  
  function multiply(a, b) {
    return a * b;
  }
  
  const boundMultiply = multiply.myBind(null, 2);
  console.log(boundMultiply(3));  
  console.log(boundMultiply(4));
```




## Object Map

```js
export default function objectMap(obj, fn) {

  const result = {};

  for(const [key, value] of Object.entries(obj)) {

    result[key] = fn.call(obj, value);

  }

  return result;

}
```
Using call method is important because the this context of the function will be set to the given object. To make it more flexible we can accept a third argument.

