```js
const rows = 3;
const cols = 3;

// Using Array.from to create a 2D array:
const array2D = Array.from({ length: rows }, () => Array(cols).fill(0));

console.log(array2D);
// Output: [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

```