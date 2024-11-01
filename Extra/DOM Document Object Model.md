It represents the structure of an HTML or XML document as a tree of objects, where each node is an object representing a part of the document, such as an element, attribute, or piece of text. By manipulating the DOM, developers can dynamically change the content, structure, and style of a web page.

### DOM Overview

- **Tree Structure**: The DOM represents a document as a hierarchical tree where the root node is the document itself, and each element (like `<div>`, `<p>`, `<a>`, etc.) and text inside it is a node.
- **Node Types**: There are different types of nodes, like **element nodes** (HTML tags), **text nodes** (text inside elements), **attribute nodes** (attributes like `class` or `id`), and **document nodes** (the document itself).
- **Live Representation**: The DOM is a live model of the document, so any changes made to it reflect immediately in the browser.

### Common Web APIS
```js
const header = document.getElementById('header');
```

![[Pasted image 20241031194702.png]]
getElementsByTagName returns an array


![[Pasted image 20241031194713.png]]

![[Pasted image 20241031194916.png]]




### Creating Removing Nodes
![[Pasted image 20241031194959.png]]


### Event Listner
![[Pasted image 20241031195057.png]]


#### Traversal
![[Pasted image 20241031195124.png]]

