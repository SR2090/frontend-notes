- New primitive data type introduced in ES6
- Unique and immutable identifiers that is primarily for object property keys to avoid name collisions.
- These values can be created using `Symbol(...)` function, and each `Symbol` value is guaranteed to be unique, even if they have the same key/description.

### Caevaet
 - `Symbol` properties are not enumerable in `for...in` loops or `Object.keys()`, making them suitable for creating private/internal object state.
 - Must be called without the new keyword.
- **Uniqueness**: Each Symbol value is unique, even if they have the same description.
- **Immutability**: Symbol values are immutable, meaning their value cannot be changed.
- **Non-enumerable**: Symbol properties are not included in for...in loops or Object.keys().

