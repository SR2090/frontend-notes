Entire JS is bundled into a single file. This will increase page load time for large bundle size. It might be case where the user does not navigate to a page but we already have it's javascript downloaded.

To improve page load time we should utilize lazy loading i.e. when the user nagviates to a page or uses a function then only it should be loaded.

For a simple module,
```js
// Without code splitting: Entire module loads at once
import { heavyFunction } from "./heavyModule";
heavyFunction();

// With code splitting: Module loads only when needed
import("./heavyModule").then(({ heavyFunction }) => {
  heavyFunction();
});

```

Consider having a dashboard page and a home page. Initial load should render the home page, the dashboard page is not required, so we render it as and when required.
In react using Lazy And Suspense
```js
const Dashboard = lazy(() => import("./Dashboard"));
function App() { return ( <div> <h1>Welcome</h1> <Suspense fallback={<p>Loading...</p>}> <Dashboard /> </Suspense> </div> ); }

export default App;
```




![[Pasted image 20250202173853.png]]


![[Pasted image 20250202174332.png]]

![[Pasted image 20250202174339.png]]



### Route based code splitting
![[Pasted image 20250202174536.png]]
```js
import React, { lazy, Suspense } from "react";
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";

// Lazy load components
const Home = lazy(() => import("./Home"));
const About = lazy(() => import("./About"));
const Contact = lazy(() => import("./Contact"));
const NotFound = lazy(() => import("./NotFound"));

function App() {
  return (
    <Router>
      <Suspense fallback={<h2>Loading...</h2>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </Suspense>
    </Router>
  );
}

export default App;

```

![[Pasted image 20250202174627.png]]
![[Pasted image 20250202174544.png]]

Does not support named export but works with default exports


### Benefits

![[Pasted image 20250202174637.png]]

## Resource
https://yuvrajpy.medium.com/frontend-performance-optimization-with-code-splitting-using-react-lazy-suspense-1e0d1a85e32c