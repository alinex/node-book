# Dependencies

To make the code manageable and good structured it will be split up in lots of
own and third party modules. This makes it not an easy task to check that everything
is up to date.


## Monitoring

Therefore I use [gemnasium](https://gemnasium.com/dashboard) which is free and works
great with GitHub. You login with your github account and are Guided through the setup
to register the webhooks and allow the access to your repositories.

Gemnasium will be informed of code changes and updates its dependency information
automatically. It will inform about new modules which are or are not covered within
your package dependency configuration in an email.

You can also use a badge on your `README.md` like:

``` markdown
[![Gemnasium status](
  https://img.shields.io/gemnasium/alinex/node-rest.svg?maxAge=86400)](
  https://gemnasium.com/alinex/node-rest)
```

## Checking on Console

To check or upgrade the dependencies on console the `yarn` tool has a lot of goodies.
This is only possible if the package is also installed using `yarn install` (if
not, call it now).

``` bash
$ yarn outdated
yarn outdated v0.24.4
Package              Current  Wanted   Latest   Package Type    URL
express-oauth-server 2.0.0-b1 2.0.0-b3 2.0.0-b1 dependencies       
mongoose             4.10.1   4.10.2   4.10.2   dependencies       
yarn                 0.24.4   0.24.5   0.24.4   devDependencies    
```

This shows you a table of all packages there an upgrade is possible. You can now install
the ones defined as wanted using `yarn upgrade`.

Or call the whole process as an interactive tool using:

``` bash
yarn upgrade-interactive v0.24.4
? Choose which packages to update. (Press <space> to select, <a> to toggle all, <i> to inverse selection)
 dependencies
❯◯ express-oauth-server  2.0.0-b1  ❯  2.0.0-b1.  
 ◯ mongoose              4.10.1    ❯  4.10.2    

 devDependencies
 ◯ yarn                  0.24.4    ❯  0.24.4    
```

Here you can select the packages to upgrade and process.
