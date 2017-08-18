# What is currying in JavaScript?

Short answer

> Currying is when you break down a function that takes multiple arguments into a series of functions that take part of the arguments.

A curried function is a function of several arguments rewritten such that it accepts the first argument and returns a function that accepts the second argument and so on. This allows functions of several arguments to have some of their initial arguments partially applied.

Currying is the technique of translating the evaluation of a function that takes multiple arguments into evaluating a sequence of functions, each with a single argument.


Currying refers to the process of taking a function with n arguments and transforming it into n functions that each take a single argument. It essentially creates a chain of partially applied functions that eventually resolves with a value.

Currying is the process of taking a function that accepts some number of arguments, then creating a new version of that function that can accept an "incomplete" argument list. 

Briefly, currying is a way of constructing functions that allows partial application of a function’s arguments. What this means is that you can pass all of the arguments a function is expecting and get the result, or pass a subset of those arguments and get a function back that’s waiting for the rest of the arguments. It really is that simple.



```javascript
function add (a, b) {
  return a + b;
}

add(3, 4); returns 7
```

```javascript
function add (a) {
  return function (b) {
    return a + b;
  }
}
```



we need to know how many arguments our function expects (called its “arity”). Otherwise, we won’t know when to stop returning new functions and give back a value instead.


https://johnresig.com/blog/partial-functions-in-javascript/#postcomment