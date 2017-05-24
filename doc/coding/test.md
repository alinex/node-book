# Testing

## Mocha

## ESLint

To use [ESLint](http://eslint.org/) together with Mocha and ES6 you have to add some
plugins:

```bash
$ yarn add eslint eslint-config-standard eslint-plugin-import eslint-plugin-promise eslint-plugin-standard eslint-plugin-mocha-only @mocha/eslint-config-mocha --dev
```

Also extend the mocha template for your test folder by placing an  `test/.eslintrc.js`
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
