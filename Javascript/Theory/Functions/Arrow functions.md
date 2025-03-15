
## Summary
 Concise syntax for writing functions in JavaScript
 They are particularly useful for maintaining the `this` context within methods and callbacks.
## Arrow functions revisited

Let’s revisit arrow functions.

Arrow functions are not just a “shorthand” for writing small stuff. They have some very specific and useful features.

JavaScript is full of situations where we need to write a small function that’s executed somewhere else.

For instance:

- `arr.forEach(func)` – `func` is executed by `forEach` for every array item.
- `setTimeout(func)` – `func` is executed by the built-in scheduler.
- …there are more.

It’s in the very spirit of JavaScript to create a function and pass it somewhere.

And in such functions we usually don’t want to leave the current context. That’s where arrow functions come in handy.

## [Arrow functions have no “this”](https://javascript.info/arrow-functions#arrow-functions-have-no-this)

As we remember from the chapter [Object methods, "this"](https://javascript.info/object-methods), arrow functions do not have `this`. If `this` is accessed, it is taken from the outside.

For instance, we can use it to iterate inside an object method:

```js
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],
  showList() {
    this.students.forEach(student => alert(this.title + ': ' + student));
  }
};
group.showList();

```

Here in `forEach`, the arrow function is used, so `this.title` in it is exactly the same as in the outer method `showList`. That is: `group.title`.

If we used a “regular” function, there would be an error:

``` `let` group `=` `{`   `title``:` `"Our Group"``,`   `students``:` `[``"John"``,` `"Pete"``,` `"Alice"``]``,`    `showList``(``)` `{`     _`this``.`students`.``forEach``(``function``(``student``)` `{`       `// Error: Cannot read property 'title' of undefined`       `alert``(``this``.`title `+` `': '` `+` student`)``;`     `}``)``;`_   `}` `}``;`  group`.``showList``(``)``;` ```

The error occurs because `forEach` runs functions with `this=undefined` by default, so the attempt to access `undefined.title` is made.

That doesn’t affect arrow functions, because they just don’t have `this`.

Arrow functions can’t run with `new`

Not having `this` naturally means another limitation: arrow functions can’t be used as constructors. They can’t be called with `new`.

Arrow functions VS bind

There’s a subtle difference between an arrow function `=>` and a regular function called with `.bind(this)`:

- `.bind(this)` creates a “bound version” of the function.
- The arrow `=>` doesn’t create any binding. The function simply doesn’t have `this`. The lookup of `this` is made exactly the same way as a regular variable search: in the outer lexical environment.

## [Arrows have no “arguments”](https://javascript.info/arrow-functions#arrows-have-no-arguments)

Arrow functions also have no `arguments` variable.

That’s great for decorators, when we need to forward a call with the current `this` and `arguments`.

For instance, `defer(f, ms)` gets a function and returns a wrapper around it that delays the call by `ms` milliseconds:

[](https://javascript.info/arrow-functions# "run")

[](https://javascript.info/arrow-functions# "open in sandbox")

```` `function` `defer``(```f`,` ms```)` `{`   `return` `function``(``)` `{`     `setTimeout``(``(``)` `=>` `f``.``apply``(``this``,` arguments`)``,` ms`)``;`   `}``;` `}`  `function` `sayHi``(``who``)` `{`   `alert``(``'Hello, '` `+` who`)``;` `}`  `let` sayHiDeferred `=` `defer``(`sayHi`,` `2000``)``;` `sayHiDeferred``(``"John"``)``;` `// Hello, John after 2 seconds` ````

The same without an arrow function would look like:

```` `function` `defer``(```f`,` ms```)` `{`   `return` `function``(``` `...`args ```)` `{`     `let` ctx `=` `this``;`     `setTimeout``(``function``(``)` `{`       `return` `f``.``apply``(`ctx`,` args`)``;`     `}``,` ms`)``;`   `}``;` `}` ````

Here we had to create additional variables `args` and `ctx` so that the function inside `setTimeout` could take them.

## [Summary](https://javascript.info/arrow-functions#summary)

Arrow functions:

- Do not have `this`
- Do not have `arguments`
- Can’t be called with `new`
- They also don’t have `super`, but we didn’t study it yet. We will on the chapter [Class inheritance](https://javascript.info/class-inheritance)

That’s because they are meant for short pieces of code that do not have their own “context”, but rather work in the current one. And they really shine in that use case.

[](https://javascript.info/bind)[](https://javascript.info/object-properties)

![[Pasted image 20250214214952.png]]

[Arrow function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#No_separate_this)




### **Do `bind()`, `call()`, and `apply()` Affect `this` in Arrow Functions?**

No, they **do not** affect the `this` context of an **arrow function**. The reason is that **arrow functions do not have their own `this`**; they inherit `this` from their surrounding lexical scope.

### **Example: Normal Function vs. Arrow Function**

#### **Using `call()`, `apply()`, and `bind()` with a Normal Function**

```js
const obj = {
  value: 42,
  normalFunc: function () {
    console.log(this.value);
  }
};

const externalFunc = obj.normalFunc;
externalFunc(); // undefined (called in global context)

externalFunc.call(obj); // 42
externalFunc.apply(obj); // 42
const boundFunc = externalFunc.bind(obj);
boundFunc(); // 42
```

✅ `this` is affected by `call`, `apply`, and `bind`.

---

#### **Using `call()`, `apply()`, and `bind()` with an Arrow Function**

```js
const obj = {
  value: 42,
  arrowFunc: () => {
    console.log(this.value);
  }
};

const externalArrow = obj.arrowFunc;
externalArrow(); // undefined (inherits `this` from outer scope, which is global)

externalArrow.call(obj); // undefined
externalArrow.apply(obj); // undefined
const boundArrow = externalArrow.bind(obj);
boundArrow(); // undefined
```

❌ `this` **does not change** in the arrow function, no matter how you try to rebind it.

---

### **Why Doesn't `this` Change for Arrow Functions?**

- Arrow functions **do not have their own `this`**.
- Instead, `this` is **lexically inherited** from their surrounding **enclosing function** (or global scope if no function surrounds them).
- Since there's no internal `this`, trying to change it using `call`, `apply`, or `bind` **has no effect**.

---

### **When is This Useful?**

Arrow functions are useful in cases where you want to ensure `this` **always refers to the outer scope**, such as:

#### **1. Inside a Class Method Without Needing `bind(this)`**

```js
class Counter {
  constructor() {
    this.count = 0;
    setInterval(() => {
      this.count++; // `this` refers to the instance of Counter
      console.log(this.count);
    }, 1000);
  }
}

const counter = new Counter();
```

- Using a normal function inside `setInterval` would require `.bind(this)`, but with an arrow function, `this` is automatically bound to the instance.

#### **2. Inside Event Listeners**

```js
const button = document.querySelector('button');
const obj = {
  value: 10,
  handleClick: () => {
    console.log(this.value); // `this` is inherited from the outer scope (global), NOT `obj`
  }
};
button.addEventListener('click', obj.handleClick); // `this` does NOT refer to `obj`
```

- Here, `this` **does not refer to `obj`** because the arrow function inherits `this` from the outer scope (which is the global object in non-strict mode, or `undefined` in strict mode).

---

### **Key Takeaways**

✅ **`call()`, `apply()`, and `bind()` work with normal functions** because they have their own `this`.  
❌ **Arrow functions ignore `call()`, `apply()`, and `bind()`** because they don’t have their own `this`.  
💡 **Use arrow functions when you want `this` to always refer to the enclosing scope.**

Would you like more examples of when to use (or avoid) arrow functions? 🚀




### **When to Use Arrow Functions vs. When to Avoid Them**

Arrow functions are great in many scenarios, but they also have limitations. Below are the best use cases and situations where you should **avoid** them.

---

## ✅ **When to Use Arrow Functions**

### **1. When You Want to Preserve `this` in Callbacks**

Arrow functions inherit `this` from their enclosing scope, making them great for callbacks.

#### ✅ **Example: Inside a Class Method**

```js
class Counter {
  constructor() {
    this.count = 0;
    setInterval(() => {
      this.count++;
      console.log(this.count);
    }, 1000);
  }
}

const counter = new Counter(); // Increments `count` every second
```

- Here, an **arrow function ensures `this` refers to the instance** of `Counter` instead of the global object.

#### ❌ **Using a Regular Function (Incorrect)**

```js
class Counter {
  constructor() {
    this.count = 0;
    setInterval(function () {
      this.count++; // `this` is now the global object (or `undefined` in strict mode)
      console.log(this.count);
    }, 1000);
  }
}

const counter = new Counter(); // NaN (because `this.count` is undefined)
```

- A normal function inside `setInterval` changes `this` to the global object.
- You would need `.bind(this)` to fix it.

---

### **2. When Using Arrow Functions in Array Methods (`map`, `filter`, `reduce`)**

Arrow functions make code cleaner when working with arrays.

#### ✅ **Example: Using `map` to Transform an Array**

```js
const numbers = [1, 2, 3, 4, 5];
const squares = numbers.map(num => num * num);
console.log(squares); // [1, 4, 9, 16, 25]
```

- **Concise** and avoids writing `return` explicitly.

#### ❌ **Using Regular Function (Less Readable)**

```js
const squares = numbers.map(function (num) {
  return num * num;
});
```

---

### **3. When Using Arrow Functions in Object Methods with `this` Reference**

If a function inside an object does not need its own `this`, use an arrow function.

#### ✅ **Example: Arrow Function Keeps `this` in an Object Method**

```js
const person = {
  name: 'Alice',
  greet: function() {
    setTimeout(() => {
      console.log(`Hello, my name is ${this.name}`);
    }, 1000);
  }
};

person.greet(); // Hello, my name is Alice
```

- The arrow function inside `setTimeout` inherits `this` from `greet`, ensuring it refers to `person`.

#### ❌ **Using a Regular Function (Incorrect)**

```js
const person = {
  name: 'Alice',
  greet: function() {
    setTimeout(function() {
      console.log(`Hello, my name is ${this.name}`); // `this` is now global
    }, 1000);
  }
};

person.greet(); // `this.name` is undefined
```

- Regular functions do **not** inherit `this`, so `this.name` is `undefined`.

---

## ❌ **When to Avoid Arrow Functions**

### **1. When You Need a Method with `this` in an Object**

Arrow functions don’t have their own `this`, so they cannot be used for object methods that rely on `this`.

#### ❌ **Incorrect: Arrow Function in an Object Method**

```js
const person = {
  name: 'Alice',
  greet: () => {
    console.log(`Hello, my name is ${this.name}`);
  }
};

person.greet(); // Undefined, because `this` refers to the outer scope (global)
```

- The arrow function takes `this` from its enclosing scope (which is global), **not `person`**.

#### ✅ **Correct: Use a Regular Function**

```js
const person = {
  name: 'Alice',
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

person.greet(); // Hello, my name is Alice
```

---

### **2. When You Need a Constructor Function**

Arrow functions cannot be used as constructors because they lack `this`.

#### ❌ **Incorrect: Arrow Function as a Constructor**

```js
const Person = (name) => {
  this.name = name;
};

const alice = new Person('Alice'); // TypeError: Person is not a constructor
```

- Arrow functions don’t have a `prototype`, so they **cannot be used with `new`**.

#### ✅ **Correct: Use a Regular Function**

```js
function Person(name) {
  this.name = name;
}

const alice = new Person('Alice');
console.log(alice.name); // Alice
```

---

### **3. When Working with `arguments`**

Arrow functions do not have their own `arguments` object.

#### ❌ **Incorrect: Arrow Function Missing `arguments`**

```js
const add = () => {
  console.log(arguments);
};

add(1, 2, 3); // ReferenceError: arguments is not defined
```

- Arrow functions do **not** have `arguments`, so the code fails.

#### ✅ **Correct: Use a Regular Function**

```js
function add() {
  console.log(arguments);
}

add(1, 2, 3); // [Arguments] { '0': 1, '1': 2, '2': 3 }
```

---

### **4. When You Need Dynamic `this` (e.g., Event Listeners)**

Arrow functions inherit `this`, so they are not ideal when `this` should refer to the event target.

#### ❌ **Incorrect: Arrow Function in an Event Listener**

```js
document.getElementById('btn').addEventListener('click', () => {
  console.log(this); // `this` is the outer scope (not the button element)
});
```

- `this` **does not** refer to the button, but to the surrounding scope (likely `window`).

#### ✅ **Correct: Use a Regular Function**

```js
document.getElementById('btn').addEventListener('click', function () {
  console.log(this); // `this` refers to the button element
});
```

---

## **🔑 Summary: When to Use and Avoid Arrow Functions**

|Situation|✅ Use Arrow Function|❌ Avoid Arrow Function|
|---|---|---|
|**Callback Functions** (e.g., `setTimeout`, array methods)|✅ Yes|❌ No|
|**Preserving `this`** (e.g., inside class methods)|✅ Yes|❌ No|
|**Object Methods** (when `this` is needed)|❌ No|✅ Yes|
|**Constructor Functions**|❌ No|✅ Yes|
|**Event Listeners** (when `this` is needed)|❌ No|✅ Yes|
|**Functions Using `arguments`**|❌ No|✅ Yes|

---

### **Final Thoughts**

- Use **arrow functions** when you need to inherit `this` from the surrounding scope.
- Use **regular functions** when you need:
    - A method that refers to its object (`this`).
    - A constructor function.
    - Access to `arguments`.

Would you like any specific examples clarified? 🚀




---
title: What advantage is there for using the JavaScript arrow syntax for a method in a constructor?
---

## TL;DR

The main advantage of using an arrow function as a method inside a constructor is that the value of `this` gets set at the time of the function creation and can't change after that. When the constructor is used to create a new object, `this` will always refer to that object.

For example, let's say we have a `Person` constructor that takes a first name as an argument has two methods to `console.log()` that name, one as a regular function and one as an arrow function:

```js
const Person = function (name) {
  this.name = name;
  this.sayName1 = function () {
    console.log(this.name);
  };
  this.sayName2 = () => {
    console.log(this.name);
  };
};

const john = new Person('John');
const dave = new Person('Dave');

john.sayName1(); // John
john.sayName2(); // John

// The regular function can have its `this` value changed, but the arrow function cannot
john.sayName1.call(dave); // Dave (because `this` is now the dave object)
john.sayName2.call(dave); // John

john.sayName1.apply(dave); // Dave (because `this` is now the dave object)
john.sayName2.apply(dave); // John

john.sayName1.bind(dave)(); // Dave (because `this` is now the dave object)
john.sayName2.bind(dave)(); // John

const sayNameFromWindow1 = john.sayName1;
sayNameFromWindow1(); // undefined (because `this` is now the window object)

const sayNameFromWindow2 = john.sayName2;
sayNameFromWindow2(); // John
```

The main takeaway here is that `this` can be changed for a normal function, but `this` always stays the same for an arrow function. So even if you are passing around your arrow function to different parts of your application, you wouldn't have to worry about the value of `this` changing.

---

## Arrow functions

Arrow functions are introduced in ES2015 and it provides a concise way to write functions in Javascript. One of the key features of arrow function is that it lexically bind the `this` value, which means that it takes the `this` value from enclosing scope.

### Syntax

Arrow functions use the `=>` syntax instead of the function keyword. The basic syntax is:

```js
const myFunction = (arg1, arg2, ...argN) => {
  // function body
};
```

If the function body has only one expression, you can omit the curly braces and the return keyword:

```js
const myFunction = (arg1, arg2, ...argN) => expression;
```

### Examples

```js
// Arrow function with parameters
const multiply = (x, y) => x * y;

// Arrow function with no parameters
const sayHello = () => 'Hello, World!';
```

### Advantages

- **Concise**: Arrow functions provide a more concise syntax, especially for short functions.
- **Implicit return**: They have an implicit return for single-line functions.
- **Value of `this` is predictable**: Arrow functions lexically bind the `this` value, inheriting it from the enclosing scope.

### Limitations

Arrow functions cannot be used as constructors and will throw an error when used with the `new` keyword.

```js
const Foo = () => {};
const foo = new Foo(); // TypeError: Foo is not a constructor
```

They also do not have `arguments` keyword; the arguments have to be obtained from using the rest operator (`...`) in the arguments.

```js
const arrowFunction = (...args) => {
  console.log(arguments); // Throws a TypeError
  console.log(args); // [1, 2, 3]
};

arrowFunction(1, 2, 3);
```

Since arrow functions do not have their own `this`, they are not suitable for defining methods in an object. Traditional function expressions or function declarations should be used instead.

```js
const obj = {
  value: 42,
  getValue: () => this.value, // `this` does not refer to `obj`
};

console.log(obj.getValue()); // undefined
```

## Why arrow functions are useful

One of the most notable features of arrow functions is their behavior with `this`. Unlike regular functions, arrow functions do not have their own `this`. Instead, they inherit `this` from the parent scope at the time they are defined. This makes arrow functions particularly useful for scenarios like event handlers, callbacks, and methods in classes.

### Arrow functions inside function constructors

```js
const Person = function (name) {
  this.name = name;
  this.sayName1 = function () {
    console.log(this.name);
  };
  this.sayName2 = () => {
    console.log(this.name);
  };
};

const john = new Person('John');
const dave = new Person('Dave');

john.sayName1(); // John
john.sayName2(); // John

// The regular function can have its `this` value changed, but the arrow function cannot
john.sayName1.call(dave); // Dave (because `this` is now the dave object)
john.sayName2.call(dave); // John

john.sayName1.apply(dave); // Dave (because `this` is now the dave object)
john.sayName2.apply(dave); // John

john.sayName1.bind(dave)(); // Dave (because `this` is now the dave object)
john.sayName2.bind(dave)(); // John

const sayNameFromWindow1 = john.sayName1;
sayNameFromWindow1(); // undefined (because `this` is now the window object)

const sayNameFromWindow2 = john.sayName2;
sayNameFromWindow2(); // John
```

### Arrow functions in event handlers

```js
const button = document.getElementById('myButton');

button.addEventListener('click', function () {
  console.log(this); // Output: Button
  console.log(this === button); // Output: true
});

button.addEventListener('click', () => {
  console.log(this); // Output: Window
  console.log(this === window); // Output: true
});
```

This can be particularly helpful in React class components. If you define a class method for something such as a click handler using a normal function, and then you pass that click handler down into a child component as a prop, you will need to also bind `this` in the constructor of the parent component. If you instead use an arrow function, there is no need to bind `this`, as the method will automatically get its `this` value from its enclosing lexical context. See this [article](https://medium.com/@machnicki/handle-events-in-react-with-arrow-functions-ede88184bbb) for an excellent demonstration and sample code.

## Further reading

- [Arrow function expressions - MDN ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [How to Use JavaScript Arrow Functions – Explained in Detail](https://www.freecodecamp.org/news/javascript-arrow-functions-in-dep)