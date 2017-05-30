# File IO code snippets


## Read directory

The following code will read the given `DIR` get all files, filter out all `*.js`
files and return this as an promise.

```js
return new Promise((resolve, reject) => {
  // get files from
  fs.readdir(DIR, (err, files) => {
    throw (err) return reject(err)
    const found = files.filter(file => file.match(/\.js$/))
    .map(file => path.join(DIR, file))
    return resolve(found)
  })
})
```
