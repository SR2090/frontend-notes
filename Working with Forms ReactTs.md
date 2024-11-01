![[Pasted image 20241005174320.png]]
The React.FormEvent 


Working with Ref
- be explcitiy about the kind of data that will be stored in the ref.![[Pasted image 20241005174641.png]]. Creating a ref with a defautl value of null indicating an empty input field.
![[Pasted image 20241005174858.png]]
using ! here ensures that enteredText does not have an inferred type of undefined apart from string. This is because allows it to have specify having a value.

? is optional operator that means that the provided value can be undefined. The `?` operator in TypeScript is used to mark properties or parameters as optional. It means that the value can either be provided or left out, and if left out, it will be `undefined`.


```ts
interface User {
  name: string;
  age?: number; // optional
}

function greet(user: User) {
  console.log(`Hello, ${user.name}!`);
  if (user.age !== undefined) {
    console.log(`You are ${user.age} years old.`);
  }
}
```


![[Pasted image 20241005175538.png]]



![[Pasted image 20241005175952.png]]


Delete ToDoHandler working with click events
![[Pasted image 20241005180926.png]]
Here, we do not need argument specification for the component because we are not accepting any parameters. 