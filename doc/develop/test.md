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
Another possibility is [Chai](http://chaijs.com/) which allows also to use an
expect style which is more consistent as should.

Here in Alinex mostly Chai with expect style will be used.

### Installlation

```bash
$ npm install mocha chai --save-dev
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
$ npm run test
```

### Writing tests

An example test may look like:

```js
import chai from 'chai'
import request from 'request'

import server from '../../src/server'

const expect = chai.expect

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
    expect(files, 'config.files').to.have.lengthOf(1)
  })

})
```

The test itself starts with the `expect` method which should be given the object
to test and the information about what is tested. This makes the error messages
readable. after that a concatenation of helpful words and assertion definitions will
follow (some as functions):

```js
expect(files, 'config.files').to.have.lengthOf(1)
```

### Plugins

There are lots of [Plugin](http://chaijs.com/plugins/) for chai to use but only
some of them which are decided as very useful are shown here.

__Promises__

This is done using the extension [chai-as-promised](http://chaijs.com/plugins/chai-as-promised/)
which was also included in the above installation and examples.

Now you may also use the following tests:

```js
import chaiAsPromised from 'chai-as-promised'
chai.use(chaiAsPromised)

expect(promiseFn()).to.be.fulfilled
expect(promiseFn()).to.eventually.deep.equal("foo")
expect(promiseFn()).to.become("foo") // same as `.eventually.deep.equal`
expect(promiseFn()).to.be.rejected
expect(promiseFn()).to.be.rejectedWith(Error) // other variants of Chai's `throw` assertion work too
```

__Http__

[chai-http](http://chaijs.com/plugins/chai-http/) includes a request method which
easily checks the result:

```js
import chaiHttp from 'chai-http'
chai.use(chaiHttp)

chai.request('http://localhost:8080')
  .get('/')
```

__File system__

[chai-fs](http://chaijs.com/plugins/chai-fs/) will allow extensive test on the NodeJS
filesystem. It has a lot of methods from which only some are shown here:

```js
import chaiFs from 'chai-fs'
chai.use(chaiFs)

expect(path).to.be.a.directory().with.files(array)
expect(path).to.be.a.directory().and.empty
expect(path).to.be.a.file().with.json
```

__RegExp matcher__

[chai-match](http://chaijs.com/plugins/chai-match/) will check assertions using
regular expressions:

```js
import chaiMatch from 'chai-match'
chai.use(chaiMatch)

expect('some thing to test').to.match(/some (\w+) to test/).and.capture(0).equals('thing')
```


## ESLint

To use [ESLint](http://eslint.org/) together with Mocha and ES6 you have to add some
plugins:

```bash
$ npm install eslint eslint-plugin-import eslint-plugin-promise eslint-plugin-standard --save-dev
$ npm install npm eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react --save-dev
$ npm install eslint-plugin-mocha-only @mocha/eslint-config-mocha --save-dev
$ npm install babel-eslint eslint-plugin-flowtype --save-dev
```

In the root folder the concrete rules can be specified `.eslintrc.js`:

```js
module.exports = {
  env: { es6: true, node: true },
  extends: 'airbnb',
  parser: "babel-eslint",
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

The `babel-eslint` parser is necessary to also parse the flow annotations correctly.

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


## Monitoring Changes

[Nodemon](https://nodemon.io/) is a utility that will monitor for any changes in
the source and automatically restart the code. Perfect for development.

__Installation__

```bash
$ npm install nodemon --save-dev
```

Now `nodemon` can be used instead of `node` to run the code and it will always stop
and restart the code if the code changes. It can also be used to start any other
executable.

__Automatic tests__

The following `package.json` setup will rerun the linter and unit tests each time
you save changes. It has to be called using `npm run dev`. This is optimal for modules
development.

```json
{
  "scripts": {
    "dev": "nodemon src/index.js --exec 'npm run lint -s && npm run test'",
    "lint": "eslint src --ext .js",
    "test": "nyc --require babel-core/register --require babel-polyfill mocha test/mocha"    
  }
}
```

__Server restart__

To work with server we mostly only lint and then start the application itself.
Therefore set the following `package.json` and also run it using `npm run dev`:

```json
{
  "scripts": {
    "dev": "nodemon src/start.js --exec 'npm run lint; babel-node --require babel-polyfill --exec node_modules/.bin/babel-node'",
    "lint": "eslint src --ext .js"
  }
}
```
