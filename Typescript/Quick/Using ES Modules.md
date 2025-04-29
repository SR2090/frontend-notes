You can import it in the same you do in javascript but the file extension should be .js instead of .ts|
More maintainable, manageable code

1. **Import/Export Basics**
    
    - **Named vs Default**:
        
        ```ts
        // named
        export function doThing() { /*…*/ }
        import { doThing } from "./module";
        
        // default
        export default class Foo { /*…*/ }
        import Foo from "./module";
        ```
        
    - **Type‑only Imports** (no runtime cost):
        
        ```ts
        import type { User } from "./types";
        ```
        
2. **`tsconfig.json` Module Targets**
    
    - `"module": "esnext"` (or `"es2020"`) for native dynamic `import()` & tree‑shaking.
        
    - `"module": "commonjs"` if you’re building for Node without bundling.
        
3. **Module Resolution Modes**
    
    - **Node**: follows `node_modules`, `package.json` `"exports"` / `"main"`.
        
    - **Classic**: legacy TS behavior—only for backwards‑compat, rarely used.
        
4. **Path Aliases & “Barrels”**
    
    ```jsonc
    // tsconfig.json
    {
      "compilerOptions": {
        "baseUrl": "./src",
        "paths": { "@utils/*": ["utils/*"] }
      }
    }
    ```
    
    —avoid deep relative imports (`../../../`), improve readability.
    
5. **Dynamic `import()` & Code‑Splitting**
    
    ```ts
    const { heavy } = await import("./heavy");
    heavy();
    ```
    
    —returns a `Promise`, perfect for lazy‑loading UI chunks or large libraries.
    
6. **Tree‑Shaking Friendly**
    
    - **ES Modules** allow bundlers to drop unused exports.
        
    - **Namespaces** & CommonJS can’t tree‑shake effectively.
        
7. **Declaration Files for Interop**
    
    - When importing a vanilla JS package:
        
        ```bash
        npm install package-name
        npm install --save-dev @types/package-name
        ```
        
    - Or write `declare module "legacy-lib";` to silence TS errors.
        
8. **Side‑Effect Imports**
    
    ```ts
    import "./setup-polyfills";     // runs top‑level code, no exports
    import "reflect-metadata";      // common in decorators
    ```
    
9. **Circular Dependency Awareness**
    
    - ES Modules resolve bindings live, so you may get `undefined` if you import too early.
        
    - **Interview tip**: explain how the “temporal dead zone” and hoisting differ from CommonJS.
        
10. **Top‑Level `await`** (in `"module": "esnext"` / Node ≥ 14)
    
    ```ts
    // only valid in ES modules
    const data = await fetchData();
    console.log(data);
    ```
    
11. **Bundler vs. Native**
    
    - **Native** in browsers: zero‑config demos, learning.
        
    - **Bundler (Webpack/Rollup)** for:
        
        - Polyfills & transpilation (older browsers)
            
        - Asset imports (CSS, images)
            
        - Filename hashing & caching
            
12. **Interview Mnemonic**
    
    > **“Static exports, dynamic imports, path aliases, plus tree‑shakeable bundles.”**
    
    - **Static exports** → TS can analyze & optimize
        
    - **Dynamic imports** → async code‑splitting
        
    - **Path aliases** → maintainable codebase
        
    - **Tree‑shakeable bundles** → smaller, faster apps



## More on ES Modules
Using alias with the help of as keyword
![[Pasted image 20250421165038.png]]

Case of default input:
![[Pasted image 20250421165335.png]]
We can use any name instead of the original default name, ![[Pasted image 20250421170154.png]]
The default export will be used



### Type based import
![[Pasted image 20250421170733.png]]
This annotation specifies that the given imported feature is a ts only feature.
If you import interface or type we can annotate it with the type keyword.

If all the imports from the file are types then we can use the following.![[Pasted image 20250421171033.png]]
