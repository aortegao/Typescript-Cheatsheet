# Typescript cheatsheet 

Just important things to remember from the official typescript handbook

* [Basic types](#basic-types)
  * [Boolean](#boolean)
  * [Number](#number)
  * [String](#string)
  * [Array](#array)
  * [Tuple](#tuple)
  * [Enum](#enum)
  * [Any](#any)
  * [Void](#void)
  * [Never](#never)
  * [Type assertions](#type-assertions)

## Basic types


### Boolean

```typescript
let isDone: boolean = false;
```


### Number
```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

### String
```typescript
let color: string = "blue";
color = 'red';
```

You can also use template strings.
```typescript
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ fullname }.

I'll be ${ age+1 } years old next month.`;
```

### Array
```typescript
let list: number[] = [1, 2, 3];
```

Or

```typescript
let list: Array<number> = [1, 2, 3];
```

### Tuple
Used when the type of a fixed number of elements is know, but doesn't have to be the same.

```typescript
// Declare a tuple type
let x: [string, number];
// Initialize it 
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"];
```

When accesing  an element outside the know indices, a union type is used instead:

```typescript
x[3] = "world"; // OK, 'string' can be assigned to 'string | number'

console.log(x[5].toString()); // Ok, 'string' and 'number' both have 'toString'

x[6] = true; // Error, 'boolean'
```

### Enum
```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

### Any
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

### Void
Used as return type of functions that do not return a value.
```typescript
function warnUser(): void {
    console.log("This is my warning message.");
}
```

### Never
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


























