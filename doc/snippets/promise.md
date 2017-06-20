# Promises

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
