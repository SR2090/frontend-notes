Here’s a summary of the **most used array methods** in JavaScript, along with syntax and examples, which are often asked during interviews.

### 1. **`forEach()`**

The `forEach()` method executes a provided function once for each array element.

**Syntax:**

```javascript
array.forEach(callback(currentValue, index, array) {
  // Your code here
});
```

**Example:**

```javascript
const numbers = [1, 2, 3];
numbers.forEach((num, index) => {
  console.log(`Index: ${index}, Value: ${num}`);
});
// Output: 
// Index: 0, Value: 1
// Index: 1, Value: 2
// Index: 2, Value: 3
```

### 2. **`map()`**

The `map()` method creates a new array populated with the results of calling a provided function on every element in the array.

**Syntax:**

```javascript
const newArray = array.map(callback(currentValue, index, array) {
  return newElement; // transformed value
});
```

**Example:**

```javascript
const numbers = [1, 2, 3];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6]
```

### 3. **`filter()`**

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

**Syntax:**

```javascript
const newArray = array.filter(callback(currentValue, index, array) {
  return condition; // returns true or false
});
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```

### 4. **`reduce()`**

The `reduce()` method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

**Syntax:**

```javascript
const result = array.reduce(callback(accumulator, currentValue, index, array) {
  return accumulator;
}, initialValue);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 10
```

### 5. **`find()`**

The `find()` method returns the first element in the array that satisfies the provided testing function.

**Syntax:**

```javascript
const foundElement = array.find(callback(currentValue, index, array) {
  return condition; // returns true or false
});
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const found = numbers.find(num => num > 3);
console.log(found); // 4
```

### 6. **`some()`**

The `some()` method tests whether at least one element in the array passes the provided function.

**Syntax:**

```javascript
const result = array.some(callback(currentValue, index, array) {
  return condition; // returns true or false
});
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4];
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true
```

### 7. **`every()`**

The `every()` method tests whether all elements in the array pass the provided function.

**Syntax:**

```javascript
const result = array.every(callback(currentValue, index, array) {
  return condition; // returns true or false
});
```

**Example:**

```javascript
const numbers = [2, 4, 6, 8];
const allEven = numbers.every(num => num % 2 === 0);
console.log(allEven); // true
```

### 8. **`includes()`**

The `includes()` method checks if an array contains a certain element.

**Syntax:**

```javascript
const result = array.includes(element, start);
```

**Example:**

```javascript
const fruits = ['apple', 'banana', 'orange'];
const hasBanana = fruits.includes('banana');
console.log(hasBanana); // true
```

### 9. **`sort()`**

The `sort()` method sorts the elements of an array in place and returns the sorted array.

**Syntax:**

```javascript
const sortedArray = array.sort([compareFunction]);
```

**Example:**

```javascript
const numbers = [3, 1, 4, 2];
numbers.sort();
console.log(numbers); // [1, 2, 3, 4]
```

Note: By default, `sort()` sorts elements as strings. For numeric sorting, you can pass a custom comparator:

```javascript
numbers.sort((a, b) => a - b);
```

### 10. **`concat()`**

The `concat()` method is used to merge two or more arrays into a new array.

**Syntax:**

```javascript
const newArray = array1.concat(array2, array3, ...);
```

**Example:**

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = arr1.concat(arr2);
console.log(combined); // [1, 2, 3, 4]
```

### 11. **`slice()`**

The `slice()` method returns a shallow copy of a portion of an array into a new array object.

**Syntax:**

```javascript
const newArray = array.slice(start, end);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const sliced = numbers.slice(1, 3);
console.log(sliced); // [2, 3]
```

### 12. **`splice()`**

The `splice()` method changes the content of an array by removing, replacing, or adding elements.

**Syntax:**

```javascript
array.splice(start, deleteCount, item1, item2, ...);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.splice(2, 1, 6, 7); // Removes 3 and adds 6, 7
console.log(numbers); // [1, 2, 6, 7, 4, 5]
```

### 13. **`join()`**

The `join()` method joins all the elements of an array into a single string.

**Syntax:**

```javascript
const result = array.join(separator);
```

**Example:**

```javascript
const words = ['Hello', 'World'];
const sentence = words.join(' ');
console.log(sentence); // "Hello World"
```

### 14. **`reverse()`**

The `reverse()` method reverses the elements of an array in place.

**Syntax:**

```javascript
const reversedArray = array.reverse();
```

**Example:**

```javascript
const numbers = [1, 2, 3];
numbers.reverse();
console.log(numbers); // [3, 2, 1]
```

---

### Summary for Interview:

- **`forEach()`**: Iterates over an array, useful for side effects.
- **`map()`**: Creates a new array from the results of calling a function on each element.
- **`filter()`**: Returns a new array containing only the elements that pass a test.
- **`reduce()`**: Reduces an array to a single value based on an accumulator.
- **`find()`**: Finds and returns the first element that satisfies a condition.
- **`some()`**: Checks if at least one element satisfies a condition.
- **`every()`**: Checks if all elements satisfy a condition.
- **`includes()`**: Checks if an array contains a specific element.
- **`sort()`**: Sorts an array in place.
- **`concat()`**: Combines multiple arrays into one.
- **`slice()`**: Creates a shallow copy of a portion of an array.
- **`splice()`**: Modifies the array by adding/removing elements.
- **`join()`**: Joins array elements into a string.
- **`reverse()`**: Reverses the array in place.

These array methods are some of the most common and important ones to know for interviews and working with arrays in JavaScript!