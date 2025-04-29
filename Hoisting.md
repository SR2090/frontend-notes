
![[Pasted image 20240929195632.png]]

Here are simple examples of each scenario for better understanding:

1. **Variable Declarations (var)**:
    
    javascript
    
    Copy code
    
    `console.log(x); // undefined (hoisted, but not initialized) var x = 5; console.log(x); // 5`
    
2. **Variable Declarations (let and const)**:
    
    javascript
    
    Copy code
    
    `console.log(y); // ReferenceError (hoisted, but not initialized) let y = 10;  console.log(z); // ReferenceError (hoisted, but not initialized) const z = 15;`
    
3. **Function Expressions (var)**:
    
    javascript
    
    Copy code
    
    `console.log(myFunc); // undefined (hoisted, but not initialized) var myFunc = function() {   return "Hello"; }; console.log(myFunc()); // "Hello"`
    
4. **Function Declarations (function)**:
    
    javascript
    
    Copy code
    
    `console.log(sayHi()); // "Hi" (fully hoisted)  function sayHi() {   return "Hi"; }`
    
5. **Class Declarations (class)**:
    
    javascript
    
    Copy code
    
    `console.log(Person); // ReferenceError (hoisted, but not initialized)  class Person {   constructor(name) {     this.name = name;   } }  const person = new Person('Alice'); console.log(person.name); // "Alice"`
    
6. **Import Declarations (import)**:
    
    javascript
    
    Copy code
    
    `import { someFunc } from './someModule'; // This runs before the rest of the code  console.log(someFunc()); // You can access the function immediately after importing`
    

Each scenario illustrates how hoisting affects variables, functions, and classes in JavaScript.




---
title: Explain the concept of "hoisting" in JavaScript
---

## TL;DR

- **Variable declarations (`var`)**: Declarations are hoisted, but not initializations. The value of the variable is `undefined` if accessed before initialization.
- **Variable declarations (`let` and `const`)**: Declarations are hoisted, but not initialized. Accessing them results in `ReferenceError` until the actual declaration is encountered.
- **Function expressions (`var`)**: Declarations are hoisted, but not initializations. The value of the variable is `undefined` if accessed before initialization.
- **Function declarations (`function`)**: Both declaration and definition are fully hoisted.
- **Class declarations (`class`)**: Declarations are hoisted, but not initialized. Accessing them results in `ReferenceError` until the actual declaration is encountered.
- **Import declarations (`import`)**: Declarations are hoisted, and side effects of importing the module are executed before the rest of the code.

The following behavior summarizes the result of accessing the variables before they are declared.

| Declaration                    | Accessing before declaration |
| ------------------------------ | ---------------------------- |
| `var foo`                      | `undefined`                  |
| `let foo`                      | `ReferenceError`             |
| `const foo`                    | `ReferenceError`             |
| `class Foo`                    | `ReferenceError`             |
| `var foo = function() { ... }` | `undefined`                  |
| `function foo() { ... }`       | Normal                       |
| `import`                       | Normal                       |

---

## Hoisting

**Hoisting is a term used to explain the behavior of variable declarations in your code**. Variables declared or initialized with the `var` keyword will have their declaration "moved" up to the top of their containing scope during compilation, which we refer to as hoisting.

Only the declaration is hoisted, the initialization/assignment (if there is one), will stay where it is. Note that the declaration is not actually moved – the JavaScript engine parses the declarations during compilation and becomes aware of variables and their scopes, but it is easier to understand this behavior by visualizing the declarations as being "hoisted" to the top of their scope.

Let's explain with a few code samples. Note that the code for these examples should be executed within a module scope instead of being entered line by line into a REPL like the browser console.

### Hoisting of variables declared using `var`

Hoisting is seen in action here as even though `foo` is declared and initialized after the first `console.log()`, the first `console.log()` prints the value of `foo` as `undefined`.

```js
console.log(foo); // undefined
var foo = 1;
console.log(foo); // 1
```

You can visualize the code as:

```js
var foo;
console.log(foo); // undefined
foo = 1;
console.log(foo); // 1
```

### Hoisting of variables declared using `let`, `const`, and `class`

Variables declared via `let`, `const`, and `class` are hoisted as well. However, unlike `var` and `function`, they are not initialized and accessing them before the declaration will result in a `ReferenceError` exception. The variable is in a "temporal dead zone" from the start of the block until the declaration is processed.

```js
y; // ReferenceError: Cannot access 'y' before initialization
let y = 'local';
```

```js
z; // ReferenceError: Cannot access 'z' before initialization
const z = 'local';
```

```js
Foo; // ReferenceError: Cannot access 'Foo' before initialization

class Foo {
  constructor() {}
}
```

### Hoisting of function expressions

Function expressions are functions written in the form of variable declarations. Since they are also declared using `var`, only the variable declaration is hoisted.

