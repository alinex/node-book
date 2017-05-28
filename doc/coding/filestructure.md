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
    config        # all
    src           # source, development
    doc           # source, development
    test          # source, development
    node_modules  # development, ...
    cover         # development
    dist          # build, ...
    local         # production
```

Read the further sections to get more information of what resides in which
directory and how it is used and created.


## Ignoring Files

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


## Directories

### Source

The source specifies what is stored in the code repository.

This stage contains the following directories:

```coffee
bin           # executable files
config        # default/example configuration
src           # source code
doc           # general documentation as gitbook
test          # test data and test suites
  data        # test data
  mocha       # mocha test suites
```

The source code resides in the `src` folder and will be copied/compiled into
`dist` to run. This step is done on build of package.

### Development

Shows what the developer will find on his machine while developing and testing
the system. While testing the development system will also get all the
directories from productive which are not listed here.

This stage contains the following directories:

```coffee
bin           # executable files
config        # default/example configuration
src           # source code
test          # test data and test suites
doc           # created documentation (optional)
dist          # copied/compiled code
node_modules  # npm installed packages
```

### Installed

This is what you get after a fresh npm installation.

This stage contains the following directories:

```coffee
bin           # executable files
config        # default/example configuration
dist          # copied/compiled code
  config      # compiled configurations
node_modules  # npm installed packages
local         # data and code which maybe changed in installation
  config      # compiled configuration
```

### Productive

And finally this shows what resides on the productive server.

This stage contains the following directories:

```coffee
bin           # executable files
config        # configuration
dist          # copied/compiled code
  config      # compiled configurations
node_modules  # npm installed packages
local         # data and code which maybe changed in installation
  config      # compiled configuration
  log         # log files
  data        # persistent file store
```


## Where belongs what?

The following list should give an overview of there to store what:

- cache files -> systems temp folder
- configuration -> system or user `alinex` folder or `config`
- resources for binaries -> `bin/lib`
- temporary files -> systems temp folder
