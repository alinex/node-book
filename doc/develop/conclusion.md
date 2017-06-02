# Conclusion

The basic settings used for my new modules are:

| Software     | Comment |
| ------------ | ------- |
| Node >= 6    | Allows to use ES6 |
| Babel        | Transpiler used for functionality up to stage-3 |
| Mocha        | To run unit tests |
| Flow         | For typüechecking |


## Initial file structure

All tools together used as an development environment will look like:

    .babelrc                # babel configuration
    .eslintrc.js            # eslint setup
    .flowconfig             # for typechecking setup
    .git                    # git store
    .gitignore              # files to not add to git
    .npmignore              # files to not publish
    .travis.yml             # vm setup for travis
    book.json               # api book setting
    doc/                    # api book
        cover.jpg           # cover image for pdf, epub
        cover_small.jpg     # cover image for pdf, epub
        README.md           # introduction chapter...
        styles/             # styles for book
          ebook.css         # epub styles
          pdf.css           # pdf styles
          website.css       # web view styles
        SUMMARY.md          # index tree of book
    package.json            # nodejs meta data
    README.md               # short info displayed on npm and github
    src/                    # sources
      index.js              # start for coding...
    test/                   # test data
      mocha/                # mocha test suites
        .eslintrc.js        # eslint changes for mocha test suites
        index.js            # start for tests...


## Configuration files

The files will look like:

__.babelrc__

```json
{
  "presets": [
    ["env", { "targets": { "node": 6 } }],
    "stage-3",
    "flow"
  ],
  "plugins": [],
  "comments": false
}
```

__.eslintrc.js__

```js
module.exports = {
  env: { es6: true, node: true },
  extends: 'airbnb',
  parser: "babel-eslint",
  parserOptions: { sourceType: 'module' },
  rules: {
    'max-len': [ 'warn', 100 ],
    'indent': [ 'error', 2 ],
    'linebreak-style': [ 'error', 'unix' ],
    'quotes': [ 'error', 'single' ],
    'semi': [ 'warn', 'never' ],
    'spaced-comment': 'warn',
    'no-unused-vars': [ 'warn' ],
    'no-console': [ process.env.NODE_ENV === 'production' ? 'error' : 'warn' ],
    'no-shadow': ['error', { 'allow': ['cb', 'err'] }],
    'import/prefer-default-export': 'warn'
  }
};
```

__.gitignore__

```bash
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Coverage tools like jscoverage/JSCover, nyc or istanbul
lib-cov
coverage
.nyc_output

# Build tools like npm, yarn, grunt or bower
.grunt
bower_components
.npm
/*.tgz
.yarn-integrity

# Other caching like eslint or repl
.eslintcache
.node_repl_history

# Dependency directories
node_modules/
jspm_packages/

# Compiled code
dist

# Runtime data
local
```

__.npmignore__

```bash
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Coverage tools like jscoverage/JSCover, nyc or istanbul
lib-cov
coverage
.nyc_output

# Build tools like npm, yarn, grunt or bower
.grunt
bower_components
.npm
/*.tgz
.yarn-integrity

# Other caching like eslint or repl
.eslintcache
.node_repl_history

# Dependency directories
node_modules/
jspm_packages/

# Development folder
doc
book.json
src
test
/.*

# Runtime data
local
```

__travis.yml__

```yaml
language: node_js
node_js:
#  - "4"  # LTS   from 2015-10 maintenance till 2018-04
  - "6"  # LTS   from 2016-10 maintenance till 2019-04
  - "7"  # devel from 2016-10
#  - "8"  # LTS   from 2017-10 maintenance till 2019-12
#  - "9"  # devel from 2017-10
os:
  - linux
#  - osx   # not possible because of mongodb service

# Additional services
services:
  - mongodb

# run with coveralls integration
script: "npm run-script test-travis"
after_script: "cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js"

# Fix the c++ compiler on Ubuntu 14.04
env:
  - CXX=g++-4.8
addons:
  apt:
    sources:
      - ubuntu-toolchain-r-test
    packages:
      - g++-4.8
```

__book.json__

```json
{
  "root": "./doc",

  "pdf": {
    "pageNumbers": true,
    "headerTemplate": " ",
    "footerTemplate": " "
  },

  "plugins": [
    "todo", "mermaid-gb3", "puml",
    "toggle-chapters", "navigator", "downloadpdf"
  ],
  "pluginsConfig": {
    "downloadpdf": {
      "base": "https://www.gitbook.com/download/pdf/book/alinex/xxxxxx",
      "label": "Download PDF",
      "multilingual": false
    }
  }
}
```

__package.json__

```json
{
  "name": "alinex-NAME",
  "version": "2.1.4",
  "description": "Some descriptive text.",
  "copyright": "Alexander Schilling 2014-2017",
  "private": false,
  "keywords": [
    "check",
    "validate",
    "sanitize",
    "schema"
  ],
  "homepage": "http://alinex.github.io/node-NAME/",
  "repository": {
    "type": "git",
    "url": "https://github.com/alinex/node-NAME"
  },
  "bugs": "https://github.com/alinex/node-NAME/issues",
  "author": {
    "name": "Alexander Schilling",
    "email": "info@alinex.de",
    "web": "http://alinex.de"
  },
  "contributors": [],
  "license": "Apache-2.0",
  "main": "./dist/index.js",
  "scripts": {
    "dev": "nodemon src/index.js --exec 'yarn flow && yarn lint && yarn unit'",
    "build": "babel src -d dist --require babel-polyfill",
    "start": "cross-env NODE_ENV=production node dist/index.js",
    "precommit": "npm run lint",
    "prepublish": "npm run build",
    "unit": "nyc --require babel-core/register --require babel-polyfill mocha test/mocha",
    "test": "npm run flow && npm run lint && npm run unit",
    "test-travis": "nyc --reporter=lcov --require babel-core/register --require babel-polyfill mocha test/mocha",
    "lint": "eslint src --ext .js"
  },
  "directories": {
    "lib": "./dist"
  },
  "dependencies": {
    "chalk": "^1.1.3",
    "debug": "^2.6.3"
  },
  "devDependencies": {
    "babel-cli": "^6.24.1",
    "babel-eslint": "^7.2.3",
    "babel-polyfill": "^6.23.0",
    "babel-preset-env": "^1.5.1",
    "babel-preset-flow": "^6.23.0",
    "babel-preset-stage-3": "^6.24.1",
    "babel-register": "^6.24.1",
    "chai": "^4.0.0",
    "chai-as-promised": "^6.0.0",
    "coveralls": "^2.13.1",
    "eslint": "^3.19.0",
    "eslint-config-airbnb": "^15.0.1",
    "eslint-config-mocha": "^0.0.0",
    "eslint-config-standard": "^10.2.1",
    "eslint-plugin-flowtype": "^2.34.0",
    "eslint-plugin-import": "^2.2.0",
    "eslint-plugin-jsx-a11y": "^5.0.3",
    "eslint-plugin-mocha-only": "^0.0.3",
    "eslint-plugin-node": "^4.2.2",
    "eslint-plugin-promise": "^3.5.0",
    "eslint-plugin-react": "^7.0.1",
    "eslint-plugin-standard": "^3.0.1",
    "flow-bin": "^0.47.0",
    "mocha": "^3.4.1",
    "nodemon": "^1.11.0",
    "nyc": "^10.3.2",
    "request": "^2.81.0",
    "should": "^11.2.1",
    "should-http": "^0.1.1",
    "yarn": "^0.24.5"
  },
  "engines": {
    "node": ">=6"
  }
}
```
