# Asynchronism

JavaScript has Asynchronism as its base feature. And the most of its performance
comes out of this. But its not really easy to use asynchronous methods and combine
them together.

With ES5 callback methods are used everywhere and if you have to call multiple
asynchronous methods one after another you send the next method as callback to the
first. This makes the so named "callback hell" because the code will look like a
pyramid. To solve this there are different efforts:
- async libraries
- promises
- async/await

Each one is build on top of it. To make the code readable Alinex modules uses async/await
and Promises whenever possible.


## Async libraries

While still working with callbacks some libraries like [async.js](http://caolan.github.io/async/)
comes with multiple methods to simplify the management of callbacks.

That's how Alinex worked earlier.


## Promises

Promises, have been around quite a while and are defined by a spec called
[Promise/A+](https://promisesaplus.com/). ES6 has adopted this spec for its Promise
implementation adhere to this spec and offer other features on top of it.

Promises give helps in handling asynchronous processing in a more synchronous fashion.
They represent a value that can be handled at some point in the future. And, better
than callbacks here, Promises give us guarantees about that future value:
- No other registered handlers of that value can change it (the Promise is immutable)
- It is guaranteed that a value will be receive, regardless of when the handler
  is registered, even if it's already resolved.


## Async/Await

Node now supports async/await out of the box since version 7.6. As a quick overview:
- Async/await is a new way to write asynchronous code.
- Async/await is actually built on top of promises and is non blocking.
- Async/await makes asynchronous code look and behave a little more like synchronous
  code.

The function need the keyword `async` before it. The `await` keyword can only be
used inside functions defined with `async`. Any `async` function returns a promise
implicitly, and the resolve value of the promise will be whatever is given by `return`.

```js
function timeout(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const wait = async () => {
  console.log(await timeout(5))
  return "done"
}
wait()
```

`await` can't be used in the top level main method because it is not defined using `async`.
But it can be given by auto calling method.

### Error handling

It's not only clean code to use `await` but it makes the error handling real easy.

Async/await makes it finally possible to handle both synchronous and asynchronous
errors with the same construct, good old try/catch. With promises, the try/catch will
not handle if a method fails because it´s happening inside a promise. We need to call
`.catch` on the promise and duplicate our error handling code.
With async/await the catch block will handle parsing errors.

```js
const makeRequest = async () => {
  try {
    // this parse may fail
    const data = JSON.parse(await getJSON())
    console.log(data)
  } catch (err) {
    console.log(err)
  }
}
```
