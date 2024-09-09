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
- Interfaces are used mostly to make sure that certain properties and methods are followed at all cost. We can add more properties if we want to but, not less than what is defined in the interfaces, if it is implemented into a class
```typescript
interface camera {
	camera_mode:string,
	filter:string,
	burst:number
}

class insta implements camera {
	// we must make sure that all the properties of interface camera are taken care of.
	constructor(
		public camera_mode:string,
		public filter:string,
		public burst:number
	){}
}

class youthoob implements camera {
	// if we want we can have more properties, but must include the ones in the implemented interface
	constructor (
		public camera_mode:string,
		public filter:string,
		public burst:number,
		public short:string
	){}
}
```


## Classes in TS

- Similar to classes in JS, just typed

```typescript
class User {
	email:string,
	name:string
	constructor(email:string,name:string){
		this.email = email;
		this.name = name;
	}
}

const new_user = new User("bunny@gmail.com","bunny");
```
- **Note** that the properties of the class should have proper initialisers.
- There are *access modifiers* in TS also namely : 
	- **private** : this doesn't allow access to that property outside the class
	- **public** : any property by default is public
	- **protected** : this means that the property will be accessible within the class and any other child class which inherits from the class. (**Reminder** by default, private variables are not inherited by children class) 
- For production level code, sometimes, people just define the access of variables in the constructor params itself

```typescript
// generates exactly same JS as above example
class User {
	constructor(
		public email:string,
		public name:string,
		private userID:number
	){
		this.email = email;
		this.name = name;
		this.userID = generateUserID()
	}
}

const new_user = new User("bunny@gmail.com","bunny");
console.log(new_user.userID) // will gives error
```

- Generally to access private variables, we want to use getters and setters in TS:
```typescript
class User {
	constructor(
		public email:string,
		public name:string,
		private userID:number,
		private city:string = "Mumbai"
	){
		this.email = email;
		this.name = name;
		this.userID = generateUserID()
	}

	// this is a getter function
	get get_userID():number{
		return this.userID
	}

	get get_companyEmail(name:string,empID:number):string{
		return `${name}.${empID}@apple.com`
	}

	// this is a setter function
	set set_cityName(city:string){
		this.city = city
	}
}

const new_user = new User("bunny@gmail.com","bunny");
console.log(new_user.get_userID())  // this will not throw an error now
```
- **Notice** how the *set* function do not have a return type hint as these functions are not meant to return anything.


## Generics 

- Behind the scenes, makes all of our components reusable.
- It was made to define the types of identity functions(which take in and return the same type) however these could also take in various types
```javascript
function identityFunc(val){
	return val
}
```
- We want to type the above function, basically we want the incoming param type to also be the return type of the function. 
- But the incoming type of the param could be anything. We could tackle this partially by using *any* or **|** but that would not be a ideal solution.
- Hence we use Generics for situations like this. Defined by **<>** 
```typescript
funciton indentityFunc<Type>(val:Type):Type{
	return val
}
```
- Note that *type* name could be anything, so people usually use a smaller format eg:
```typescript
funciton indentityFunc<T,>(val:T):T{
	return val
}
```
- The **,** within the <T,> is there to signal that this is not a *JSX* tag but a TS type.
- You can also use custom types like *interfaces*,*types*, etc
```typescript
interface bottle {
	brand:string,
	bottle_id:number,
	bottle_type:string
}

funciton indentityFunc<bottle,>(val:bottle):bottle{
	return val
}
```


