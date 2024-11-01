![[Pasted image 20241002141857.png]]


The useReducer hook accepts the reducer fuction, this function will have a state and an action.
The action is dispatched when calling the useRedcuer.
The staet is the latest state snapshot of the state used by the reducer. Similar to one we get during funciton form.

![[Pasted image 20241002143753.png]]
The useReducer hook will accept the reducer function and an initial state.

```js
const shoppingCartReducer = (state, action) => {
	if(action.type === "ADD_ITEM") {
		const updatedItems = [...state.items];
		const existingItemIndex = upadtedItems.findIndex((item) => item?.id === action.payload);
		const existingCartItem = updatedItems[existingItemIndex];
		 // If present then remove the quanitity 
		 // If not then add it to the list
		 return {
		 ...state, 
		// new updates
		 }
	}
}
```


Calling an action method
```js
function addItemToCart(id) {
	// Reducer obtained from the useReducer hook
	shoppingCartDispatch({
		type: "ADD_ITEM",
		payload: id
	})
}
```




# React `useReducer` Hook

The `useReducer` hook is an alternative to `useState` for managing more complex state logic in React. It allows you to handle state transitions in a predictable manner by providing a reducer function that manages how the state changes in response to different actions.

## Syntax

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```


```
- `state`: The current state returned by the `useReducer` hook.
- `dispatch`: A function to trigger the execution of the reducer function with a specific action.
- `reducer`: A function that defines how the state will be updated based on the action.
- `initialState`: The initial value of the state.
```


## Key Concepts
### 1. Reducer Function:
The reducer function takes two arguments: `state` and `action`. It returns a new state based on the action type.
- `state`: The latest snapshot of the state, similar to how state works in function components with `useState`.
- `action`: An object that describes how the state should change. It typically has a `type` property, but it can also include additional data.
```js
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error('Unknown action type');
  }
}
```

### 2. Dispatching an Action
The `dispatch` function is used to trigger the reducer with an action. For example:
```js
dispatch({ type: 'increment' });
```

This will trigger the increment logic
#### 3. Initial State
The `initialState` can be a static value or a function that returns the initial state. If you need to compute the initial state, you can use a function for optimization.
```js
const [state, dispatch] = useReducer(reducer, { count: 0 });
```
#### 4. Lazy Initialization
If the initial state is expensive to calculate, you can pass an `init` function as the third argument to `useReducer` to lazily initialize the state.
```js
function init(initialCount) {
  return { count: initialCount };
}

const [state, dispatch] = useReducer(reducer, initialCount, init);

```
### Basic Counter Implementation using useReducer
```js
import React from "react";

export function counterReducer(state, action) {
    if(action.type === "INCREMENT") {
        return {count: state.count + 1}
    }
     if(action.type === "DECREMENT") {
        return {count: state.count - 1}
    }
     if(action.type === "RESET") {
        return {count: 0}
    }
    return state;
}

function App() {
    const [counterState, counterStateDispatch] = React.useReducer(counterReducer, {
        count: 0
    });
    
  return (
    <div id="app">
      <h1>The {counterState?.count} Counter</h1>
      <p id="actions">  
        <button onClick={() => counterStateDispatch({type: "INCREMENT"})}>Increment</button>
        <button onClick={() => counterStateDispatch({type: "DECREMENT"})}>Decrement</button>
        <button onClick={() => counterStateDispatch({type: "RESET"})}>Reset</button>
      </p>
      <p id="counter">{counterState?.count}</p>
    </div>
  );
}

export default App;

```




# When to useReducer
- When you have complex state logic involving multiple sub-values. (In a cart)
- When the next state depends on the previous one.
- When managing state that needs more predictability, especially in larger components.