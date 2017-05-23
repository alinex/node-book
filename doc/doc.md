# API Documentation

Earlier I used different Tools to create API Documentation out of the code and
it's containing markdown format. But as I optimized it more and more may code
got bloated with them.

Now I decided to put the documentation out of the code into it's own directory
and files. As I had a look for good tools helping me to make it pretty displayable
in the browser I decided to use [GitBook](https://www.gitbook.com).


## GitBook

GitBook is an online platform for writing and hosting documentation using open
source book format and toolchain. It has a big user base and can be integrated
with GitHub and also working nearly as I did before using Markdown syntax.

See all my current books under https://www.gitbook.com/@alinex


## General Usage

Firstly I had to install the GitHub Integrations Plugin within the GitBook options.
Also the GitHub had to be allowed to use for GitBook.

Then I set up the repository by placing a `book.json` in it's root directory. It
should at least contain the definition of the root directory used for the book.
I need this because I store my documentation beside the code in its own directory.

``` javascript
{
  "root": "./doc"
}
```

Then you need the `doc` directory with the following files:

- `doc/README.md`
- `doc/SUMMARY.de`

The `SUMMARY.de` should contain your table of contents as bullet list with
optional headings for chapters. This could look like:

``` markdown
# Summary

- [Introduction](README.md)
- [Alinex Project](alinex.md)

### Standards
- [Quality](quality.md)
- [Documentation](doc.md)
- [File Structure](filestructure.md)
- [Exit Codes](exitcodes.md)

### Modules
- [Alinex](modules.md)
- [3rd Party](3rd-party.md)
```


## eBook Cover

To have a special cover on the PDF, ePub version of the book is done by providing two images:
- `cover.jpg`
- `cover_small.jpg`

A good cover should respect the following guidelines:
- Size of 1800x2360 pixels for `cover.jpg`
- Size of 200x262 pixels for `cover_small.jpg`
- No border
- Clearly visible book title
- Any important text should be visible in the small version


## Writing Documentation

All the pages are written as single files in the `doc` folder using
[Markdown](https://toolchain.gitbook.com/syntax/markdown.html) language. It is nearly
the same as used on GitHub.


## Plugins

### Code Highlighting

In contrast to the already included code display this plugin allows to mark specific
lines in the code like with an textmarker.

The default highlight plugin that is built into GitBook must be disabled, because it prevents other plugins from processing code blocks. Here is an example book.json with the highlight plugin disabled and this code-highlighter plugin enabled.

```json
{
  "plugins": ["-highlight", "code-highlighter"]
}
```

Also you need the following styles setting in `styles/website.css`, `styles/pdf.css` and `styles.ebook.css`:

```css
.code-line-highlight {background-color: #ffff00;}
```

Now you can highlight some code using `&&&` at the start of any line:

```javascript
import restInit from 'alinex-rest/dist/init'
import RestServer from 'alinex-rest/dist/server'

RestServer.init({ ... }) // configure server
&&&RestServer.start()
.then(doSomething)
```

### Mermaid Graphs

Using [Mermaid](https://knsv.github.io/mermaid/) it is possible to include easy
flowcharts without a specific program. It is written as plaintext and converted into
chart on display.

To make this work the following plugin have to be defined:

``` json
{
  "plugins": ["mermaid-gb3"]
}
```

As an example this can look like:

```mermaid
graph TD;
  A-->B;
  A-->C;
  B-->D;
  C-->D;
```

This is done using:

    ``` mermaid
    graph TD;
      A-->B;
      A-->C;
      B-->D;
      C-->D;
    ```
