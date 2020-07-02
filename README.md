# pdssg - pandoc static site generator

Generate a static site and Atom feeds, with Markdown, shell, and pandoc.


## Requirements

*	sh
*	pandoc


## Installation

git clone pdssg, ideally beside your site source directory.

```sh
git clone https://github.com/torresjrjr/pdssg
```


## Usage

To run pdssg and build a static site, execute the pdssg script in one directory
above the site source directory.

```sh
$ ls
src/  pdssg/
$ ./pdssg/pdssg
```

pdssg is a single executable shell script, with no command-line flags. It simply
generates a neighboring site directory `dst/` (destination) from an existing,
neigboring directory `src/` (source) with the site's contents (Markdown files to
be converted to HTML webpages, and other files).

pdssg's design is modular and tree-based. Here's an **example site** source
directory.

```
src/
|-- _ignore
|-- _feeds
|-- index.md
|-- about.md
|-- posts.md
|-- posts/
|   |-- _drafts/
|   |   `--- 2020-04-01-bored.md
|   |-- 2020-01-01-new-year.md
|   |-- 2020-02-01-corona-what.md
|   `-- 2020-03-01-stuck-at-home.md
|-- feeds/
|   `-- posts.md
|-- assets/
|   `-- style.css
|-- _templates/
|   |-- atom.xml
|   `-- main.html
`-- _includes/
    |-- header.html
    |-- footer.html
    `-- meta.html
```

Here's the resulting build directory.

```
dst/
|-- index.html
|-- about.html
|-- posts.html
|-- posts/
|   |--- 2020-01-01-new-year.html
|   |--- 2020-02-01-corona-what.html
|   `--- 2020-03-01-stuck-at-home.html
|-- feeds/
|   `--- posts.html
`-- assets/
    `--- style.css
```

Note: files and directories beginning with an underscore `_` will be discarded.


### Webpages and Markdown

[Markdown][Markdown] files will be converted to HTML files, ready as webpages.
The exceptions are filepaths matched by patterns in an `./_ignore` file, like a
`.gitignore` file.

  [Markdown]: https://en.wikipedia.org/wiki/Markdown

pdssg expects Markdown files to have a [YAML][YAML] frontmatter block, which is
a block of YAML metadata surrounded by a pair of `---`, preceding the rest of
the file contents.

The frontmatter _should_ at least have a `title` value, which will be used to make
a `<h1>` title heading. `author` and `date` values are common, and recommended
where appropriate.

  [YAML]: https://en.wikipedia.org/wiki/YAML

Example of a Markdown file:

```markdown
---
title:  My Webpage Title
author: John Smith
date:   2020-12-30
---

## Subheading

contents...
```

### Templates and Includes

As in the example, the `_includes` and `_templates` directories will be used to
generate the HTML and Atom files. They are then discarded.

For the files in `_templates`:

*	`atom.xml`  is used to make HTML documents.
*	`main.html` is used to make Atom feeds.

For the files in `_includes`:

*	`meta.html`   is inserted in the document header within the `<meta>` tags.
*	`header.html` is inserted in the body within the `<body>` tags, before
	the main content.
*	`footer.html` is inserted in the body within the `<body>` tags, after
	the main content.


### Atom feeds

[Atom][Atom] feeds are RSS-like feeds based on a newer, more-robust syndication
format. They are essentially used just like [RSS][RSS] and referred to as such.
Atom feeds allow readers to subscribe to a website's new content, like a blog.

  [Atom]: https://en.wikipedia.org/wiki/Atom_(Web_standard)
  [RSS]: https://en.wikipedia.org/wiki/RSS

pdssg can make Atom feeds from directories, with the directory's files as feed
entries. To do this, you need to make a specified directory for your feeds, and
make an "Atom seed file" as such:

1.	Create a feeds directory (e.g. `./feeds/`) and write it's path in the config
	file `_feeds`
2.	Note the path of a directory you want to make a feed (e.g. `./posts/`).
3.	Prepend your feeds directory path to it (e.g. `./feeds/posts/`).
4.	Append the `.md` file extension to the path (e.g. `./feeds/posts.md`).
5.	Create a Markdown file with this path. This is the Atom seed file.
6.	Write a YAML frontmatter to the file.

Refer to the **example site** above for demonstration (the `posts/` directory).

The Atom seed file will be converted to an Atom feed file. This resulting feed
will exist at the new path but with an `.xml` extension instead of `.md`. In
this example, the atom feed will appear at `example.com/feeds/posts.xml`. Note,
the `./posts.md` file is not necessary for a feed, only a directory.

**NOTE:** Atom entries are ordered alphanumerically by their corresponding
filenames, not by their `date` specified by their YAML frontmatter.

---

## Author's notes

This project was born out of a personal challenge, for my own site. At the
request of a friendly blogger, I cleaned it up and made it public.

Contact me: [t.me/torresjrjr](https://t.me/torresjrjr)

