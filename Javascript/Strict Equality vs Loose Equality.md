---
title: What is the difference between `==` and `===` in JavaScript?
---
## Strict Equality (===) vs Loose Equality (==)
![[Pasted image 20250223140433.png]]


### Strict Equality (`===`)
- **No Type Conversion:**  
  Strict equality compares both the type and the value, without performing any type conversion.
- **Usage:**  
  Preferred in most cases to avoid unexpected behavior due to implicit type conversion.
- **Example:**  
  ```js
  5 === 5;        // true
  5 === '5';      // false, because the types differ
  null === null;  // true


## TL;DR

`==` is the abstract equality operator while `===` is the strict equality operator. The `==` operator will compare for equality after doing any necessary type conversions. The `===` operator will not do type conversion, so if two values are not the same type `===` will simply return `false`.

| Operator | `==` | `===` |
| --- | --- | --- |
| Name | (Loose) Equality operator | Strict equality operator |
| Type coercion | Yes | No |
| Compares value and type | No | Yes |

---

### Equality operator (`==`)

The `==` operator checks for equality between two values but performs type coercion if the values are of different types. This means that JavaScript will attempt to convert the values to a common type before making the comparison.

```js
42 == '42'; // true
0 == false; // true
null == undefined; // true
[] == false; // true
'' == false; // true
```

In these examples, JavaScript converts the operands to the same type before making the comparison. For example, `42 == '42'` is true because the string `'42'` is converted to the number `42` before comparison.

However, when using `==`, unintuitive results can happen:

```js
1 == [1]; // true
0 == ''; // true
0 == '0'; // true
'' == '0'; // false
```

As a general rule of thumb, never use the `==` operator, except for convenience when comparing against `null` or `undefined`, where `a == null` will return `true` if `a` is `null` or `undefined`.

```js
var a = null;
console.log(a == null); // true
console.log(a == undefined); // true
```

### Strict equality operator (`===`)

The `===` operator, also known as the strict equality operator, checks for equality between two values without performing type coercion. This means that both the value and the type must be the same for the comparison to return true.

```js
console.log(42 === '42'); // false
console.log(0 === false); // false
console.log(null === undefined); // false
console.log([] === false); // false
console.log('' === false); // false
```

For these comparisons, no type conversion is performed, so the statement returns `false` if the types are different. For instance, `42 === '42'` is `false` because the types (number and string) are different.

```js
// Comparison with type coercion (==)
console.log(42 == '42'); // true
console.log(0 == false); // true
console.log(null == undefined); // true

// Strict comparison without type coercion (===)
console.log(42 === '42'); // false
console.log(0 === false); // false
console.log(null === undefined); // false
```

### Bonus: `Object.is()`

There's one final value-comparison operation within JavaScript, that is the [`Object.is()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is) static method. The only difference between `Object.is()` and `===` is how they treat of signed zeros and `NaN` values. The `===` operator (and the `==` operator) treats the number values `-0` and `+0` as equal, but treats `NaN` as not equal to each other.

## Conclusion

- Use `==` when you want to compare values with type coercion (and understand the implications of it). Practically, the only valid use case for the equality operator is when against `null` and `undefined` for convenience.
- Use `===` when you want to ensure both the value and the type are the same, which is the safer and more predictable choice in most cases.

### Notes

- Using `===` (strict equality) is generally recommended to avoid the pitfalls of type coercion, which can lead to unexpected behavior and bugs in your code. It makes the intent of your comparisons clearer and ensures that you are comparing both the value and the type.
- ESLint's [`eqeqeq`](https://eslint.org/docs/latest/rules/eqeqeq) rule enforces the use of strict equality operators `===` and `!==` and even provides an option to always enforce strict equality except when comparing with the `null` literal.

### Further reading

- [Equality (==) | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality)
- [Strict equality (===) | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)