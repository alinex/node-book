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


## Usage

Firstly I had to install the GitHub Integrations Plugin within the GitBook options.
Also the GitHub had to be allowed to use for GitBook.

Then I set up the repository by placing a `book.json` in it's root directory.

``` javascript
{
  "root": "./doc",
  "title": "Alinex NodeJS Modules",
  "description": "This is a book explaining all the major parts and development background around the Alinex namespaced modules.",
  "author": "Alexander Schilling",
  "language": "en"
}
```

Then you need the `doc` directory with the following files:

- `doc/README.md`
- `doc/SUMMARY.de`

The `SUMMARY.de` should contain your table of contents as bullet list with
optional headings for chapters.
