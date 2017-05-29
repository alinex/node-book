# Debug Output

While working in different stages like development or even production it may be
useful to switch on and off debug statements on demand.

This is done through a tiny NodeJS `debug` utility modelled after node core´s
debugging technique. It can be enabled through environment settings and will printout
some predefined messages. Another small helper called `chalk` to make the output
messages color full.

A lot of foreign libraries are also using debug so it will work on their code also.


## Installation

Because this should also stay in the productive code

```bash
# install using yarn
yarn add debug chalk
# and alternatively using npm
npm install debug chalk --save
```


## Usage

Simply create a `debug` instance by giving it the name of your module and maybe
the subroutine as concatenated function. Using it´s `debug` method will return a
decorated version of the given message to `console.error` only if debug is enabled.

```js
import Debug from 'debug'

// initialize debug with module name and maybe sub element
const debug = Debug('<module>')('<sub>')

debug('new instance created using %o', setup)
```

You may also make the output colorful by also adding the earlier mentioned `chalk`
module:

```js
import Debug from 'debug'
import chalk from 'chalk'

// initialize debug with module name and maybe sub element
const debug = Debug('<module>')('<sub>')

debug(chalk.red('new instance created using %o'), setup)
```

__Code to run only if enabled__

```js
if (debug.enabled) {
  debug(claculateMessage())
}
```

This allows to only run the message calculation if debugging is enabled for this
module.

__Formatters__

Debug uses printf-style formatting supporting the following formatters:

| Formatter | Representation |
| --------- | -------------- |
| `%O` | Pretty-print an Object on multiple lines. |
| `%o` | Pretty-print an Object all on a single line. |
| `%s` | String. |
| `%d` | Number (both integer and float). |
| `%j` | JSON. Replaced with the string '[Circular]' if the argument contains circular references. |
| `%%` | Single percent sign ('%'). This does not consume an argument. |


__Debug names__

The convention is to use the short name of the module as debug name like `config` for
the `alinex-config` module. The sub names are often used after their file names which
implies the functional part like `config:compile` for the compiler class in `compile.js`.

Also within the tests you may use `test` as debug module name.


## Colors

The `debug` module already uses colors if possible for the namespace identifier. It
will try to pick a different color for each namespace to make it easier to overflow
a bigger output. But like described above you may use `chalk` yourself to make the
message itself also colorful. Possible colors are:

- `red`, `bold.red`
- `green`, `bold.green`
- `yellow`, `bold.yellow`
- `blue`, `bold.blue`
- `magenta`, `bold.magenta`
- `cyan`, `bold.cyan`
- `white`, `bold.white`
- `gray`, `bold.gray`
- `black`, `bold.black`

The `bold` versions resemble the color more. But you may also combine this with
`dim`, `italic`, `underline`, `inverse`, `strikethrough` and also set `bgRed`...


## Control debugging

When running the code, you can set a few environment variables that will change
the behavior of the debug logging:

| Name  | Purpose |
| ------| ------- |
| `DEBUG` | Enables/disables specific debugging namespaces. |
| `DEBUG_COLORS` | Whether or not to use colors in the debug output. |
| `DEBUG_DEPTH` | Object inspection depth. |
| `DEBUG_SHOW_HIDDEN` | Shows hidden properties on inspected objects. |

For the `DEBUG` variable, you can give multiple comma separated namespaces using
colon as delimiter between the namespace levels. An `*` character is also possible
to select multiple or all:

| DEBUG | Usage   |
| ------| ------- |
| `DEBUG=*` | Show all messages. |
| `DEBUG=test*` | Show additional messages from the test suite. |
| `DEBUG=config,config:compile` | Show only the main and compile messages from the config module. |
| `DEBUG=config*,file*` | Show all config and file module messages. |
