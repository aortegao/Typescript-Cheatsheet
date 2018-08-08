Just important things to remember from the official typescript handbook

* [Basic types](#basic-types)
  * [Boolean](#boolean)
  * [Number](#number)
  * [String](#string)
    * [Template strings](#template-strings)
  * [Array](#array)
  * [Tuple](#tuple)
    * [Union types](#union-types)
  * [Enum](#enum)
  * [Any](#any)
  * [Void](#void)
  * [Never](#never)
  * [Type assertions](#type-assertions)
* [Variable declarations](#variable-declarations)
  * [`let` declarations](#let-declarations)
    * [Block scoping](#block-scoping)
	* [Cannot use blocked scoped variables before declared](#cannot-use-blocked-scoped-variables-before-declared)
  * [`const` declarations](#const-declarations)
    * [`const` is not _inmutable_](#const-is-not-inmutable)
  * [Destructuring](#destructuring)
    * [Array destructuring](#array-destructuring)
	* [Object destructuring](#object-destructuring)
	  * [Property renaiming](#property-renaiming)
  * [Spread]($spread)
    * [Array spread](#array spread)
	* [Object spread](#object spread)

# Basic types


## Boolean

```typescript
let isDone: boolean = false;
```


## Number
```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

## String
```typescript
let color: string = "blue";
color = 'red';
```

### Template strings
You can also use template strings.
```typescript
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ fullname }.

I'll be ${ age+1 } years old next month.`;
```

## Array
```typescript
let list: number[] = [1, 2, 3];
```

Or

```typescript
let list: Array<number> = [1, 2, 3];
```

## Tuple
Used when the type of a fixed number of elements is know, but doesn't have to be the same.

```typescript
// Declare a tuple type
let x: [string, number];
// Initialize it 
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"];
```

### Union types
When accesing  an element outside the know indices, a union type is used instead:

```typescript
x[3] = "world"; // OK, 'string' can be assigned to 'string | number'

console.log(x[5].toString()); // Ok, 'string' and 'number' both have 'toString'

x[6] = true; // Error, 'boolean'
```

## Enum
```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

## Any
Used for opting-out of type-checking and let the values pass through compile-time checks.
```typescript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

The any type is also in handy if you know some part of the type, buth perhaps not all of it. For example, you may have an array but the array has a mix of different types:

```typescript
let list: any[] = [1, true, "free"];

list[1] = 100;
```

## Void
Used as return type of functions that do not return a value.
```typescript
function warnUser(): void {
    console.log("This is my warning message.");
}
```

## Never
`never` is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns.

```typescript
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(Message);
}

// Inferred return type is never
function fail() {
    return error("Something failed");
}

function infiniteLoop(): never {
    while (true) {
	}
}
```

## Type assertions

Type assertions is like a type cast in other languages, but performs no special checking or restructuring of data. It has no runtime impact,
and is used purely by the compiler. There are two forms. One is the "angle-bracket" syntax:

```typescript
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

And the orhter is the `as` -syntax:
```typescript
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

# Variable declarations

## `let` declarations 
### Block scoping
`let` statements are declarations with block-scoping.

```typescript
function f(input: boolean) {
    let a = 100;
	
	if (input) {
	    // Still okay to reference 'a'
		let b = a + 1;
		return b;
	}
	
	// Error: 'b' doesn't exist here
}
```

### Cannot use blocked scoped variables before declared

```typescript
a++; // illegal to use 'a' before it's declared;
let a;
```

## `const` declarations
`const` cariables value cannot be changed once they are bound.

### `const` is not _inmutable_
```typescript
const numLivesForCat = 9;
const kitty = {
    name: "Aurora",
	numLives: numLivesForCat
};

// Error 
kitty = {
    name: "Danielle",
	numLives: numLivesForCat
};

// all "okay"
kitty.name = "Rory";
kitty.name = "Kitty";
kitty.name = "Cat";
kitty.numLives--;
```

## Destructuring

### Array destructuring
The simplest form of destructuring is array destructuring assignment:
```typescript
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2
```

Is the same as:
```typescript
first = input[0];
second = input[1];
```

Destructuring works with already-declared variables:
```typescript
// swap variables
[first, second] = [second, first];
```

And with parameters to a function:
```typescript
function f([first, second]: [number, number]) {
    console.log(first);
	console.log(second);
}
f([1, 2]);
```

You can create a variable for the remaining items in a list using the syntax `...`:
```typescript
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4];
```

Of course, since this is Javascript, you can just ignore trailing elements you don't care about:
```typescript
let [first] = [1, 2, 3, 4]
console.log(first) // outputs 1
```

Or other elements:
```typescript
let [, second, , fourth] = [1, 2, 3, 4];
```

### Object destructuring 
You can also destructure objects:
```typescript
let o = {
    a: "foo",
	b: 12,
	c: "bar"
};

let { a, b } = o;
```

You can create a variable for the remaining items in an object using the syntax `...`:
```typescript
let { a, ...passthrough } = o;
let total = passthrough.b + passthrough.c.length;
```

#### Property renaming
You can also give different names to properties:
```typescript
let { a: newName1, b: newName2 } = o;
```

Is equal to:
```typescript
let newName1 = o.a;
let newName2 = o.b;
```

## Spread
It allows you to spread an array into another array, or an object into another object. 

### Array spread
```typescript
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
```
 This gives `bothPlus` the value `[0, 1, 2, 3, 4, 5]`. Spreading creates a shallow copy of `first` and `second`. **They are not changed by the spread**
 
### Object spread
```typescript
let defaults = { food: "spicy", price: "$$", ambiance: "noisy"}
let search = { ...defaults, food: "rich"};
```

Now `search` is `{ food: "rich", price: "$$", ambiance:"noicy"}`. In object spreading **properties that come later in the spread object overwrite properties that 
come earlier**.




