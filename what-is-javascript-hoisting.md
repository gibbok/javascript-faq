# What is JavaScript Hoisting?

Short answer:

> Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

## ES5

Variable declarations are processed before any code is executed, declaring a variable anywhere in the code is equivalent to declaring it at the top. This also means that a variable can appear to be used before it's declared. 

The scope of a variable declared with the keyword `var` is its current execution context, which is its enclosing function or global if declared outside any functions (top level). 


## Example with global variables:

```javascript

console.log(message);
message = 'Hello world!'; // Hello world!
var message;
```

JavaScript has hoisted the variable declaration `message`. This code is implicitly understood as:

```javascript

var message;
message = 'Hello world!';
console.log(message); // Hello world!

```

Notes: Hoisting does not affect the variable value initialization. The value will be assigned when the assignment statement is reached.

## Example with function as execution context:

```javascript

function sayMessage() {
  console.log(message); // undefined
  var message = 'Hello world!';
}

sayMessage();

```

This is how the interpreter views the above code:

```javascript

function sayMessage() {
	var message;
	console.log(message); // undefined
	message = 'Hello world!';
	console.log(message); // Hello world!
}

sayMessage();

```

## ES6

Variables declared with the keyword `let` are block scoped and not function scoped as `var`. 


```javascript

var a = 'a';

{
	let a = 'b';    // block scoped
	console.log(a); // b
}

console.log(a);     // a

```

Also `let` bindings are not subject to variable Hoisting.

Consider:


```javascript

console.log( a );	// undefined
console.log( b );	// ReferenceError (TDZ - Temporal Dead Zone)

var a; // hoisted
let b; // not hoisted

```

## Block-scoped Functions
Function declarations inside of blocks are in ES6 specified to be scoped to that block. 

```javascript

{
	let sayHello = function() {
		console.log('Hellow world!');
	};
	sayHello();
}

sayHello(); // ReferenceError

```


### Useful resources:

[Block-scoped variables](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md#let-declarations)

[Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
