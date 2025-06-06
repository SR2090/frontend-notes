## TL;DR

There are multiple ways to iterate over object properties as well as arrays in JavaScript:

**`for...in` loop**

The `for...in` loop iterates over all enumerable properties of an object, including inherited enumerable properties. So it is important to have a check if you only want to iterate over object's own properties

const obj = {

  a: 1,

  b: 2,

  c: 3,

};

for (const key in obj) {

  // Optional: to avoid iterating over inherited properties

  if (obj.hasOwn(obj, key)) {

    console.log(`${key}: ${obj[key]}`);

  }

}

**`Object.keys()`**

`Object.keys()` returns an array of the object's own enumerable property names. You can then use a for...of loop or forEach to iterate over this array.

const obj = {

  a: 1,

  b: 2,

  c: 3,

};

Object.keys(obj).forEach((key) => {

  console.log(`${key}: ${obj[key]}`);

});

Most common ways to iterate over array are using `for` loop and `Array.prototype.forEach` method.

**Using `for` loop**

let array = [1, 2, 3, 4, 5, 6];

for (let index = 0; index < array.length; index++) {

  console.log(array[index]);

}

**Using `Array.prototype.forEach` method**

let array = [1, 2, 3, 4, 5, 6];

array.forEach((number, index) => {

  console.log(`${number} at index ${index}`);

});

**Using `for...of`**

This method is the newest and most convenient way to iterate over arrays. It automatically iterates over each element without requiring you to manage the index.

const numbers = [1, 2, 3, 4, 5];

for (const number of numbers) {

  console.log(number);

}

There are also other inbuilt methods available which are suitable for specific scenarios for example:

- `Array.prototype.filter`: You can use the `filter` method to create a new array containing only the elements that satisfy a certain condition.
- `Array.prototype.map`: You can use the `map` method to create a new array based on the existing one, transforming each element with a provided function.
- `Array.prototype.reduce`: You can use the `reduce` method to combine all elements into a single value by repeatedly calling a function that takes two arguments: the accumulated value and the current element.

---

## Iterating over objects

Iterating over object properties and array is very common in JavaScript and we have various ways to achieve this. Here are some of the ways to do it:

### `for...in` statement

This loop iterates over all **enumerable** properties of an object, including those inherited from its prototype chain.

for (const property in obj) {

  console.log(property);

}

Since `for...in` statement iterates over all the object's **enumerable** properties (including inherited enumerable properties). Hence most of the time you should check whether the property exists on directly on the object via `Object.hasOwn(object, property)` before using it.

for (const property in obj) {

  if (Object.hasOwn(obj, property)) {

    console.log(property);

  }

}

Note that `obj.hasOwnProperty()` is not recommended because it doesn't work for objects created using `Object.create(null)`. It is recommended to use [`Object.hasOwn()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn) in newer browsers, or use the good old `Object.prototype.hasOwnProperty.call(object, key)`.

### `Object.keys()`

`Object.keys()` is a static method that will return an array of all the enumerable property names of the object that you pass it. Since `Object.keys()` returns an array, you can also use the array iteration approaches listed below to iterate through it.

Object.keys(obj).forEach((property) => {

  console.log(property);

});

### `Object.entries()`:

This method returns an array of an object's enumerable properties in `[key, value]` pairs.

const obj = { a: 1, b: 2, c: 3 };

Object.entries(obj).forEach(([key, value]) => {

  console.log(`${key}: ${value}`);

});

### `Object.getOwnPropertyNames()`

Object.getOwnPropertyNames(obj).forEach((property) => {

  console.log(property);

});

`Object.getOwnPropertyNames()` is a static method that will lists all enumerable and non-enumerable properties of the object that you pass it. Since `Object.getOwnPropertyNames()` returns an array, you can also use the array iteration approaches listed below to iterate through it.

## Arrays

### `for` loop

for (var i = 0; i < arr.length; i++) {

  console.log(arr[i]);

}

A common pitfall here is that `var` is in the function scope and not the block scope and most of the time you would want block scoped iterator variable. ES2015 introduces `let` which has block scope and it is recommended to use `let` over `var`.

for (let i = 0; i < arr.length; i++) {

  console.log(arr[i]);

}

### `Array.prototype.forEach()`

arr.forEach((element, index) => {

  console.log(element, index);

});

The `Array.prototype.forEach()` method can be more convenient at times if you do not need to use the `index` and all you need is the individual array elements. However, the downside is that you cannot stop the iteration halfway and the provided function will be executed on the elements once. A `for` loop or `for...of` statement is more relevant if you need finer control over the iteration.

### `for...of` statement

for (let element of arr) {

  console.log(element);

}

ES2015 introduces a new way to iterate, the `for-of` loop, that allows you to loop over objects that conform to the [iterable protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) such as `String`, `Array`, `Map`, `Set`, etc. It combines the advantages of the `for` loop and the `forEach()` method. The advantage of the `for` loop is that you can break from it, and the advantage of `forEach()` is that it is more concise than the `for` loop because you don't need a counter variable. With the `for...of` statement, you get both the ability to break from a loop and a more concise syntax.

Most of the time, prefer the `.forEach` method, but it really depends on what you are trying to do. Before ES2015, we used `for` loops when we needed to prematurely terminate the loop using `break`. But now with ES2015, we can do that with `for...of` statement. Use `for` loops when you need more flexibility, such as incrementing the iterator more than once per loop.

Also, when using the `for...of` statement, if you need to access both the index and value of each array element, you can do so with ES2015 `Array.prototype.entries()` method:

const arr = ['a', 'b', 'c'];

for (let [index, elem] of arr.entries()) {

  console.log(index, ': ', elem);

}