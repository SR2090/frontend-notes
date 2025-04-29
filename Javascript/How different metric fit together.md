Here’s how the pieces fit together:

- **FCP (First Contentful Paint)**  
    Marks when the browser renders the first bit of “content” (text, image, SVG, canvas) to the screen. It doesn’t say anything about interactivity—just “you saw something” ([First Contentful Paint (FCP) | Articles - web.dev](https://web.dev/articles/fcp?utm_source=chatgpt.com)).
    
- **TBT (Total Blocking Time)**  
    Measures the sum of all _blocking portions_ of Long Tasks (>50 ms) that occur **between FCP and TTI**.
    
    - A “blocking portion” is task-duration minus the initial 50 ms (e.g. a 120 ms task contributes 70 ms of blocking).
        
    - TBT is a _diagnostic_ metric: it tells you how much time the main thread was busy doing long JavaScript work that _could_ block user input. ([Total Blocking Time (TBT) | Articles - web.dev](https://web.dev/articles/tbt?utm_source=chatgpt.com), [Total Blocking Time | Lighthouse - Chrome for Developers](https://developer.chrome.com/docs/lighthouse/performance/lighthouse-total-blocking-time?utm_source=chatgpt.com))
        
- **TTI (Time to Interactive)**  
    The moment when the page:
    
    1. Has displayed useful content (i.e. FCP has happened),
        
    2. Has registered event handlers for most visible elements, and
        
    3. Consistently responds to user input within 50 ms.  
        Until TTI, the page is _not_ reliably interactive—even if you can see parts of it. ([What is TTI (Time To Interactive)? What does it say about your ...](https://uploadcare.com/blog/time-to-interactive/?utm_source=chatgpt.com), [Time to Interactive | Lighthouse - Chrome for Developers](https://developer.chrome.com/docs/lighthouse/performance/interactive?utm_source=chatgpt.com))
        
- **FID (First Input Delay)**  
    The delay between a user’s very first action (click, tap, keypress) and the browser’s ability to respond. In lab tools, TBT often correlates with—and is used as a proxy for—FID. ([Time To Interactive Examples & Best Practices - Catchpoint](https://www.catchpoint.com/core-web-vitals/time-to-interactive?utm_source=chatgpt.com))
    

---

### So… what you’re observing

> _“Once the first element paints, I still can’t interact until everything else loads.”_

- **That “can’t interact until everything else loads”** is captured by **TTI**, not by TBT alone.
    
- **TBT** only sums up the _blocked_ time slices between FCP and TTI; it doesn’t measure the _absolute_ delay until full interactivity.
    
- The true “time until you can reliably click or type” is **TTI**, and the _quality_ of that wait (how janky it felt) is diagnosed by **TBT**.
    

In short:

- Use **TBT** to pinpoint and quantify long-running JavaScript work that blocks input.
    
- Look at **TTI** to know when your page actually becomes interactive.
    
- And measure **FID** in the field to see the real-world delay users experience on first interaction.