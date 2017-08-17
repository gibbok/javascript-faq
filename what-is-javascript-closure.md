# What is JavaScript closure?

Short answer:

> A closure is an inner function that has access to the outer (enclosing) function’s variables.


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
  var counter = 0;
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


Emulating private methods with closures. JavaScript does not provide a native way of doing this, but it is possible to emulate private methods using closures.


```javascript
var testModule = (function() {
  // counter and reset cannot be seen outside testModule
  var counter = 0;
  var reset = function(){
     counter = 0;
  };

  return {
    incrementCounter: function() {
      counter++;
      console.log(counter);
      return counter;
    },

    resetCounter: function() {
      console.log(`counter value prior to reset: ${counter}`);
      reset();
      console.log(counter);
    }
  };

})();

testModule.incrementCounter(); // 1
testModule.incrementCounter(); // 2
testModule.incrementCounter(); // 3

testModule.resetCounter();     // 0
testModule.incrementCounter(); // 1

```



