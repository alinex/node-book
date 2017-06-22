# Promises

Promises are a way out of the callback hell. They are standardized after
[Promise A+](https://promisesaplus.com/) and are a part of ES6. Here are some special cases.

## Synchronous functions

A list of functions (maybe mixed with promise based and synchronous) can be processed one after
each other by concatenating them with an initially created fulfilled Promise.

```js
const jobs = [] // list of normal or Promise based functions

// normal
jobs.push((data) => {
  if (data === undefined) throw new Error('Data argument is needed.')
  return data
})
// and as promised
jobs.push((data) => {
  if (typeof data === 'function') {
    Promise.reject(new Error('Function as data not supported!'))
  }
  Promise.resolve(data)
})

function process(input: any): Promise<any> {
  let data = input
  // run rules seriously
  let p = Promise.resolve(input)
  jobs.forEach((fn) => {
    p = p.then(data => fn.call(this, data))
  })
  return p.then(data => data)
  .catch(err => (err instanceof Error ? Promise.reject(err) : err))
}
```

This pattern also for three possibilities within each serious function:
- `resolve(result)` or `return result` to send the result and go on
- `reject(new Error(...))` or `throw new Error(...)` to stop processing with fail
- `reject(result)` or `throw result` to stop further processing but with success


## Resolve outside of Promise

In some cases you want to resolve a promise on a specific event from the outside:

```js
let promiseResolve
let promiseReject

var promise = new Promise((resolve, reject) => {
  promiseResolve = resolve
  promiseReject = reject
})

promiseResolve()
```
