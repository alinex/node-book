# Alinex NodeJS Modules

This is a book explaining all the major parts and development background around
the Alinex namespaced modules. But it is not completely specific but mostly a book
about NodeJS development with best practice from the Alinex modules.

The decisions from this book are not real hard facts but a definition to follow as
possible. It may change as the world around changes. And you don't have to
follow this standards but it helps for all which are working deeply with the Alinex
modules and participating to it to understand the parts behind.

Some of the Alinex modules use an older standard (CoffeeScript based) but will
eventually be upgraded to this.

Keep in mind that the book explains a lot of technologies around NodeJS and web
development but it is neither meant as a guide to teach the technologies more like
a best practice and how to bring it all together.


## Why this book

This is a living book, it is not only written to teach others but also to keep
the knowledge as a reference for myself. Also it is not statically written but a
type of living book which evolve and grow in time hopefully as fast as technology
goes on. So read it once, but come back again to see the newest changes.

The key concepts are "Configuration over Implementation" and "Keep it Simple".

All the different modules in the Alinex namespace are loose coupled but optimal
integrated. At first they solve my own problems but I will enlarge their functionality
and often my problems are the problems of others, too.


## Structure of Book

I believe in open source and all the tools which are mentioned here are free for
open source projects.But you may also use them for private use with some costs.

__Introduction__

Contains this basic information and some words about Alinex and why and how.

__Development Environment__

And at last some documentation on how to make the development environment work
seamlessly with lots of goodies.

__Coding__

Lots of opinionated decisions on how to build the software.

__Modules__

You will find a [list of modules](modules.md) which are notable within this documentation.
And also some more third party modules with short descriptions.

__Snippets / examples__

This section will collect different code examples with short explanations to show
how to do some specific tasks.


## Requirements

As far as possible Alinex tries to not be restricted by a specific system or service
but to come to an end it focuses on specific systems and services.

__Linux OS:__ At first this documentation is based on debian Linux examples but it
will work on any other linux system or mac with some minor changes. You may also
work with windows by replacing the few OS specific calls with appropriate ones.

All the environment tools used here may also be replaced by other ones for their
work.

And at last the most important thing the modules are mostly not OS specific and
will run on any system.