```js
console.log(bar); // undefined
bar(); // Uncaught TypeError: bar is not a function

var bar = function () {
  console.log('BARRRR');
};
```

### Hoisting of function declarations

Function declarations use the `function` keyword. Unlike function expressions, function declarations have both the declaration and definition hoisted, thus they can be called even before they are declared.

```js
console.log(foo); // [Function: foo]
foo(); // 'FOOOOO'

function foo() {
  console.log('FOOOOO');
}
```

The same applies to generators (`function*`), async functions (`async function`), and async function generators (`async function*`).

### Hoisting of `import` statements

Import declarations are hoisted. The identifiers the imports introduce are available in the entire module scope, and their side effects are produced before the rest of the module's code runs.

```js
foo.doSomething(); // Works normally.

import foo from './modules/foo';
```

## Under the hood

In reality, JavaScript creates all variables in the current scope before it even tries to executes the code. Variables created using `var` keyword will have the value of `undefined` where variables created using `let` and `const` keywords will be marked as `<value unavailable>`. Thus, accessing them will cause a `ReferenceError` preventing you to access them before initialization.

In ECMAScript specifications `let` and `const` declarations are [explained as below](https://tc39.es/ecma262/#sec-let-and-const-declarations):

> The variables are created when their containing Environment Record is instantiated but may not be accessed in any way until the variable's LexicalBinding is evaluated.

However, this statement is [a litle bit different for the `var` keyword](https://tc39.es/ecma262/#sec-variable-statement):

> Var variables are created when their containing Environment Record is instantiated and are initialized to `undefined` when created.

## Modern practices

In practice, modern code bases avoid using `var` and use `let` and `const` exclusively. It is recommended to declare and initialize your variables and import statements at the top of the containing scope/module to eliminate the mental overhead of tracking when a variable can be used.

ESLint is a static code analyzer that can find violations of such cases with the following rules:

- [`no-use-before-define`](https://eslint.org/docs/latest/rules/no-use-before-define): This rule will warn when it encounters a reference to an identifier that has not yet been declared.
- [`no-undef`](https://eslint.org/docs/latest/rules/no-undef): This rule will warn when it encounters a reference to an identifier that has not yet been declared.

## Further reading

- [Hoisting | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [JavaScript Visualized: Hoisting](https://dev.to/lydiahallie/javascript-visualized-hoisting-478h)



## Flashcards

### 1. What is hoisting in JavaScript?

**Answer**: Hoisting is JavaScript’s behavior of moving variable and function declarations to the top of their containing scope during compilation. Although we describe it as “moving” code, in practice, the JavaScript engine makes these declarations known before execution begins.

---

### 2. How does hoisting affect variables declared with `var`?

**Answer**: For `var`, the declaration is hoisted and initializes to `undefined` at the start of the scope. Accessing it before its actual assignment logs `undefined` (rather than throwing an error).

---

### 3. How are `let` and `const` variables hoisted differently from `var`?

**Answer**: Although `let` and `const` are also hoisted, they remain uninitialized until the execution reaches their declaration. Attempting to access them beforehand results in a `ReferenceError` (the “temporal dead zone”).

---

### 4. How do function declarations (`function`) behave under hoisting?

**Answer**: A function declared with the `function` keyword is fully hoisted: both the declaration and the function body. This means it can be called before its definition appears in the code.

---

### 5. How do function expressions (e.g., `var myFunc = function() {...}`) behave under hoisting?

**Answer**: Only the variable declaration (`var myFunc`) is hoisted—initially set to `undefined`. The actual function expression is not hoisted. Calling `myFunc` before the assignment will result in `undefined` or an error if you try to invoke it as a function.

---

### 6. What happens if you try to use a class declaration before it’s defined?

**Answer**: Classes are hoisted but not initialized. Accessing a class before its definition results in a `ReferenceError`, similar to `let` and `const`.

---

### 7. How are `import` statements hoisted?

**Answer**: Import statements are hoisted to the top of the module. The imported bindings are available throughout the module, and any side effects from the import occur before the rest of the module’s code runs.

---

### 8. What is the “temporal dead zone”?

**Answer**: The temporal dead zone (TDZ) is the period between the start of a variable’s scope and its actual declaration (for `let`, `const`, or `class`). During this time, accessing the variable will result in a `ReferenceError`.

---

### 9. What are modern practices regarding variable declarations in JavaScript?

**Answer**: Modern JavaScript typically avoids `var` and instead uses `let` and `const`. It’s recommended to declare and initialize variables (and import statements) at the top of their scope/module to avoid confusion and potential errors related to hoisting.

---

### 10. Which ESLint rules help catch issues related to hoisting?

**Answer**:

1. **`no-use-before-define`** – warns if a variable or function is used before its declaration.
    
2. **`no-undef`** – warns if a variable is referenced but never declared.
    

---

Feel free to adjust or refine these Q&A pairs further to match your preferred flashcard format.