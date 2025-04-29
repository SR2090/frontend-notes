![[Pasted image 20250322102235.png]]
Output 10
All of the setState will be batched.

![[Pasted image 20250322102327.png]]

O/P 25 this will go in a queue and updated sequentially because we are accessing the previous value.




![[Pasted image 20250322102646.png]]

O/P 0 because due to state re-render will not be happening.



![[Pasted image 20250322102903.png]]

Map will return a jsx storing it in a variable does not change it.

