# What is JavaScript closure?

Short answer:

> A closure is an inner function that has access to the outer (enclosing) function’s variables-scope.


A closure can be created by adding a function inside another function. The inner function has access not only to the outer function’s variables, but also to the outer function’s parameters.

In JavaScript, closures are created every time a function is created, at function creation time.

```javascript

function sayHello(firstName, lastName) {
  var intro = 'Hello my name is';
  // nested functions have access to variables and parameters declared in their outer scope
  function createMessage() {
    return `${intro} ${firstName} ${lastName}`;
  }

  return createMessage();
}

var message = sayHello('James', 'Bond'); // Hello my name is James Bond
alert(message);

```


## Interesting aspects:

Closures have access to the outer function’s variable even after the outer function returns.

Example:

```javascript
var add = function() {
  var counter = 0; // lexical environment
  return function() {
    counter += 1;
    alert(counter);
    return counter;
  }
}();

add();  // 1
add();  // 2
add();  // 3 

```


Closures are commonly used to give objects data privacy.


```javascript
var module = function(){
    // counter and reset are not visible outside module
	var counter = 0;
	var reset = function(){
		counter = 0;
	};
	return {
		increment: function(){
			counter++;
			console.log(counter);
		},
		reset: function(){
			reset();
		}
	};

};

var moduleA = module();
moduleA.increment(); // 1
moduleA.increment(); // 2
moduleA.increment(); // 3
moduleA.reset();     // 0

var moduleB = module();
moduleB.increment(); // 1
moduleB.increment(); // 2 

```

In functional programming, closures are frequently used for partial application & currying.


## Lexical Scope

Lexical scoping describes how a parser resolves variable names when functions are nested. The word "lexical" refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. In JavaScript nested functions have access to variables declared in their outer scope.

---

### Useful resources:

[Lexical Scope](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/ch2.md#chapter-2-lexical-scope)

[Closures on MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)
