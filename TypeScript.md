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


## Unions

- Union is the combination of 2 or more types.
- We use the **|** operator for that.

```typescript
type user = {
	name : string,
	id : number
}

type admin = {
	emp_name : string
	emp_id : number
}

let new_user:user|admin = {}
```
- If we expect one or more type of parameters, then before doing any manipulations on the param, we need to verify it's type
```typescript
let func1 = (id:number|string) => {
	if (typeof id=="number")
		id.toLowerCase()
	elsif (typeof id=="string")
		id+10
	return id
}
```
- This is called as **union narrowing**
- This is useful in arrays also if we want our array to have multiple types within it 
```typescript
const data:number[] | string[] = ["2", 3]  // will give error cause this means that data can be either complete array of numbers or complete array of strings

const data:(number|string)[] = [1,"2",3]  // this will work
```

## Enums

- When we want to give restrictive options in code, **enums** are very good 
```typescript
enum seat_choice = {
	AISLE = "aisle",
	MIDDLE = "middle",
	WINDOW = "window",
	FIRST_CLASS = "first"
}

const new_seat = seat_choice.WINDOW // this has the value = "window"
```
- While making node apps, these are extensively used in things like constants, such as status codes :
```typescript
const enum StatusCodes = {
    OK = 200,
    CREATED = 201,
    BAD_REQUEST = 400,
    UNAUTHORIZED = 401,
    FORBIDDEN = 403,
    NOT_FOUND = 404,
    CONFLICT = 409,
    UNPROCESSABLE = 422,
    INTERNAL_SERVER_ERROR = 500
};

export {
    StatusCodes
};
```


## Interface

- you could see interface as a lose overview of something like a class 

```typescript
interface user = {
	readonly dbID:number,
	readonly userID:number,

	email:string,
	name:string,
	batchNo:number,

	startTrail():string   // is a function which retunrs a string
	getCoupon(couponName:string, off:number):number // also a function with types params and returns a number
}

const new_user = {
	dbID:22,
	userID:33,

	email:"b@b.com,
	name:"bunny",
	batchNo:44,

	startTrail: () => { return "Congrats Trail Started";}
	getCoupon: (cName:"bunny",off:10) = {return 10}
}
```

- If we want to add more properties to a interface, we can simply redeclare the interface and do so. This is called *re-opening* of a interface.
```typescript
interface user = {
	readonly dbID:number,
	readonly userID:number,

	email:string,
	name:string,
	batchNo:number,

	startTrail():string 
	getCoupon(couponName:string, off:number):number
}

interface user = {
	github_token:string
}
```

- We can also inherit from other interfaces, similar to classes.
```typescript
interface admin extends user {
	role:"admin"|"ta"|"qa"|"intern"|"emp"
}
```

- **NOTE** that though very similar to *type*, **interfaces** are different. They can add new values to themselves by reopening and can be inherited. 
- **types** cannot add more properties to themselves and can inherit properties from other types only by using the "**&**" symbol.

