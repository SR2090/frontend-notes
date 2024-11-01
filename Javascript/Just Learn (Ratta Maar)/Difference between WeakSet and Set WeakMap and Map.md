```js
// Create a Set to track visited objects
const visited = new Set();

// Function to traverse an object recursively
function traverse(obj) {
  // Check if the object has already been visited
  if (visited.has(obj)) {
    return;
  }

  // Add the object to the visited set
  visited.add(obj);

  // Traverse the object's properties
  for (let prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      let value = obj[prop];
      if (typeof value === 'object' && value !== null) {
        traverse(value);
      }
    }
  }

  // Process the object
  console.log('Processing object: ', obj);
}

// Create a large object with circular references
function createLargeObject() {
  const largeObject = {};

  // Create many nested objects
  for (let i = 0; i < 10000; i++) {
    largeObject['prop' + i] = { data: 'Some large data ' + i };
  }

  // Create a circular reference
  largeObject.self = largeObject;

  return largeObject;
}

// Create the large object
const obj = createLargeObject();

// Traverse the large object
traverse(obj);

```