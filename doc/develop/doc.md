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


## eBook Setup

To have a special cover on the PDF, ePub version of the book is done by providing two images:
- `cover.jpg`
- `cover_small.jpg`

A good cover should respect the following guidelines:
- Size of 1800x2360 pixels for `cover.jpg`
- Size of 200x262 pixels for `cover_small.jpg`
- No border
- Clearly visible book title
- Any important text should be visible in the small version

And to set the layout you may use:

```json
{
  "pdf": {
    "pageNumbers": true,
    "headerTemplate": " ",
    "footerTemplate": " "
  }
}
```

## Writing Documentation

All the pages are written as single files in the `doc` folder using
[Markdown](https://toolchain.gitbook.com/syntax/markdown.html) language. It is nearly
the same as used on GitHub.

__Attention:__ In contrast to the other markdown parsers there should be no space between
the code tag and the language.


## Plugins

### Layout

To improve the layout of the book I use three different plugins:

```json
{
  "plugins": ["toggle-chapters", "navigator", "downloadpdf"]
}
```

This will open/close chapters like folders, display a page navigation on the
right side and a link to download as PDF on the top line.

To optimize the navigator output set the following in `styles/ebook.css` and
`styles/pdf.css` to disable navigator:

```css
#anchors-navbar, #goTop {display: none}
```

And for `styles/website.css` add this to optimize display and remove for small
display:

```css
#anchors-navbar {color: darkgray; right: 28px; top: 45px}
#goTop {display: none}
@media (max-width: 660px) {
  #anchors-navbar {display: none}
}
```

### ToDo

As already used in GitHub markdown this plugin allows to write ToDo lists with
check boxes which may be checked:

```json
{
  "plugins": ["todo"]
}
```

Now you may create a checklist using:

- [ ] Mercury
- [x] Venus
- [x] Earth (Orbit/Moon)
- [x] Mars
- [ ] Jupiter
- [ ] Saturn
- [ ] Uranus
- [ ] Neptune
- [ ] Comet Haley

This is done using:

    - [ ] Mercury
    - [x] Venus
    - [x] Earth (Orbit/Moon)
    - [x] Mars
    - [ ] Jupiter
    - [ ] Saturn
    - [ ] Uranus
    - [ ] Neptune
    - [ ] Comet Haley


### Mermaid Graphs

Using [Mermaid](https://knsv.github.io/mermaid/) it is possible to include easy
flowcharts without a specific program. It is written as plaintext and converted into
chart on display.

To make this work the following plugin have to be defined:

```json
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

    ```mermaid
    graph TD;
      A-->B;
      A-->C;
      B-->D;
      C-->D;
    ```

### PlantUML

[PlantUML](http://plantuml.com/) is another format to make graphs out of text descriptions like mermaid.

The plugin is loaded using:

```json
{
  "plugins": ["puml"]
}
```

And the diagram may look like:

{% plantuml %}
Bob->Alice : hello
{% endplantuml %}

It is written using:

    {% plantuml %}
    Bob->Alice : hello
    {% endplantuml %}


## Final Setup

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
    "-highlight", "code-highlighter",
    "toggle-chapters", "navigator", "downloadpdf"
  ],
  "pluginsConfig": {
    "downloadpdf": {
      "base": "https://www.gitbook.com/download/pdf/book/alinex/nodejs",
      "label": "Download PDF",
      "multilingual": false
    }
  }
}
```

__Further files__

```coffee
doc/README.md           # Introduction
doc/SUMMARY.md          # Page index of book
doc/cover.jpg           # eBook cover
doc/cover_small.jpg     # small cover
doc/styles/ebook.css    # user style
doc/styles/pdf.css      # user style
doc/styles/website.css  # user style
```
