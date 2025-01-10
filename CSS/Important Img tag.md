```js
  <Box component="img" src={SideBar} alt="Not found" sx={{

            borderRadius: "8px",

            objectFit: "contain",

            height: "98%",

            width: "auto",

            overflow: "hidden",

            padding: "8px"

        }} />
```

objectFit contain will make the image fit the parent container. 
Another property value cover takes up the entire image size and that will lead to distortion of the image.
98% height is taken to prevent scrolling as the padding causes the content to overflow. The parent component has height of 100vh.
Width auto will help the image maintain aspect ratio.
overflow will prevent any scroll.

![[Pasted image 20241031024326.png]]



Another scenario can be we can make the parent div prevent overflow and use object-fit :cover on the image this will make the image fit the container appropriately 

Giving max-width: 100% is better than width:100% because the former will prevent image distortion. Example if the container is 100px wide and the image is just 20px then with the former the width of the image will be 20px but for latter it will be 100px making the final image distorted.

### Key Differences

1. **`max-width: 100%`**
    
    - Ensures that the image never exceeds the width of its container.
    - If the image is smaller than the container, it retains its original size, preventing distortion.
    - **Example Behavior**:
        - Image is 20px wide, container is 100px wide: Image remains 20px wide.
        - Image is 200px wide, container is 100px wide: Image shrinks to 100px wide, maintaining aspect ratio.
2. **`width: 100%`**
    
    - Forces the image to stretch or shrink to match the container's width, regardless of its original size.
    - If the image's natural dimensions do not match the container, it can become distorted.
    - **Example Behavior**:
        - Image is 20px wide, container is 100px wide: Image stretches to 100px wide, leading to distortion.
        - Image is 200px wide, container is 100px wide: Image shrinks to 100px wide, maintaining aspect ratio only if height is automatically adjusted.

---

### Why `max-width: 100%` is Often Better for Images

- **Prevents Distortion**: It allows the image to scale down to fit within the container, but it won't force it to stretch beyond its natural size.
- **Responsive Design**: In fluid layouts, it ensures the image scales proportionally within varying container widths.