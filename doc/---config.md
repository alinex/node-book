# Config Structure

Most modules support extensive configurations without code change. This is done
using the [config](http://alinex.github.io/node-config) package. Which will read
different configuration formats from file sources, validates and optimizes the values.
So it is often also possible to use natural language for definition.


File Search
==========================================================

The base for storing configuration settings often is a file structure. The alinex
modules supports them with different file formats (also mixed) and multiple search
paths.

In an application you may put your configuration files in:

1. `/etc/alinex` - used by all alinex-config based applications
1. `~/.alinex` - same in the user home directory
2. `<installdir>/var/local/config` - specific settings only for one application
2. `/etc/<appname>` - same in the global directory
2. `~/.<appname>` - same in the user home directory

Config
-----------------------------------------------------------
If existing files of all of them are red and the later overwrites the earlier ones
values. So what you get is a combination out of all of them and the last setting
for the same path is used.

This means that you don't have to write complete config files but only make some
update changes in later directories.

Other files
-----------------------------------------------------------
