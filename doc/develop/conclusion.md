# Conclusion

The basic settings used for my new modules are:

| Software     | Comment |
| ------------ | ------- |
| Node >= 6    | Allows to use ES6 |
| TypeScript   | Type safe superset to ES6 |
| Mocha        | To run unit tests |

| Alternative  | Comment |
| ------------ | ------- |
| Babel        | Transpiler used for functionality up to stage-3 |
| Flow         | For type checking |


## Initial file structure

All tools together used as an development environment will look like:

    # for TypeScript
    tsconfig.json           # TS compilation settings
    tslint.json             # TS linting settings
    # for ES.Next
    .babelrc                # babel configuration
    .eslintrc.js            # eslint setup
    .flowconfig             # for typechecking setup
    # repository
    .git                    # git store
    .gitignore              # files to not add to git
    .npmignore              # files to not publish
    .travis.yml             # vm setup for travis
    # documentation
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
    # content
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

__tslint.json__

```json
{
  "defaultSeverity": "warning",
  "extends": [
      "tslint:recommended"
  ],
  "rules": {
    "max-line-length": {
        "options": [120]
    },
    "no-console": [true, "log", "warning"],
    "semicolon": [true, "never"]
  },
  "jsRules": {
    "max-line-length": {
        "options": [120]
    }
  },
  "rulesDirectory": []
}
```

__tsconfig.json__

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "declaration": true,
    "sourceMap": true,
    "removeComments": true,
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  },
  "files": [
    "./node_modules/@types/mocha/index.d.ts",
    "./node_modules/@types/node/index.d.ts"
  ],
  "include": [
    "src/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```

__.babelrc__

```json
{
  "presets": [
    ["env", { "targets": { "node": 6 } }],
    "stage-3",
    "flow"
  ],
  "plugins": ["dynamic-import-node"],
  "comments": false
}
```

__.eslintrc.js__

```js
module.exports = {
  env: { es6: true, node: true },
  extends: 'airbnb',
  plugins: ["flowtype"],
  parser: "babel-eslint",
  parserOptions: { sourceType: 'module' },
  rules: {
    'max-len': [ 'warn', 120 ],
    'indent': [ 'error', 2 ],
    'linebreak-style': [ 'error', 'unix' ],
    'quotes': [ 'error', 'single' ],
    'semi': [ 'warn', 'never' ],
    'spaced-comment': 'warn',
    'no-unused-vars': [ 'warn' ],
    'no-console': [ process.env.NODE_ENV === 'production' ? 'error' : 'warn' ],
    'no-shadow': ['error', { 'allow': ['cb', 'err'] }],
    'import/prefer-default-export': 'warn',
    'no-underscore-dangle': 'off',
    'no-restricted-syntax': 'off',
    'no-multi-str': 'off',
    'no-param-reassign': 'off',
    'prefer-destructuring': 'off'
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
tsconfig.json

# Other caching like eslint or repl
tslint.json
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
#  - "6"  # LTS   from 2016-10 maintenance till 2019-04
#  - "7"  # devel from 2016-10
  - "8"  # LTS   from 2017-10 maintenance till 2019-12
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
      "base": "https://www.gitbook.com/download/pdf/book/alinex/rest",
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
    "lint": "tslint -c tslint.json 'src/**/*.ts'",
    "test": "mocha -r ts-node/register test/mocha/**.ts",
    "coverage": "nyc mocha",
    "dev": "NODE_ENV=development nodemon --exec ./node_modules/.bin/ts-node -- ./src/index.ts",
    "build": "tsc",
    "start": "node dist/index"
  },
  "nyc": {
    "extension": [
      ".ts",
      ".tsx"
    ],
    "exclude": [
      "**/*.d.ts"
    ],
    "reporter": [
      "lcov",
      "text-summary"
    ],
    "cache": true,
    "all": true
  },
  "directories": {
    "lib": "./dist"
  },
  "dependencies": {
    "chalk": "^1.1.3",
    "debug": "^2.6.3"
  },
  "devDependencies": {
    "@types/mocha": "^2.2.43",
    "@types/node": "^8.0.37",
    "@types/chai": "^4.0.4",
    "@types/chai-as-promised": "^7.1.0",
    "@types/chai-http": "^3.0.3",
    "async": "^2.5.0",
    "chai": "^4.1.2",
    "chai-as-promised": "^7.1.1",
    "chai-http": "^3.0.0",
    "codacy-coverage": "^2.0.3",
    "coveralls": "^3.0.0",
    "marked-man": "^0.2.1",
    "mocha": "^4.0.1",
    "nodemon": "^1.12.1",
    "nyc": "^11.2.1",
    "ts-node": "^3.3.0",
    "tslint": "^5.7.0",
    "typescript": "^2.5.3",
    "typescript-eslint-parser": "^8.0.0"
  },
  "engines": {
    "node": ">=6"
  }
}
```
