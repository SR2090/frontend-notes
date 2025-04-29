```ts
const inputEl = document.getElementById("user-name");
console.log(inputEl.value) 
```

By default TypeScript does not know the type of element being returned by this DOM API.
Hence, it assigns the most generic type to it which is HTMLElement.

Due to this we will get error for trying to access value.

using typecasting we can make this value to become HTMLInputElement that will have a value property present.

```ts
const inputEl = document.getElementById("user-name") as HTMLInputElement | null;
console.log(inputEl.value) 
```

Be careful,
As each type we overwrite a type inference made my TypeScript we have to ensure that it does not fail.