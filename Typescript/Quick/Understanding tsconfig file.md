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
