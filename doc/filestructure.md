# File Structure

All modules in the Alinex namespace will use the same directory structure.
This follows the general standards and is described here.

Read more on the following pages:


## Overview

The locally installed system may be in one of the following states which
presents the development cycle of the system:

1. **Source** - the real code base
2. **Development** - after installing
3. **Build** - if installed from npm or after building
4. **Productive** - after the system is configured

Each of these states may have some of the possible directories so they will
be referenced in the further description.

**Source**

> The developer will start with the GIT source by cloning or forking.

**Development**

> While in development additional directories will be created while compiling and
> testing the code.

**Build**

> For productive use, this is the start point. You get a ready to run compiled
> system.

**Productive**

> In the first run the system may be configured and create some additional
> directories for configs and runtime data.


## Possible directories

The following list displays all directories of any state which may exist each
listed with the states to which it belongs:

``` coffee
    .             # source
    bin           # all
    dist          # build, ...
    doc           # source, development
    node_modules  # development, ...
    src           # source, development
    test          # source, development
    local         # development, ...
```

Read the further sections to get more information of what resides in which
directory and how it is used and created.


## Ignorance

To properly support the file structure in all phases two ignore files are needed:

__.gitignore__ (used to not push everything to git)

``` coffee
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

__.npmignore__ (used fro npm publishing)

``` coffee
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


## Source

The source specifies what is stored in the code repository.

This stage contains the following directories:

``` coffee
bin           # executable files
src           # source code
  doc         # general documentation which won't belong to any specific file
  man         # sources for man pages
test          # test data and test suites
  data        # test data
  mocha       # mocha test suites
var           # data and code which maybe changed in installation
  example     # examples
  src         # original data, will be overridden on update
```

The source code resides in the `src` folder and will be copied/compiled into
`lib` to run. This step is done on prepublication of package.


Development
-------------------------------------------------

Shows what the developer will find on his machine while developing and testing
the system. While testing the development system will also get all the
directories from productive which are not listed here.

This stage contains the following directories:

``` text
bin           // executable files
doc           // created documentation (optional)
lib           // copied/compiled code
man           // created man pages
node_modules  // npm installed packages
report        // development
src           // source code
test          // test data and test suites
var           // data and code which maybe changed in installation
  example     // examples
  src         // original data, will be overridden on update
```


Installed
-------------------------------------------------

This is what you get after a fresh npm installation.

This stage contains the following directories:

``` text
bin           // executable files
lib           // copied/compiled code
man           // created man pages
node_modules  // npm installed packages
var           // data and code which maybe changed in installation
  example     // examples
  local       // specific settings for this installation
  src         // original data, will be overridden on update
```


Productive
-------------------------------------------------

And finally this shows what resides on the productive server.

This stage contains the following directories:

``` text
bin           // executable files
lib           // copied/compiled code
man           // created man pages
node_modules  // npm installed packages
var           // data and code which maybe changed in installation
  example     // examples
  data        // persistent data stores (if needed)
  lib         // linked or compiled from src/local (on system start)
  local       // customized settings for this installation
  log         // log files
  src         // base settings, will be updated with package
```

VAR Data
-------------------------------------------------
The var folder contains everything that may be changed for the individual
installations.

It contains different sub folders:

- `example` - examples to be used as template for own configuration
- `src` - the source files which will change with each update
- `local` - local maybe changed files
- `lib` - linked or compiled files from source overridden by local

Within these directories you will find the following possible structure:

``` text
config        // configuration
htdocs        // for webserver
  <theme>     // or use 'default'
locale        // localization
script        // user scripts
template      // templates
```

Templates and statics will be compiled from `local` or `src` to `lib`. This is done:

- on server start the maybe changed ones
- on file change the maybe changed ones
- after software update all

Therefore dependency have to be held (`.dependency.map`). To know which one is
made from which.

In the productive system the settings and data locations may vary. Therefore
the system will look in the following places and the later has the higher precedence:

__Source__

    config: <app>/var/src/config/
    locale: <app>/var/src/locale/
    data:   <app>/var/src/data/

__Local__

    config: <app>/var/local/config/
    data:   <app>/var/local/data/

__Global__

    config: /etc/<app>/config/
    data:   /etc/<app>/data/

__User__

    config: ~/.<app>/config/
    data:   ~/.<app>/data/

You may also use softlinks for `var/local` or within it to move your files to
any other position on your filesystem.

On server start these files will be copied or linked into the var/lib/data
folder. If they are newer than the files there. And the files will be removed
if no longer existent.

This enables the user to upgrade the base system without losing the own changes.




Where belongs what?
-------------------------------------------------
The following list should give an overview of there to store what:

- cache files -> systems temp folder
- configuration -> `/var/.../config`
- language packs -> `/var/.../locale`
- resources for binaries -> `/bin/lib`
- webserver statics -> `/var/.../www/default/`
- temporary files -> systems temp folder
