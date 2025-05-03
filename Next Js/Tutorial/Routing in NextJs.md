![[Pasted image 20250429225206.png]]


## FIle based routing 
- the file structure defines the routing path![[Pasted image 20250429225319.png]]
- To make route accessible you have to create page .Tsx file inside the folder this is going to be the content that gets displayed corresponding to the route. d in the app is going to be the place where the child which is the nested folders are going to get rendered.![[Pasted image 20250429225852.png]]


## How to make a folder a route![[Pasted image 20250429230320.png]]
Make sure that folder has a page.tsx file



## Purpose of layout.tsx
All the common UI elements like header, footer, sidebar etc go in this place. 
#### Benefit:
1. on navigation, only the page components update while the layout won't re-render. #nextjslearn This is partial rendering maintaining client side react state
Example

```tsx
import SideNav from '@/app/ui/dashboard/sidenav';
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
      <div className="w-full flex-none md:w-64">
        <SideNav />
      </div>
      <div className="flex-grow p-6 md:overflow-y-auto md:p-12">{children}</div>
    </div>
  );
}
```

![[Pasted image 20250429232559.png]]

![[Pasted image 20250429232609.png]]


## Root Layout![[Pasted image 20250429233624.png]]


# Navigation between pages
![[Pasted image 20250429233701.png]]

When using **a** tag for navigation the entire page reloads. but instead switching to Link we will utilize client side navigation


## Benefits of using Link tag

To improve the navigation experience, Next.js automatically code splits your application by route segments. This is different from a traditional React [SPA](https://nextjs.org/docs/app/building-your-application/upgrading/single-page-applications), where the browser loads all your application code on the initial page load.

Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work. This is also less code for the browser to parse, which makes your application faster.

Furthermore, in production, whenever [`<Link>`](https://nextjs.org/docs/api-reference/next/link) components appear in the browser's viewport, Next.js automatically **prefetches** the code for the linked route in the background. By the time the user clicks the link, the code for the destination page will already be loaded in the background, and this is what makes the page transition near-instant!


## Showing active links
1. use the hook usePathname() to check the path and then implement this pattern. #nextjslearn 
2. its a react hook the component needs to converted into a client component.
```tsx
"use client"

import {

  UserGroupIcon,

  HomeIcon,

  DocumentDuplicateIcon,

} from '@heroicons/react/24/outline';

import Link from 'next/link';

import clsx from 'clsx';

import { usePathname } from 'next/navigation';

// Map of links to display in the side navigation.

// Depending on the size of the application, this would be stored in a database.

const links = [

  { name: 'Home', href: '/dashboard', icon: HomeIcon },

  {

    name: 'Invoices',

    href: '/dashboard/invoices',

    icon: DocumentDuplicateIcon,

  },

  { name: 'Customers', href: '/dashboard/customers', icon: UserGroupIcon },

];

  

export default function NavLinks() {

  const pathname = usePathname()

  console.log(pathname, "pathname")

  return (

    <>

      {links.map((link) => {

        const LinkIcon = link.icon;

        return (

          <Link

            key={link.name}

            href={link.href}

            className={clsx("flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3", {

              'bg-sky-100 text-blue-600': pathname === link.href,

            })}

          >

            <LinkIcon className="w-6" />

            <p className="hidden md:block">{link.name}</p>

          </Link>

        );

      })}

    </>

  );

}
```


![[Pasted image 20250430122136.png]]
