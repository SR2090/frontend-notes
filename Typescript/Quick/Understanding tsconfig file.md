Each project can be individually configured
Just learn it based on when you encounter each of them.
If want the settings of tsconfig to be applied then you should compile the project without specifying a single file.

```ts
tsc --watch
// Will recompile the ts file each time there is a change.
```

```json
1. {
2. "target": "ES2022", // Good for modern browsers or Node.js
3. "compilerOptions": {
4. "esModuleInterop": true, // Ensures ESM and CJS imports work together well
5. "skipLibCheck": true, // Ensures .d.ts files from 3rd libraries are not type-checked
6. "target": "es2022", // Sets a relatively modern ECMAScript version as compilation target
7. "allowJs": true, // Allows importing .js files into .ts (helpful when migrating projects)
8. "strict": true, // Ensures strict type checking (i.e., noImplicitAny etc)
9. "noUncheckedIndexedAccess": true, // Adds undefined as a value when accessing by index
10. // "noImplicitOverride": true, // Enable this when working with classes & inheritance
11. "noUnusedLocals": true, // to avoid unused variables
12. "module": "NodeNext", // Supports both ESM & CJS modules / imports
13. "outDir": "dist", // Store compiled files in "dist" folder
14. "sourceMap": true, // Enables source maps for easier debugging
15. "lib": ["es2022", "dom", "dom.iterable"] // Or without "dom" libs when building for Node
16. }
17. }
```
## Just the ones worth your while
![[Pasted image 20250407222013.png]]

If true it would cry out error error each time you do not specify the error.


This is a typescript file for configuration specification in this file we can specify the compiler option the files that should be included for compiling, project structure.

```json
{
  "compilerOptions": {
    // Compiler settings
  },
  "include": [
    // List of files or directories to include
  ],
  "exclude": [
    // List of files or directories to exclude
  ],
  "files": [
    // Explicit list of files to compile
  ],
  "references": [
    // References to other tsconfig files for a multi-project setup
  ]
}

```

#### 1. **`compilerOptions`**

Defines how TypeScript should behave during compilation.

- **`target`**: Specifies the JavaScript version to output.
    
    - Example: `"es5"`, `"es6"`, `"esnext"`
- **`module`**: Specifies the module system to use.
    
    - Example: `"commonjs"`, `"esnext"`, `"umd"`
- **`strict`**: Enables all strict type-checking options.
    
    - Example: `true` (recommended)
- **`baseUrl`**: Sets the base path for module resolution.
    
    - Example: `"./src"`
- **`paths`**: Maps module names to specific locations for imports.
-  **`outDir`**: Specifies the output directory for compiled files.
    
    - Example: `"./dist"`
- **`rootDir`**: Specifies the root directory of input files.
    
    - Example: `"./src"`
- **`sourceMap`**: Generates `.map` files for debugging.
    
    - Example: `true`
- **`jsx`**: Specifies JSX handling for React projects.
    
    - Example: `"react"`, `"react-jsx"`
- **`typeRoots`**: Specifies directories containing type declarations.
    
    - Example: `["./node_modules/@types"]`
- **`lib`**: Specifies built-in TypeScript libraries to include.
    
    - Example: `["es2015", "dom"]`


```json
{
  "paths": {
    "@components/*": ["components/*"]
  }
}

```

![[Pasted image 20250105160133.png]]
![[Pasted image 20250105160139.png]]
![[Pasted image 20250105160149.png]]
![[Pasted image 20250105160156.png]]
![[Pasted image 20250105160203.png]]

![[Pasted image 20250105160210.png]]
