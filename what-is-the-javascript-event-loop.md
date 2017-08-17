# What is the JavaScript Event Loop?

> The event loop is mechanism which look at the call stack and at the callback queue. If the stack is empty it takes the first thing on the queue and pushes it on to the stack which effectively run it.

Some simplified background information:

JavaScript is a single threaded programming language, it has a single call stack and it can do one thing at a time.

> One thread === one call stack === one thing at a time

The JavaScript runtime in the browser (v8 in this case) is composed of:

- The heap, where memory allocation happens (unstructured region of memory).
- The call stack, which is where your stack frames (functions) are and it is used to keep track of what function is currently being run, what functions are called from within that function and should be called next, etc. 

The browser also provides:
- APIs which are extra things that the browser provides. DOM, AJAX, time out, etc.
- Callback queue, which is a list of functions to be processed. When the stack has enough capacity, a function is taken out of the queue and processed. The callback queue is simply a staging area for functions waiting to be invoked and moved over to the call stack.
- The event loop's job is to look at the call stack and at the callback queue. If the stack is empty it takes the first thing on the queue and pushes it on to the call stack which effectively run it.

Synchronous code example:

In the following example, both functions are added on the stack and executed synchronous one after another.

```javascript
var first = function () {  
  console.log('first');
};

var second = function () {  
  first();
  console.log('second');
};

second();

/*
 *  Results:
 *  => first
 *  => second
 */
```

Asynchronous code example:

In the following example, the first and second `console.log` are executed synchronously and are being added in the call stack. `setTimeout()` instead is executed asynchronous and is being added in the callback queue. Only when the  stack is empty, the event loop will take `setTimeout` and push it to the call stack which effectively run it.

The delay parameter in `setTimeout` will add a message to the queue after the time passed as a second argument. If there is no other message in the queue, the message is processed right away; however, if there are messages, the `setTimeout` message will have to wait for other messages to be processed. For that reason the second argument indicates a minimum time and not a guaranteed time.

```javascript
console.log('start');

setTimeout(function cb(){
   // asynchronous handled by browser API
   console.log('cb');
}, 0);

console.log('end');

/*
 *  Results:
 *  => start
 *  => end
 *  => cb
 */
```


Useful resources:

[Concurrency model and Event Loop](https://developer.mozilla.org/en/docs/Web/JavaScript/EventLoop)

[Philip Roberts: What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

[Stack/event loop/callback visualizer](http://latentflip.com/loupe/)
