# All Formats

## Overview

Pandoc supports a huge array of output formats, all of which can be used with Quarto. To use any Pandoc format just use the `format` option or the `--to` command line option.

For example, here’s some YAML that specifies the use of the `html` format as well as a couple of format options:

``` yaml
---
title: "My Document"
format: 
  html:
    toc: true
    code-fold: true
---
```

Alternatively you can specify the use of a format on the command line:

``` bash
quarto render document.qmd --to html
```

See below for a list of all output formats by type along with links to their reference documentation.

## Documents

|  |  |
|----|----|
| [HTML](../../docs/reference/formats/html.llms.md) | HTML is a markup language used for structuring and presenting content on the web. |
| [PDF](../../docs/reference/formats/pdf.llms.md) | PDF is a file format for creating print-ready paged documents. |
| [MS Word](../../docs/reference/formats/docx.llms.md) | MS Word is the word processor included with Microsoft Office. |
| [OpenDocument](../../docs/reference/formats/odt.llms.md) | ODT is an open standard file format for word processing documents. |
| [ePub](../../docs/reference/formats/epub.llms.md) | ePub is an e-book file format that is supported by many e-readers. |

## Presentations

|  |  |
|----|----|
| [Revealjs](../../docs/reference/formats/presentations/revealjs.llms.md) | Revealjs is an open source HTML presentation framework. |
| [PowerPoint](../../docs/reference/formats/presentations/pptx.llms.md) | PowerPoint is the presentation editing software included with Microsoft Office. |
| [Beamer](../../docs/reference/formats/presentations/beamer.llms.md) | Beamer is a LaTeX class for producing presentations and slides. |

## Markdown

|  |  |
|----|----|
| [GitHub](../../docs/reference/formats/markdown/gfm.llms.md) | GitHub Flavored Markdown (GFM) is the dialect of Markdown that is currently supported for user content on GitHub. |
| [CommonMark](../../docs/reference/formats/markdown/commonmark.llms.md) | CommonMark is a strongly defined, highly compatible specification of Markdown. |
| [Hugo](../../docs/output-formats/hugo.llms.md) | Hugo is an open-source static website generator. |
| [Docusaurus](../../docs/output-formats/docusaurus.llms.md) | Docusaurus is an open-source markdown documentation system. |
| [Markua](../../docs/reference/formats/markdown/markua.llms.md) | Markua is a markdown variant used by Leanpub. |

## Wikis

|  |  |
|----|----|
| [MediaWiki](../../docs/reference/formats/wiki/mediawiki.llms.md) | MediaWiki is the native document format of Wikipedia. |
| [DokuWiki](../../docs/reference/formats/wiki/dokuwiki.llms.md) | DokuWiki is a simple to use and highly versatile open source wiki software that doesn’t require a database. |
| [ZimWiki](../../docs/reference/formats/wiki/zimwiki.llms.md) | Zim is a graphical text editor used to maintain a collection of wiki pages. |
| [Jira Wiki](../../docs/reference/formats/wiki/jira.llms.md) | Jira Wiki is the native document format for the Jira issue tracking and project management system from Atlassian. |
| [XWiki](../../docs/reference/formats/wiki/xwiki.llms.md) | XWiki is an open-source enterprise wiki system. |

## More Formats

|  |  |
|----|----|
| [JATS](../../docs/reference/formats/jats.llms.md) | JATS (Journal Article Tag Suite) is an XML format for marking up and exchanging journal content. |
| [Jupyter](../../docs/reference/formats/ipynb.llms.md) | Jupyter Notebooks combine software code, computational output, explanatory text and multimedia resources in a single document. |
| [ConTeXt](../../docs/reference/formats/context.llms.md) | ConTeXt is a system for typesetting documents based on TEX and METAPOST. |
| [RTF](../../docs/reference/formats/rtf.llms.md) | The Rich Text Format (RTF) is a file format for cross-platform document interchange. |
| [reST](../../docs/reference/formats/rst.llms.md) | reStructuredText is an easy-to-read, what-you-see-is-what-you-get plaintext markup syntax and parser system. |
| [AsciiDoc](../../docs/reference/formats/asciidoc.llms.md) | AsciiDoc is a text document format for writing documentation, articles, and books, ebooks, slideshows, web pages, man pages and blogs. |
| [Org-Mode](../../docs/reference/formats/org.llms.md) | Org-Mode is an Emacs major mode for keeping notes, authoring documents, creating computational notebooks, and more. |
| [Muse](../../docs/reference/formats/muse.llms.md) | Emacs Muse is an authoring and publishing environment for Emacs. |
| [GNU Texinfo](../../docs/reference/formats/texinfo.llms.md) | Texinfo is the official documentation format of the GNU project. |
| [Groff Man Page](../../docs/reference/formats/man.llms.md) | The Groff (GNU troff) man page document formats consists of plain text mixed with formatting commands that produce ASCII/UTF8 for display at the terminal. |
| [Groff Manuscript](../../docs/reference/formats/ms.llms.md) | The Groff (GNU troff) manuscript format consists of plain text mixed with formatting commands that produces PostScript, PDF, or HTML. |
| [Haddock markup](../../docs/reference/formats/haddock.llms.md) | Haddock is a tool for automatically generating documentation from annotated Haskell source code. |
| [OPML](../../docs/reference/formats/opml.llms.md) | OPML (Outline Processor Markup Language) is an XML format for outlines. |
| [Textile](../../docs/reference/formats/textile.llms.md) | Textile is a simple text markup language that makes it easy to structure content for blogs, wikis, and documentation. |
| [DocBook](../../docs/reference/formats/docbook.llms.md) | DocBook is an XML schema particularly well suited to books and papers about computer hardware and software. |
| [InDesign](../../docs/reference/formats/icml.llms.md) | ICML is an XML representation of an Adobe InDesign document. |
| [TEI Simple](../../docs/reference/formats/tei.llms.md) | TEI Simple aims to define a new *highly-constrained* and *prescriptive* subset of the Text Encoding Initiative (TEI) Guidelines suited to the representation of early modern and modern books. |
| [FictionBook](../../docs/reference/formats/fb2.llms.md) | FictionBook is an open XML-based e-book format. |
