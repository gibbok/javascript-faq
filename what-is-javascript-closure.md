# What is JavaScript closure?

Short answer:

> A closure is an inner function that has access to the outer (enclosing) function’s variables-scope.


A closure can be created by adding a function inside another function. The inner function has access not only to the outer function’s variables, but also to the outer function’s parameters.


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
var module = (function(){
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

})();

module.increment(); // 1 
module.increment(); // 2 
module.increment(); // 3 
module.reset();     // 0 
module.increment(); // 1 

```


## Lexical Scope

Lexical scoping describes how a parser resolves variable names when functions are nested. The word "lexical" refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. In JavaScript nested functions have access to variables declared in their outer scope.


---


A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
To use a closure, simply define a function inside another function and expose it. To expose a function, return it or pass it to another function.
The inner function will have access to the variables in the outer function scope, even after the outer function has returned.



In functional programming, closures are frequently used for partial application & currying.


https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36








https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/ch2.md#chapter-2-lexical-scope