![[Pasted image 20250429203241.png]]
The problem with browser is when it initially renders the page it uses the fall back font because the actual font that was required was not downloaded,  After it goes through we are going to have to see a shift.

In next year's this problem is mitigated if we use next/fonts. He does this by downloading the font during the build time and then hosting it in the public assets so when the user first receives his page he is going to see the final font instead of the rollback.
Another benefit it hosts font files with other static assets so that there are no additional network requests.


## Steps to add primary fonts
fonts.ts

- In your `/app/ui` folder, create a new file called `fonts.ts`.
- All the fonts that will be used in our application will be kept in this file.

fonts.ts
```tsx
import { Inter } from 'next/font/google';
 
export const inter = Inter({ subsets: ['latin'] });
```


![[Pasted image 20250429211118.png]]
#### Adding the font to a body element.
![[Pasted image 20250429211130.png]]


## Image handling

Well handling when working with images in next year's application we should use the image component it handles all the image optimization![[Pasted image 20250429224545.png]]

![[Pasted image 20250429224656.png]]



## Extra learning 
![[Pasted image 20250429225056.png]]

https://nextjs.org/learn/dashboard-app/optimizing-fonts-images