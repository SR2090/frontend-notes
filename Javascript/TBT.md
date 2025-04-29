Here’s a deeper dive into **Total Blocking Time (TBT)**:

---

## What Is Total Blocking Time (TBT)?

- **Definition**: TBT measures the **sum** of all the time slices during which the main thread was **blocked** (i.e. unable to respond to user input) by “Long Tasks” between **First Contentful Paint** (FCP) and **Time to Interactive** (TTI).
    
- A **Long Task** is any task running on the main thread for **>50 ms**—the extra milliseconds beyond that 50 ms threshold count toward your TBT. ([Total Blocking Time (TBT) | Articles - web.dev](https://web.dev/articles/tbt?utm_source=chatgpt.com), [Total Blocking Time | Lighthouse - Chrome for Developers](https://developer.chrome.com/docs/lighthouse/performance/lighthouse-total-blocking-time?utm_source=chatgpt.com))
    

---

## How TBT Is Calculated

1. **Record all tasks** on the main thread after FCP until TTI.
    
2. **Identify Long Tasks**: any task with duration > 50 ms.
    
3. **Compute blocking time** per task:  
    ```  
    blockingTime = taskDuration – 50 ms  
    ```
    
4. **Sum** those blocking times across all Long Tasks → **Total Blocking Time**.
    

### Example Breakdown

|Task Duration|Blocking Time (duration – 50 ms)|
|---|---|
|250 ms|200 ms|
|90 ms|40 ms|
|35 ms|0 ms (not a Long Task)|
|30 ms|0 ms|
|155 ms|105 ms|
|**Total**|**345 ms TBT**|

> Even though the main thread was busy for 560 ms in total, only 345 ms of that actually “blocked” input handling. ([Total Blocking Time (TBT) | Articles - web.dev](https://web.dev/articles/tbt?utm_source=chatgpt.com))

---

## Why TBT Matters

- **User Perception**: High TBT means the page feels sluggish—clicks, taps or keypresses can’t be handled until blocking work finishes.
    
- **Lab Proxy for FID**: In lab tools (e.g. Lighthouse), TBT correlates strongly with **First Input Delay** (FID) and helps predict real-world input delays. ([Measure And Optimize Total Blocking Time (TBT) - DebugBear](https://www.debugbear.com/docs/metrics/total-blocking-time?utm_source=chatgpt.com))
    
- **Lighthouse Scoring**: TBT makes up 25 % of your Performance score in Lighthouse/PSI. ([Measure And Optimize Total Blocking Time (TBT) - DebugBear](https://www.debugbear.com/docs/metrics/total-blocking-time?utm_source=chatgpt.com))
    

---

## Relation to Other Metrics

- **FCP**: Marks when you first see content; doesn’t guarantee interactivity.
    
- **TBT**: Quantifies _how much_ the browser was blocked _after_ that first paint.
    
- **TTI**: The point when the page is reliably interactive. TBT is only measured _up to_ TTI.
    
- **FID**: Field metric measuring actual delay on first user interaction; TBT is a lab stand-in for FID.
    

---

## Strategies to Reduce TBT

1. **Break up long JavaScript**
    
    - Split large functions into smaller async chunks
        
    - Use `requestIdleCallback` or `setTimeout(fn, 0)` to yield back to the browser
        
2. **Code-split & defer**
    
    - Only load scripts when needed (`<script defer>` or dynamic `import()`)
        
3. **Offload work**
    
    - Move heavy computation into Web Workers
        
4. **Minimize render-blocking resources**
    
    - Inline critical CSS, defer non-critical CSS and JS
        
5. **Audit with Long Tasks**
    
    - Use Chrome’s Performance panel to spot and slice up tasks > 50 ms
        

---

By focusing on trimming down or breaking up your Long Tasks—and deferring any non-critical work—you can drive your TBT (and thus your real and perceived interactivity) way down.

![[Pasted image 20250427202456.png]]