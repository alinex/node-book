# Conclusion

All tools together used as an development environment will look like:

    .babelrc                # babel configuration
    .eslintrc.js            # eslint setup
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
    "stage-3"
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
