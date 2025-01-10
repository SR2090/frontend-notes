![[Pasted image 20241129165712.png]]
preventing widely used for implementing dark mode in next js


```tsx
"use client"

  

import { ThemeProviderProps } from 'next-themes';

import { ThemeProvider as NextThemesProvider } from 'next-themes';

import React from 'react'

// Wrap entire application in a contenxt and allow us to access theme specific properties like mode

function ThemeProvider({ children, ...props }: ThemeProviderProps) {

  return (

    <NextThemesProvider {...props}>{children} </NextThemesProvider>

  )

}

  

export default ThemeProvider;
```

Using the theme provider in our application
```tsx
export default function RootLayout({

  children,

}: Readonly<{

  children: React.ReactNode;

}>) {

  return (

    <html lang="en">

      <body

        className={`${inter.className} ${spaceGrotesk.variable} antialiased`}

      >

        <ThemeProvider

          attribute="class"

          defaultTheme="system"

          enableSystem

          disableTransitionOnChange

        >{children}</ThemeProvider>

      </body>

    </html>

  );

}
```


## Theme Toggle
