# Testing

Software Testing is necessary because we all make mistakes. Some of those mistakes
are unimportant, but some of them are expensive or dangerous. We need to check
everything and anything we produce because things can always go wrong – humans make
mistakes all the time.

Ideally, someone else should check our work because another person is more
likely to spot the flaws.

Automatic tests help to find some of the problems but the tests will never be perfect
and couldn't guaranty error free code. How and then to make this tests can be
different:

- Write the tests first and then code till everything succeeds.
- Write your code and then the tests to ensure it will also keep working for the future.
- Write tests for each bug, then fix it till the test succeeds.
- Neither write tests.

The tests itself may be unit tests which check some internal part of the software or
end-to-end test which checks whole procedures.


## Mocha

[Mocha](https://mochajs.org/) is a feature-rich JavaScript test framework running
on Node.js and in the browser, making asynchronous testing simple and fun.
Mocha tests run serially, allowing for flexible and accurate reporting, while mapping
uncaught exceptions to the correct test cases.

### Helper

As mocha itself needs a powerful assertion library to check within the tests
[Should.js](https://shouldjs.github.io/) allows just this. It supports a lot of
methods which can be used to check any object.

There are a lot of other alternatives like [Chai](http://chaijs.com/)...
Here in Alinex the Should.js library is often used.

### Installlation

```bash
# yarn install
$ yarn add mocha should should-http --dev
# alternative npm install
$ npm install mocha should should-http --save-dev
```

This will install the modules. The tests itself are mostly stored in the folder
`test/mocha`.

```json
{
  "scripts": {
    "test": "mocha --require babel-core/register --require babel-polyfill test/mocha"
  }
}
```

Now you can run your tests using:

```bash
# run using yarn
$ yarn test
# alternative npm call
$ npm run test
```

### Writing tests

An example test may look like:

```js
import should from 'should'
import shouldHttp from 'should-http'
import request from 'request'

import server from '../../src/server'

// start server before tests
before((cb) => {
  server.init({ logging: null }) // no request logging needed
  server.start()
  .then(cb)
})

// stop server after tests
after(() => {
  server.stop()
})

// run the tests
describe('server', () => {

  it('should have default folders', async () => {
    const compiler = new Compiler({schemaPath: 'test/data/config'})
    const files = await compiler.schema()
    files.should.be.above(1)
  })

})
```


## ESLint

To use [ESLint](http://eslint.org/) together with Mocha and ES6 you have to add some
plugins:

```bash
# install basic eslint
# add the airbnb standard rules
# add the plugins for mocha
$ yarn add eslint eslint-plugin-import eslint-plugin-promise eslint-plugin-standard --dev
$ yarn add npm eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react --dev
$ yarn add eslint-plugin-mocha-only @mocha/eslint-config-mocha --dev
# do the same using npm
$ npm install eslint eslint-plugin-import eslint-plugin-promise eslint-plugin-standard --save-dev
$ npm install npm eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react --save-dev
$ npm install eslint-plugin-mocha-only @mocha/eslint-config-mocha --save-dev
```

In the root folder the concrete rules can be specified `.eslintrc.js`:

```js
module.exports = {
  env: { es6: true, node: true },
  extends: 'airbnb',
  parserOptions: { sourceType: 'module' },
  rules: {
    'indent': [ 'error', 2 ],
    'linebreak-style': [ 'error', 'unix' ],
    'quotes': [ 'error', 'single' ],
    'semi': [ 'warn', 'never' ],
    'no-unused-vars': [ 'warn' ],
    'no-console': [ process.env.NODE_ENV === 'production' ? 'error' : 'warn' ]
  }
};
```

And extend the mocha template for your test folder by placing an  `test/mocha/.eslintrc.js`
file in your test folder:

```js
module.exports = {
  extends: [ 'mocha/es6' ],
  rules: {
    quotes: 'off',
    no-unused-vars: 'off',
    no-console: 'off'
  }
};
```

If you want some explanation for a rule best way ist too look up Google using the message
or the rule name combined with `eslint`. Or look directly in the
[rules index](http://eslint.org/docs/rules).
