# Publishing

As we are here in the NodeJS world there is not really a choice. The NPM is the only
repository used here. But it can be used using the default `npm` tool or the
alternative `yarn` tool.


## Publish in Git

First if you have a `develop` branche you have to merge it with the master. After this you may set a
tag.

```bash
$ git checkout master
$ git merge develop
$ git tag -a v3.0.1 -m "version 3.0.1 with bug fixes"
```

## Publish to Repository

It is an easy task as already described in the description of the tools.

```bash
$ npm publish
```

While npm published the package using the version from `package.json`, Yarn will
interactively ask for it and update package.json for you.

After the first package was released you can also use a badge on your `README.md` like:

``` markdown
[![npm package](
  https://img.shields.io/npm/v/alinex-rest.svg?maxAge=86400&label=latest%20version)](
  https://www.npmjs.com/package/alinex-rest)
[![latest version](
  https://img.shields.io/npm/l/alinex-rest.svg?maxAge=86400)](#license)
```
