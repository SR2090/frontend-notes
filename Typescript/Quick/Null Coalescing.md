```ts
const input = "";
const didProvideInput1 = input || false; // Inferred type will be string | boolean'

const didProvideInput = input ?? false; // Inferred type string
```