- **[[Styling]]**: The different ways to style your application in Next.js.
- **[[Optimizations for images fonts ]]**: How to optimize images, links, and fonts.
- **[[Routing in NextJs]]**: How to create nested layouts and pages using file-system routing.
- **[[Data Fetching in Next JS]]**: How to set up a Postgres database on Vercel, and best practices for fetching and streaming.
	- [[Static and dynamic rendering in next js]]
	- [[Overcoming shortfalls of dynamic rendering (Streaming)]]
	- Streaming page in next js
	- [[Streaming component in next js]]
- [[Improve application performance - nextjs]]
- [[02. Route groups]]
- **[[Search and Pagination]]**: How to implement search and pagination using URL search params.
- **[[Mutating Data]]**: How to mutate data using React Server Actions, and revalidate the Next.js cache.
	- [[Server Actions]]
	- [[Creation of data using server action]]
	- [[Updating data using server action]]
- **[[Error Handling in Next Js]]:** How to handle general and `404` not found errors.
- **[[Form Validation and Accessibility]]:** How to do server-side form validation and tips for improving accessibility.
- **Authentication**: How to add authentication to your application using [`NextAuth.js`](https://next-auth.js.org/) and Middleware.
- **Metadata**: How to add metadata and prepare your application for social sharing.






1. Creating next js application using the create-next-app cli tool
2. [[Folder structure nextjs]]



### Extra knoweldge
![[Pasted image 20250429194744.png]]

Unrelated
Why optimize images in web application ?
![[Pasted image 20250429223749.png]]
. It's good practice to set the `width` and `height` of your images to avoid layout shift, these should be an aspect ratio **identical** to the source image. These values are _not_ the size the image is rendered, but instead the size of the actual image file used to understand the aspect ratio.


### UUID Vs Incrementing keys
![[Pasted image 20250503023159.png]]

### Passing id![[Pasted image 20250503023624.png]]
