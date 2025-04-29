Specify a type otherwise you will always use any which is detrimental to actually using typescript.

![[Pasted image 20241005155607.png]]
This function return type is inferred based on that of its parameter.

To set a specific return type we can use : then specify the type.
![[Pasted image 20241005155644.png]]
![[Pasted image 20241005155651.png]]
No need to explicitly specify types as there is automatic inference in this case unless required.


##### Void return type
And you need to specify type if you do not return anything.
```ts
function printSomething(value: any) : void{
console.log(value);
}
```


#### Never
![[Pasted image 20250407151941.png]]
It will never finish. Hence, a more appropriate return type.


### Function as a type
Its specified using an arrow function.


```js
function performJob(cb: (m: string) => void) {
 cb("string");
}

performJob((msg: string) => console.log(msg));
```



