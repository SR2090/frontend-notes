![[Pasted image 20241010133924.png]]
The query function
```js
  const { data, isPending, isError, error, refetch } = useQuery({ queryKey: ['events'], queryFn: fetchEvents })
```
fetchEvents has a default tanStack object being passed as argument. The console.log statement shows this object![[Pasted image 20241010134149.png]]

In this object, the signal key is useful as it allows us to abort an api callout if the user moves away from the page.


