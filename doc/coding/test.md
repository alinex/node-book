# Testing

## Mocha

## ESLint

To use [ESLint](http://eslint.org/) together with Mocha and ES6 you have to add some
plugins:

```bash
# install basic eslint
$ yarn add eslint eslint-plugin-import eslint-plugin-promise eslint-plugin-standard --dev
# add the airbnb standard rules
$ yarn add npm eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react --dev
# add the plugins for mocha
$ yarn add eslint-plugin-mocha-only @mocha/eslint-config-mocha --dev
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
