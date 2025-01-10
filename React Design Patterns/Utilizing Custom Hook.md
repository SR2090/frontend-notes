![[Pasted image 20241207000115.png]]
The initialise count method is being used by useState to initialise that on the 1st render.
If we were to use useState(initialzeCount()) then the method would be executed on every render.

Passing the function by reference will allow the method to be executed only once which is the first time when the component renders


![[Pasted image 20241207000456.png]]
This is a custom hook with increment, decrement function. We need to optimize this because we are going to return the state as well as these two function back to whatever component that is using our custom hook.

![[Pasted image 20241207000714.png]]

The optimization needed would wrap increment, decrement to constant function  wrap them in a usecallback hook. 

Use callback will prevent the reference of the function to change therefore we can use this function as a dependency in an useEffect hook.

![[Pasted image 20241207001020.png]]




