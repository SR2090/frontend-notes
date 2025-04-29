null and undefined are different.

### Inferred Type null
```ts
const inputEl = document.getElementById("user-name");
if (!inputEl) {
 throw new Error("Element is not defined")
}
console.log(inputEl.value) // the type inferred will be narrowed down to HTML element.
```

## Convince Typescript that a statement will not yield null
```ts
const inputEl = document.getElementById("user-name")!;
console.log(inputEl.value) // No need for the null check but run time error will be thrown
```

##### Another way of using ! operator.
```ts
const inputEl = document.getElementById("user-name");
console.log(inputEl!.value)
```