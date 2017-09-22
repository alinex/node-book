# Mocha Testing


## Set timeout

You need to use a named function to get the right context and therefore the ability to set the
timeout. In a lambda function this is not possible.

```js
describe('greylist', function greylisttest() {
  this.timeout(5000)
  ...
})
```

## Don't run on Travis

Because some specific tests may not work in the Travis environment you have to skip them but only there.

```js
const notTravisDescribe = process.env.TRAVIS ? describe.skip : describe
const notTravisIt = process.env.TRAVIS ? it.skip : it

// now you can skip a block
notTravisDescribe('simple', () => {
  it('should work', () => {
    ...
  })
  it('should work, too', () => {
    ...
  })
})

// or only skip one test
describe('simple', () => {
  it('should work', () => {
    ...
  })
  notTravisIt('should work, too', () => {
    ...
  })
})
```
