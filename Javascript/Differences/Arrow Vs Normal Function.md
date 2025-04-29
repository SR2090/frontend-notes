## **Arrow Functions vs Normal Functions in JavaScript**

Both **arrow functions (`=>`)** and **normal functions (`function`)** allow defining functions in JavaScript, but they behave differently in terms of `this`, arguments, and usage.

---

### **1. Syntax Differences**

#### **Normal Function**

```js
function greet(name) {
  return `Hello, ${name}`;
}
console.log(greet("John")); // Hello, John
```

#### **Arrow Function**

```js
const greet = (name) => `Hello, ${name}`;
console.log(greet("John")); // Hello, John
```

- **Concise syntax**: Arrow functions allow omitting `{}` and `return` for single expressions.

---

### **2. `this` Behavior**

#### **Normal Function (Own `this`)**

```js
const person = {
  name: "Alice",
  sayName: function () {
    console.log(this.name);
  },
};
person.sayName(); // Alice (this refers to person)
```

#### **Arrow Function (Inherits `this`)**

```js
const person = {
  name: "Alice",
  sayName: () => {
    console.log(this.name);
  },
};
person.sayName(); // Undefined (Arrow functions do not bind `this`)
```

- **Normal functions**: `this` refers to the calling object.
- **Arrow functions**: `this` is inherited from the surrounding lexical scope.

---

### **3. `arguments` Object**

#### **Normal Function (Has `arguments`)**

```js
function showArgs() {
  console.log(arguments);
}
showArgs(1, 2, 3); // [1, 2, 3]
```

#### **Arrow Function (No `arguments`)**

```js
const showArgs = () => {
  console.log(arguments);
};
showArgs(1, 2, 3); // Uncaught ReferenceError: arguments is not defined
```

- **Normal functions**: Have an `arguments` object.
- **Arrow functions**: Do not have `arguments`, but can use rest parameters `(...args)`.

---

### **4. Usage in Object Methods**

#### **Normal Function (Recommended for Object Methods)**

```js
const obj = {
  value: 42,
  method: function () {
    console.log(this.value);
  },
};
obj.method(); // 42
```

#### **Arrow Function (Not Recommended for Object Methods)**

```js
const obj = {
  value: 42,
  method: () => {
    console.log(this.value);
  },
};
obj.method(); // Undefined (because `this` is not bound to `obj`)
```

- **Normal functions**: Work correctly in object methods.
- **Arrow functions**: Should **not** be used for object methods.

---

### **5. Can Be Used as a Constructor?**

#### **Normal Function (Can Be Used as Constructor)**

```js
function Person(name) {
  this.name = name;
}
const user = new Person("John");
console.log(user.name); // John
```

#### **Arrow Function (Cannot Be Used as Constructor)**

```js
const Person = (name) => {
  this.name = name;
};
const user = new Person("John"); // Error: Person is not a constructor
```

- **Normal functions**: Can be used with `new` to create objects.
- **Arrow functions**: Cannot be used as constructors.

---

## **Key Differences Summary Table**

|Feature|Normal Function (`function`)|Arrow Function (`=>`)|
|---|---|---|
|**Syntax**|Verbose|Shorter, concise|
|**`this` binding**|Own `this` (depends on caller)|Inherited `this` (lexical scope)|
|**`arguments` object**|Available|Not available (use rest parameters)|
|**Object methods**|Works correctly|Not recommended (loses `this`)|
|**Constructor function**|Can be used with `new`|Cannot be used with `new`|

---

## **Mnemonic to Remember:**

### **"THIS ARROW AIMS HIGH"**

- **THIS**: Arrow functions **don’t bind `this`**, they inherit it.
- **ARROW**: **No `arguments`**, concise syntax.
- **AIMS**: **Avoid in Methods** (objects).
- **HIGH**: **Not for Constructors** (no `new`).

This helps recall when to use normal functions vs. arrow functions! 🚀




## Why use arrow functions 

```markdown
When we say the callback is invoked “as a plain function,” we mean it’s called with **no owning object**, so its `this` value falls back to the default (the global object in non-strict mode, or `undefined` in strict mode).

---

## 1. Method Call vs. Plain Function Call

- **Method call**:  
  ```js
  obj.method();
  // Inside method(), this === obj
```

- **Plain function call**:
    
    ```js
    func();
    // Inside func(), this === window (non-strict) or undefined (strict)
    ```
    

---

## 2. How `setTimeout` Executes Your Callback

When you write:

```js
Person.prototype.delayedGreet = function() {
  setTimeout(function() {
    console.log(this.name);
    // ← here, this is NOT the Person instance,
    // because setTimeout invokes the function “plainly”
  }, 100);
};
```

1. You pass an anonymous function reference into `setTimeout`.
    
2. After 100 ms, the browser/runtime does something like:
    
    ```js
    callback();  // plain call, no receiver object
    ```
    
3. Because there’s no `receiver` (no `obj.callback()`), JavaScript doesn’t bind `this` to your instance—so `this` is global/undefined.
    

---

## 3. Why Arrow Functions Avoid This

Contrast with an arrow callback:

```js
Person.prototype.delayedGreet = function() {
  setTimeout(() => {
    console.log(this.name);
    // ← arrow reuses the `this` from delayedGreet,
    // which *was* called as a method on your Person instance
  }, 100);
};
```

- **Arrow callbacks** don’t get their own `this` at call-time; they close over the `this` of the surrounding scope (lexical `this`).
    
- So even though `setTimeout` still does `callback()`, the arrow’s `this` is already bound to your instance.
    

---

### Key Point

> **Plain function execution** means “calling a function without any object before the dot,” so your `this` is **not** set to your instance—hence the lost context in `setTimeout(function(){…})`.