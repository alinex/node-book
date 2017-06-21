# Promises

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
  let p = Promise.resolve()
  jobs.forEach((fn) => {
    p = p.then(() => fn.call(this, data))
  })
  return p.then(() => data)
  .catch(err => (err ? Promise.reject(err) : data))
}
```

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
