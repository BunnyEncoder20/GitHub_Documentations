- TypeScript has only one job : Static Type checking
- Javascript does not have this by default.
- **TS** is just a development tool. It is not a independent language and it's just a wrapper on top of native JS.

## Types 

1. Number 
2. String 
3. Boolean
4. Null
5. Undefined 
6. Void 
7. Object 
8. Arrays
9. Tuples
10. ...

- There is also **ANY** (never, unknow) types, which should not really be used unless absolutely necessary. Due to these, we are making the code more like JS again, defeating the whole point of using TS in the first place.
- **void** is used if a function is not going to return a value (like a function which only logs something to the console).
- Sometimes, a function can also **never** return a value (like a function made to throw new errors). Hence there are 2 different types. 

- Proper Documentations of TS can be found at [Typescript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#the-primitives-string-number-and-boolean)

## The primitives

1. String 
2. Numbers 
3. Booleans

## Arrays 

To specify the type of an array like `[1, 2, 3]`, you can use the syntax `number[]`; this syntax works for any type (e.g. `string[]` is an array of strings, and so on).

```typescript
let users:string[] = [] // 1D array
let scores:number[][] = [[],[],[]] // 2D array
let powerLevels: Array<number> = [] // Array<T> special TS type
```
- We can also have arrays of types :
```typescript
let User = {
	readonly _id:string,
	name:string,
	email:string,
	isActive:boolean
}

let indian_users:User[] = []
```

## Functions 

- When making functions, we can type their parameters and their return types as well.
- Eg:
```Typescript
// Parameter type annotation
function greet(name: string) {
	console.log("Hello, " + name.toUpperCase() + "!!");
}
```

```Typescript
function getFavoriteNumber(): number {
	return 26;
}
```

- **NOTE :** What will happen when a function can have more than 1 return type ?

## Type Alias 

```Typescript
// This is a type alias
type Point = {
  x: number;
  y: number;
};
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

- We can even make new types by combining previously crated types like : 
```typescript
type cardNumber = {
	long_card_num : number
}

type cardExpiry = {
	exp_date : Date
}

type Card = cardNumber & cardExpiry & {
	cvv : number
}
```
- Note that the **&** means that all of the types mentioned are required.

## TypeScript Special Keywords

1. **readonly** is a special keyword used before variables which we do not want to change in our code. Eg: MongoDB \_id property.
```typescript
type User = {
	readonly _id:string,
	name:string,
	email:string,
	isActive:boolean
}

let my_new_user:User = {
	_id = "12345",
	name = "bunny",
	email = "b@gmail.com",
	isActive = true
}

my_new_user._id = "5678" // Throws type error : cannot change readonly property
```

2. **?** is used when we want to mark a variable/field as optional

```Typescript
type User = {
	_id : string,
	name : string,
	creditCard? : number 
}
```