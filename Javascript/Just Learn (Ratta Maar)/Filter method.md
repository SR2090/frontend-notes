---
tags:
  - arraymethod
---
![[Pasted image 20240928163536.png]]

![[Pasted image 20240928163602.png]]
![[Pasted image 20240928163616.png]]

```js
filter(callbackFn)
filter(callbackFn, thisArg)

```

![[Pasted image 20240928163452.png]]
From mdn

thisArg will be the object using which we will call the callback function.


### Useful
![[Pasted image 20240928163717.png]]

### Implementing Filter method

The `this` in the provided `myFilter` function refers to the array on which the custom `myFilter` method is called.

This behavior is derived from how `Array.prototype` methods work. In JavaScript, when a function is attached to an object (like a method), the `this` keyword inside that function refers to the object it was called on.

### How it works:

1. **Declaring the method**:  
    The `myFilter` method is attached to the prototype of `Array`. This means any array object (e.g., `[1, 2, 3]`) will inherit this method.
    
2. **Calling `myFilter`**:  
    When you call `myFilter` on an array, like `[1, 2, 3].myFilter(...)`, the `this` inside `myFilter` refers to the array `[1, 2, 3]`.
    
3. **Usage of `this`**:
    
    - `this.length`: Refers to the length of the array the method is operating on.
    - `this[i]`: Accesses the element at index `i` of the array.
    - `Object.hasOwn(this, i)`: Ensures that the array has an element at index `i` (not a property inherited from the prototype chain).

### Example:

```javascript
const array = [1, 2, 3, 4];

const filtered = array.myFilter(function (element) {
  return element > 2;
});

console.log(filtered); // [3, 4]
```

Here, `this` in the `myFilter` method refers to the `array` object, i.e., `[1, 2, 3, 4]`. The `callbackFn` is invoked with each element of the array, and `result` accumulates elements for which the callback returns `true`.

### Key Points:

- `this` provides access to the array on which the method is called.
- The `callbackFn.call(thisArg, currentElement, i, this)` allows `thisArg` to specify the value of `this` inside the `callbackFn`, similar to how the native `Array.prototype.filter` works. If no `thisArg` is provided, `undefined` will be used.