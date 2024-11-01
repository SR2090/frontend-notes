![[Pasted image 20241005155607.png]]
This function return type is inferred based on that of its parameter.

To set a specific return type we can use : then specify the type.
![[Pasted image 20241005155644.png]]
![[Pasted image 20241005155651.png]]
No need to explicitly specify types as there is automatic inference in this case unless required.


##### Void return type
```ts
function printSomething(value: any) : void{
console.log(value);
}
```