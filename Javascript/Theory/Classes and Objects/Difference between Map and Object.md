
![[Pasted image 20240930235023.png]]
## Key differences

Here are the main differences between a `Map` object and a plain object:

1. **Key types**: In a plain object, keys are always strings (or symbols). In a `Map`, keys can be any type of value, including objects, arrays, and even other `Map`s.
2. **Key ordering**: In a plain object, the order of keys is not guaranteed. In a `Map`, the order of keys is preserved, and you can iterate over them in the order they were inserted.
3. **Iteration**: A `Map` is iterable, which means you can use `for...of` loops to iterate over its key-value pairs. A plain object is not iterable by default, but you can use `Object.keys()` or `Object.entries()` to iterate over its properties.
4. **Performance**: `Map` objects are generally faster and more efficient than plain objects, especially when dealing with large datasets.
5. **Methods**: A `Map` object provides additional methods, such as `get`, `set`, `has`, and `delete`, which make it easier to work with key-value pairs.
6. **Serialization**: When serializing a `Map` object to JSON, it will be converted to an object but the existing `Map` properties might be lost in the conversion. A plain object, on the other hand, is serialized to a JSON object with the same structure.

Explanation of the 6th point:

When a `Map` object is serialized to JSON, it is first converted to a plain object. The issue is that the **keys** of the `Map` might get lost in this conversion if they are not of type `string` or `number`. This is because JSON only supports strings as object keys, whereas a `Map` can have keys of any data type (e.g., objects, functions, or other non-primitive types).

For example, consider the following `Map`:
Copy code
```
const map = new Map(); map.set('name', 'John');  // String key map.set(42, 'Answer');    // Number key map.set(true, 'Yes');     // Boolean key map.set({}, 'Object key'); // Object key`
```

When serializing this to JSON:
```js
const json = JSON.stringify(Object.fromEntries(map)); console.log(json);
```

The output would be:
```json
{"name":"John","42":"Answer","true":"Yes"}
```

Here’s what happens:

1. **String keys** (`'name'`) and **number keys** (`42`) are correctly converted to JSON.
2. **Boolean keys** (`true`) are converted to their string equivalents.
3. **Object keys** (`{}`) and other non-primitive types are lost because JSON objects cannot use them as keys.

In the case of object or function keys in the `Map`, their properties are not serialized, and they are essentially "lost" because JSON cannot represent them as object keys.

This is what is meant by "the existing Map properties might be lost in the conversion"—it refers to the inability to serialize non-string/number keys properly in JSON format.



![[Pasted image 20240930234959.png]]


![[Pasted image 20240930235245.png]]
![[Pasted image 20240930235255.png]]