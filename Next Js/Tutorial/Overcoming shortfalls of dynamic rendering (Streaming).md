Steaming is a technique by which the data of a route is divided into chunks that are loaded independent of each other. They are shown to the UI as and when they get loaded. 

The benefit of using streaming is that it prevents the entire website being blocked when the whole page is loading. It allows the user to see and interact with the parts of page without waiting for all the data.

![[Pasted image 20250501103706.png]]

![[Pasted image 20250501103807.png]]
![[Pasted image 20250501103821.png]]


### 2 ways to implement streaming
1. using loading.tsx page for the entire page 
2. Using Suspense to wait for specific components.


## Using the loading.tsx
![[Pasted image 20250501104002.png]]

While the dashboard content is loading we have access to the rest of the static part of the page for which the content is available.
The user can navigate to other page without waiting for this content to fully load.
![[Pasted image 20250501104108.png]]

## Dashboard page loading
![[Pasted image 20250501104135.png]]
The loading in the root of dashboard will cause it to be use by the customer and invoices route. To prevent it we are going to use the route group called overview. Wrapping folder name within parenthesis prevent it from being a part of url defintion.

![[Pasted image 20250501105914.png]]


## 2. Steaming a specific component

Specific components of the page can be streamed instead of applying the suspense fall back to the entire page so the use of loading.tsx . We can achieve this through suspense using which we can show a fall back UI while the data is being dooted and the other parts of the page can be statically loaded![[Pasted image 20250501110202.png]]

Implementing:

We know that fetchRevenue is the cause of concern :
```ts
export async function fetchRevenue() {
  try {
    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 30000));
    const data = await sql<Revenue[]>`SELECT * FROM revenue`;
    return data;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }
}
```

We need the data inside the revenue component. Therefore we will move this call from dashboard to that component. In the dasboard page we are going to wrap it with Suspense.![[Pasted image 20250501110505.png]]

The revenue part data loading blocks the loading of the entire page.
Remove revenue fetch and wrap Revenue with Suspense![[Pasted image 20250501110837.png]]
The data fetch has been moved on to revenue![[Pasted image 20250501110856.png]]



The result: we can see other component while the revenue keeps loading.
![[Pasted image 20250501110806.png]]

### Removed the outer layout
![[Pasted image 20250501124821.png]]


## Suspense Boundary guidelines for specific components

![[Pasted image 20250501125759.png]]

![[Pasted image 20250501125827.png]]

example implementation:
Move data fetching to that component
![[Pasted image 20250501125859.png]]

![[Pasted image 20250501130018.png]]




![[Pasted image 20250501125532.png]]
