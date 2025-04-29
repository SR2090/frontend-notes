Consider the following scenario
![[Pasted image 20250419114010.png]]
The method getLength returns an union type string | number because of which numOfWords cannot use exclusive string method as those will not exist on the number.



Overloading means have the same function name with different function signature (argument type).
![[Pasted image 20250419114332.png]]
So instead of explicit type casting (**as string** in line 11 and **as number** in line 13) we can directly use the string method as it will match the required function signature and it return type.