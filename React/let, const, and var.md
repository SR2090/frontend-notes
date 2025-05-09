
---
title: What are the differences between JavaScript variables created using `let`, `var` or `const`?
---

## TL;DR

In JavaScript, `let`, `var`, and `const` are all keywords used to declare variables, but they differ significantly in terms of scope, initialization rules, whether they can be redeclared or reassigned and the behavior when they are accessed before declaration:

| Behavior | `var` | `let` | `const` |
| --- | --- | --- | --- |
| Scope | Function or Global | Block | Block |
| Initialization | Optional | Optional | Required |
| Redeclaration | Yes | No | No |
| Reassignment | Yes | Yes | No |
| Accessing before declaration | `undefined` | `ReferenceError` | `ReferenceError` |

---

## Differences in behavior

Let's look at the difference in behavior between `var`, `let`, and `const`.

### Scope

Variables declared using the `var` keyword are scoped to the function in which they are created, or if created outside of any function, to the global object. `let` and `const` are _block scoped_, meaning they are only accessible within the nearest set of curly braces (function, if-else block, or for-loop).

```js
function foo() {
  // All variables are accessible within functions.
  var bar = 1;
  let baz = 2;
  const qux = 3;

  console.log(bar); // 1
  console.log(baz); // 2
  console.log(qux); // 3
}

console.log(bar); // ReferenceError: bar is not defined
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
```

In the following example, `bar` is accessible outside of the `if` block but `baz` and `quz` are not.

```js
if (true) {
  var bar = 1;
  let baz = 2;
  const qux = 3;
}

// var variables are accessible anywhere in the function scope.
console.log(bar); // 1
// let and const variables are not accessible outside of the block they were defined in.
console.log(baz); // ReferenceError: baz is not defined
console.log(qux); // ReferenceError: qux is not defined
```

### Initialization

`var` and `let` variables can be initialized without a value but `const` declarations must be initialized.

```js
var foo; // Ok
let bar; // Ok
const baz; // SyntaxError: Missing initializer in const declaration
```

### Redeclaration

Redeclaring a variable with `var` will not throw an error, but `let` and `const` will.

```js
var foo = 1;
var foo = 2;
console.log(foo); // 2

let baz = 3;
let baz = 4; // Uncaught SyntaxError: Identifier 'baz' has already been declared
```

### Reassignment

`let` and `const` differ in that `var` and `let` allow reassigning the variable's value while `const` does not.

```js
var foo = 1;
foo = 2; // This is fine.

let bar = 3;
bar = 4; // This is fine.

const baz = 5;
baz = 6; // Uncaught TypeError: Assignment to constant variable.
```

### Accessing before declaration

`var` ,`let` and `const` declared variables are all hoisted. `var` declared variables are auto-initialized with an `undefined` value. However, `let` and `const` variables are not initialized and accessing them before the declaration will result in a `ReferenceError` exception because they are in a "temporal dead zone" from the start of the block until the declaration is processed.

```js
console.log(foo); // undefined
var foo = 'foo';

console.log(baz); // ReferenceError: can't access lexical declaration 'baz' before initialization
let baz = 'baz';

console.log(bar); // ReferenceError: can't access lexical declaration 'bar' before initialization
const bar = 'bar';
```

## Notes

- In modern JavaScript, it's generally recommended to use `const` by default for variables that don't need to be reassigned. This promotes immutability and prevents accidental changes.
- Use `let` when you need to reassign a variable within its scope.
- Avoid using `var` due to its potential for scoping issues and hoisting behavior.
- If you need to target older browsers, write your code using `let`/`const`, and use a transpiler like Babel compile your code to older syntax.

## Further reading

- [The Difference of "var" vs "let" vs "const" in Javascript](https://medium.com/swlh/the-difference-of-var-vs-let-vs-const-in-javascript-abe37e214d66)