## **React Lifecycle Methods**

React components have lifecycle phases that dictate how they are created, updated, and destroyed. These phases are managed through lifecycle methods (for class components) and **React Hooks** (for function components).

---

## **Phases of the React Component Lifecycle**

1. **Mounting (Component is Created and Inserted into the DOM)**
2. **Updating (Component is Re-rendered due to State/Prop Changes)**
3. **Unmounting (Component is Removed from the DOM)**

---

## **Lifecycle Methods in Class Components**

|Phase|Method|Purpose|
|---|---|---|
|**Mounting**|`constructor()`|Initializes state and binds methods.|
||`static getDerivedStateFromProps(props, state)`|Updates state based on props before render (rarely used).|
||`render()`|Renders UI.|
||`componentDidMount()`|Runs after first render (used for API calls, subscriptions).|
|**Updating**|`static getDerivedStateFromProps(props, state)`|Updates state before render when props change.|
||`shouldComponentUpdate(nextProps, nextState)`|Controls re-rendering (returns `true` or `false`).|
||`render()`|Re-renders UI when state/props change.|
||`getSnapshotBeforeUpdate(prevProps, prevState)`|Captures info before update (used for scroll positions).|
||`componentDidUpdate(prevProps, prevState, snapshot)`|Runs after re-render (used for API calls after prop/state change).|
|**Unmounting**|`componentWillUnmount()`|Cleanup function (removes timers, event listeners, API calls).|

---

## **Lifecycle in Functional Components (Using Hooks)**

Since React 16.8, functional components rely on hooks to handle lifecycle events.

|Lifecycle in Class Component|Equivalent Hook in Functional Component|
|---|---|
|`componentDidMount`|`useEffect(() => { ... }, [])`|
|`componentDidUpdate`|`useEffect(() => { ... }, [dependency])`|
|`componentWillUnmount`|`useEffect(() => { return () => { ... } }, [])`|

### **Example using `useEffect`**

```jsx
import { useState, useEffect } from "react";

function MyComponent({ propValue }) {
  const [count, setCount] = useState(0);

  // Runs once when component mounts
  useEffect(() => {
    console.log("Component mounted");

    return () => {
      console.log("Component will unmount");
    };
  }, []);

  // Runs when `propValue` changes
  useEffect(() => {
    console.log("Prop changed:", propValue);
  }, [propValue]);

  return <div>Count: {count}</div>;
}
```

---

## **Lifecycle Mnemonic: "MCU"**

- **M** → **Mounting** (`componentDidMount / useEffect([])`)
- **C** → **Changing (Updating)** (`componentDidUpdate / useEffect([dependency])`)
- **U** → **Unmounting** (`componentWillUnmount / useEffect cleanup`)

This mnemonic helps recall the three key phases of a React component’s lifecycle. 🚀
