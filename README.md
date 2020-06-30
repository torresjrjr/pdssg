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
|-- index.md
|-- about.md
|-- posts.md
|-- posts/
|   |--- 2020-01-01-new-year.md
|   |--- 2020-02-01-corona-what.md
|   `--- 2020-03-01-stuck-at-home.md
|-- feeds/
|   `--- posts.md
|-- assets/
|   `--- style.css
|-- _includes/
|   |--- header.html
|   |--- footer.html
|   `--- meta.html
`-- _templates/
    |--- atom.xml
    `--- main.html
```

Here's the resulting build directory.

```
dst/
|-- index.md
|-- about.md
|-- posts.md
|-- posts/
|   |--- 2020-01-01-new-year.md
|   |--- 2020-02-01-corona-what.md
|   `--- 2020-03-01-stuck-at-home.md
|-- feeds/
|   `--- posts.md
`-- assets/
    `--- style.css
```

Note: files and directories beginning with an underscore `_` will not be added.


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


### Atom feeds

[Atom][Atom] feeds are RSS-like feeds based on a newer, more-robust syndication
format. They are essentially used just like [RSS][RSS] and referred to as such.
Atom feeds allow readers to subscribe to a website's new content, like a blog.

  [Atom]: https://en.wikipedia.org/wiki/Atom_(Web_standard)
  [RSS]: https://en.wikipedia.org/wiki/RSS

pdssg can make Atom feeds from directories, with the directory's files as feed
entries. To do this, make an "Atom seed file" as such:

1.	Note the path of the directory.
2.	Prepend `./feeds/` to the path.
3.	Append the `.md` file extension to the path.
4.	Create a Markdown file with the path.
5.	Write a YAML frontmatter to the file.

Refer to the **example site** above for demonstration (the `posts/` directory).

The Atom seed file will be converted to an Atom feed file. This resulting feed
will exist at the new path but with an `.xml` extension. In this example, the
atom feed will appear at `example.com/feeds/posts.xml`. Note, the `post.md` file
is not necessary for a feed, only a directory.

**NOTE:** Atom entries are ordered alphanumerically by their corresponding
filenames, not by their `date` specified by their YAML frontmatter.

---

## Author's notes

This project was born out of a personal challenge, for my own site. At the
request of a friendly blogger, I cleaned it up and made it public.

Contact me: [t.me/torresjrjr](https://t.me/torresjrjr)

