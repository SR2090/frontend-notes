```ts
let person : {
	name: string;
	age: number;
}

// type Person = // type definition
type Person = person;
let people: Person[];

```

this is a ts only feature. Give a complex base type an alias to use it everywhere else in your code. The type keyword is used to define type alias.