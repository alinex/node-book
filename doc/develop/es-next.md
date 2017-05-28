# ES.Next JavaScript

At the moment I already write new code in the upcoming new language
standards like ES6 and newer...

ES6 also known as ECMAScript 2015 adds significant new syntax for writing complex
applications, including classes and modules. Other new features include iterators
and for/of loops, Python-style generators and generator expressions, arrow functions,
binary data, typed arrays, collections (maps, sets and weak maps), promises, number
and math enhancements, reflection, and proxies.

ES7 also known as ECMAScript 2016 adds only two new functionalities:
- `Array.prototype.includes`
- Exponentiation Operator

ES8 officially named ECMAScript 2017 will add:
- `Object.values`/`Object.entries`
- String padding
- `Object.getOwnPropertyDescriptors`
- Trailing commas in function parameter lists and calls
- Async Functions using async/awaut

Learn more about this:
- [ES6 Overview examples](http://es6-features.org/#StringInterpolation)
- [ES6 Learning tutorial](https://babeljs.io/learn-es2015/)
- [ES8 Async/await](http://stackabuse.com/node-js-async-await-in-es7/)

Browser and server support for ES2015 is still incomplete but it can be transpiled
into ES5 code to work (see below).


## Babel

[Babel](http://babeljs.io/) is a JavaScript compiler which will take modern JavaScript
code and transpile them into an older language using transformations and polyfills.
Essentially this makes the code runable in an environment which didn't support
the newest JavaScript standards.

For the Alinex modules this is used to already use the newest language features
while also get it working today.

### Installation

First you need to install Babel CLI within your project as development requirement
and you will also need some additional presets:

```bash
# using yarn:
$ yarn add babel-cli babel-preset-es2015 babel-preset-stage-0 babel-polyfill --dev
# alternative using npm:
$ npm install babel-cli babel-preset-es2015 babel-preset-stage-0 babel-polyfill --save-dev
```

## Usage

To make it usable you also have to add a configuration file `.babelrc` in your project
root and specify the installed presets to be used:

```json
{
  "presets": ["es2015", "stage-0"],
  "plugins": [],
  "comments": false
}
```

Now you can integrate babel with your project by defining it's call in the scripts
section of `package.json`:

```json
{
  "scripts": {
    "dev": "node_modules/.bin/babel-node src/index.js --require babel-polyfill",
    "build": "babel src -d dist --require babel-polyfill",
    "start": "node dist/index.js",
    "prepublish": "npm run build"
  }
}
```

This defines the babel transformation to:
1. Be used as JIT compiler in dev mode (run using `yarn dev`)
2. Be converted into ES5 code by running `yarn build` (into `dist` folder)
3. Everything in dist folder can be used without babel
4. Before publishing to npm the `build` command is called automatically

The babel polyfills are needed to use the async/await which will come with
node 7.6.


## Coding Rules

The following rules defines the basics which are derived from the
[Airbnb Style Guide](https://github.com/airbnb/javascript/blob/master/README.md).
If configured the linter (see more under [Testing](test.md)) will ensure that these
rules are followed.

A compact list of the essential rules are:
- avoid using `var`
- literal object creation
- use object method shorthand
- use property shorthand
- use single quote strings
- use template strings
