# pdssg - pandoc static site generator

Generate a static site and Atom feeds, with Markdown, shell, and pandoc.

## Requirements

*	sh
*	pandoc

## Installation

Clone pdssg beside your site source directory

```sh
$ git clone https://github.com/torresjrjr/pdssg
$ ls
src  pdssg
```

## Usage

To run pdssg:

```sh
$ ./pdssg/pdssg
```

pdssg is a single executable shell script, with no command-line flags. It simply
generates a neighboring site directory `dst/` from an exiting, neigboring `src/`
directory with the site contents (Markdown files to be converted to HTML, and
other files).

pdssg's design is modular and tree-based. Here's an **example site**.

```
src/
|-- index.md
|-- about.md
|-- posts.md
|-- assets/
|   `--- style.css
|-- posts/
|   |--- 2020-01-01-new-year.md
|   |--- 2020-02-01-corona-what.md
|   `--- 2020-03-01-stuck-at-home.md
|-- feeds/
|   `--- posts.md
`-- _ignore
```

### Webpages and Markdown

[Markdown][MD Wiki] files will be converted to HTML files, ready as webpages.
The exceptions are filepaths matched by patterns in an `./_ignore` file.

  [MD Wiki]: https://en.wikipedia.org/wiki/Markdown

pdssg expects Markdown files to have a [YAML][YAML Wiki] frontmatter block,
which is a block of YAML metadata surrounded by a pair of `---` preceding
everything else.

The frontmatter should at least have a `title` value, which will be used to make
a `<h1>` heading. `author` and `date` values are recommended when appropriate.

  [YAML Wiki]: https://en.wikipedia.org/wiki/YAML

Example of a Markdown file:

```
---
title:  My Webpage Title
author: John Smith
date:   2020-12-30
---

## Markdown contents...
```

### Atom feeds

[Atom][Atom Wiki] feeds are RSS-like feeds based a newer, improved syndication
format. They are essentially used just like RSS and referred to as such.

  [Atom Wiki]: https://en.wikipedia.org/wiki/Atom_(Web_standard)

pdssg can make Atom feeds from directories, with their contained files as feed
entries. To do this, make an "Atom seed file" as such:

1.	Note the path of the Directory.
2.	Prepend `./feeds/` to the path.
3.	Append the `.md` file extension.
4.	Create a Markdown file with this path.
5.	Write a YAML frontmatter to the file.

Refer to the example site above (the `posts/` directory).

The resulting Atom feed will be at the path but with an `.xml` extension.  In
this example, the atom feed will appear at `example.com/feeds/posts.xml`.

**NOTE:** File entries are ordered alphanumerically by their filenames.

---

## Author's notes

This project was born out of a personal challenge, for my own site.  At the
request of a friendly blogger, I cleaned it up and made it public.

Contact me: [t.me/torresjrjr](https://t.me/torresjrjr).

