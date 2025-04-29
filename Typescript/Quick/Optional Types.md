```ts
function generateError(msg?: string) {
throw new Error(msg);
}
generateError();
generateError("An error Occurred")
```

The ? operator tells Ts that the msg parameter is optional.
It also allows us to set optional parameter for role.

```ts
type User {
name: string;
age: number;
role?: 'admin' | 'guest'
}
```