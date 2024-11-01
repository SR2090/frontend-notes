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

objectFit contain will make the image fit the parent container. Another property value cover takes up the entire image size and that will lead to distortion of the image.
98% height is taken to prevent scrolling as the padding causes the content to overflow. The parent component has height of 100vh.
Width auto will help the image maintain aspect ratio.
overflow will prevent any scroll.

![[Pasted image 20241031024326.png]]