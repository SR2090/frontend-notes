### Function Return Type declaration
```ts
export default function Layout({ children }: { children: React.ReactNode }): React.JSX.Element {
```


Example TSX component
```ts
const Layout = ({ children }: { children: React.ReactNode }): React.JSX.Element => {

    return <>

        <nav></nav>

        <main>

            {children}

        </main>

    </>

}

  

export default Layout;
```