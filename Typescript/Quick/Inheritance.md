Using extends keyword.
When calling child class we have to use the super keyword that will call the base class constructor.

The user class does not have a custom constructor hence we area only required to call the super() keyword.

We can also define our own specific method unique to the child class.

![[Pasted image 20250418114225.png]]


## Protected mode modifier
- We have work method inside which we would want to access firstName property. This property is a private property which cannot be accessed outside of the class.
- We have a fullName getter that will not provide this specific property.
- Hence, we have the protected keyword using which we can access the protected keyword.
![[Pasted image 20250418124228.png]]


