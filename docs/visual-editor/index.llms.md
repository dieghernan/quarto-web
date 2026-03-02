# Visual Editing in RStudio

## Overview

The Quarto visual editor provides a [WYSIWYM](https://en.wikipedia.org/wiki/WYSIWYM) editing interface for all of Pandoc markdown, including tables, citations, cross-references, footnotes, divs/spans, definition lists, attributes, raw HTML/TeX, and more. The visual editor also includes support for executing code cells and viewing their output inline:

![An RMarkdown file opened in the RStudio visual editor. The page is titled 'Filter joins'. Underneath is a table containing R syntax, mathematical notation, and definitions for the semi- and anti-joins. Underneath this table is an R code chunk that displays a graphical representation of a semi-join.](images/visual-editing.png)

The visual editor doesn’t attempt to abstract away or obscure the underlying markdown document. Rather, it aims to provide a highly productive writing interface for people that love markdown. You can also still use most markdown constructs (e.g., \## or **bold**) directly for formatting.

### Switching Modes

Markdown documents can be edited in either source or visual mode. To switch into visual mode for a given document, use the Source or Visual button at the top-left of the document toolbar (or alternatively the keyboard shortcut):

![A snippet of an RStudio window showing the options bar at the top of a Quarto document.](images/visual-editing-switch-modes.png)

Note that you can switch between source and visual mode at any time (editing location and undo/redo state will be preserved when you switch).

## Getting Started

The Quarto visual editor is currently available as a feature of the [RStudio IDE](https://posit.co/download/rstudio-desktop/). The visual editor will eventually also be made available in standalone form.

To get started with the visual editor, download the latest release of RStudio for your platform from:

<https://posit.co/download/rstudio-desktop/>

## Using the Editor

### Keyboard Shortcuts

There are keyboard shortcuts for all basic editing tasks. Visual mode supports both traditional keyboard shortcuts (e.g.  for bold) as well as markdown shortcuts (using markdown syntax directly). For example, enclose `**bold**` text in asterisks or type `##` and press space to create a second level heading. Here are some of the most commonly used shortcuts:

| Command      | Keyboard Shortcut | Markdown Shortcut |
|--------------|:-----------------:|:-----------------:|
| Bold         |                   |    `**bold**`     |
| Italic       |                   |    `*italic*`     |
| Code         |                   |   `` `code` ``    |
| Heading 1    |                   |        `#`        |
| Heading 2    |                   |       `##`        |
| Heading 3    |                   |       `###`       |
| Link         |                   |     `<href>`      |
| R Code Chunk |                   | ```` ```{r} ````  |

See the [editing shortcuts](../../docs/visual-editor/options.llms.md#shortcuts) article for a complete list of all shortcuts.

### Insert Anything

You can also use the catch-all shortcut to insert just about anything. Just execute the shortcut then type what you want to insert. For example:

![There is a line of text (with a cursor at the end) where someone has typed '/lis'. There is a drop-down menu underneath this with options for 'Bullet List', 'Numbered List', and 'Definition List' arranged vertically. The title of each item is bolded, has a small icon to the left, and a small description in lighter gray text underneath it.](images/visual-editing-omni-list.png)

![There is a line of text (with a cursor at the end) where someone has typed '/ma'. There is a drop-down menu underneath this with options for 'Inline Math', 'Display Math', and 'Image...' arranged vertically. The title of each item is bolded, has a small icon to the left, and a small description in lighter gray text underneath it.](images/visual-editing-omni-math.png)

If you are at the beginning of a line (as displayed above), you can also enter plain `/` to invoke the shortcut.

### Editor Toolbar

The editor toolbar includes buttons for the most commonly used formatting commands:

![A snippet of an RStudio window showing the options bar at the top of an RMarkdown document.](images/visual-editing-toolbar.png)

Additional commands are available on the **Format**, **Insert**, and **Table** menus:

| Format | Insert | Table |
|----|----|----|
| ![The contents of the Format drop down menu.](images/visual-editing-format-menu.png) | ![The contents of the Insert drop down menu.](images/visual-editing-insert-menu.png) | ![The contents of the Table drop down menu.](images/visual-editing-table-menu.png) |

## Learning More

Check out the following articles to learn more about visual markdown editing:

- [Technical Writing](../../docs/visual-editor/technical.llms.md) covers features commonly used in scientific and technical writing, including citations, cross-references, footnotes, equations, embedded code, and LaTeX.

- [Content Editing](../../docs/visual-editor/content.llms.md) provides more depth on visual editor support for tables, lists, pandoc attributes, CSS styles, comments, symbols/emojis, etc.

- [Shortcuts & Options](../../docs/visual-editor/options.llms.md) documents the two types of shortcuts you can use with the editor: standard keyboard shortcuts and markdown shortcuts and describes various options for configuring the editor.

- [Markdown Output](../../docs/visual-editor/markdown.llms.md) describes how the visual editor parses and writes markdown and describes various ways you can customize this.
