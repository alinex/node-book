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

With npm you have to use the additional package [nvm-check](https://github.com/dylang/npm-check/blob/master/README.md). After you have
installed this globally or within your project. You may call it using `npm-check -u`
this will show an interactive selection to upgrade.

![npm-check](npm-check.png)

You may select the updates you want to have and hit enter to upgrade them.

To check or upgrade the dependencies on console using the `yarn` tool this is integrated.
This is only possible if the package is also installed using `yarn install` (if
not, call it first).

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


## Gemnasium

[Gemnasium](https://gemnasium.com/dashboard) will analyze the repositories after
linked from GitHub and check for the dependent modules regularly. It will alert
with an email if new versions are released often with changes.

Ann online overview will look like:

![Gemnasium Overview](dependency-gemnasium.png)
