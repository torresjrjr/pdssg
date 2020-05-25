# pdssg - pandoc static site generator

A shell script which generates a static site and Atom feed from Markdown files
with pandoc.

## Requirements

*	sh
*	pandoc

## Installation

Go to one directory above your website source directory, and `git clone` the
pdssg repo.

```sh
$ pwd
/home/user/website
$ ls
src
$ git clone https://github.com/torresjrjr/pdssg
$ ls
pdssg  src
```

You should now have an executable is a single shell script `./pdssg/pdssg`.

## Usage

pdssg is a single executable shell script, with an optional `config.sh` script,
and no command-line flags. It simply generates a site from an exiting `src/`
directory.

```sh
$ ./pdssg/pdssg
```

pdssg's design is modular. It requires a neighboring `src/` directory with the
site contents (Markdown files to be converted to HTML). Here's an example site.

```
src/
|-- index.md
|-- about.md
|-- archive.md
|-- archive/
|   |--- 2020-01-01-new-year.md
|   |--- 2020-02-01-corona-what.md
|   `--- 2020-03-01-stuck-at-home.md
`-- feed/
    `--- atom.md
```

pdssg expects Markdown files to have a YAML frontmatter block, which is an
initial block of YAML metadata surrounded by a pair of `---`. The frontmatter
should at least have a `title:` value.

```
---
title:  My Webpage Title
author: John Smith
date:   2020-12-30
---

contents...
```

When pdssg is executed, it copies the `src/` directory to `dst/` and converts
all markdown files (ending in `.md`) to HTML, except for files in the
sub-directories `ast` (assets), `pub` (public), and `feed` (atom feed).

## Author's notes

This was originally a farily personal script I made to challange myself, and to
generate my own site. At the request of a friendly blogger, I made it public.

You can contact me at my Telegram: [t.me/torresjrjr](https://t.me/torresjrjr).
I'll more likely respond there.

