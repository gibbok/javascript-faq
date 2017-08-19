# What is currying in JavaScript?

Short answer


> Currying is the technique of translating the evaluation of a function that takes multiple arguments into evaluating a sequence of functions, each with a single argument. It essentially creates a chain of partially applied functions that eventually resolves with a value.


In a curried function its several arguments are rewritten such that it accepts the first argument and returns another function that accepts the second argument and so on. This allows functions of several arguments to have some of their initial arguments partially applied.

> Currying is a useful technique, with which you can partially evaluate functions.

## Notes:
When currying we need to know how many arguments our function expects (called its "arity"). Otherwise, we won’t know when to stop returning new functions and give back a value instead.

Example without currying:

```javascript

function add (a, b) {
  return a + b;
}

add(3, 4); // 7

```

The curried function:

```javascript

function add (a) {
  return function (b) {
    return a + b;
  }
}

add(3)(4); // 7

```

### Useful resources:
[Partial Application in JavaScript](https://johnresig.com/blog/partial-functions-in-javascript/#postcomment)
[A Beginner’s Guide to Currying in Functional JavaScript](https://www.sitepoint.com/currying-in-functional-javascript/)
