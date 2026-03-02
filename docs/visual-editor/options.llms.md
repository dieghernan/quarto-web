# Shortcuts & Options

## Shortcuts

Visual mode supports both traditional keyboard shortcuts (e.g.  for bold) as well as markdown shortcuts (using markdown syntax directly). For example, enclose `**bold**` text in asterisks or type `##` and press space to create a second level heading.

Here are the available keyboard and markdown shortcuts:

| Command             |   Keyboard Shortcut    |  Markdown Shortcut   |
|---------------------|:----------------------:|:--------------------:|
| Bold                |                        |      `**bold**`      |
| Italic              |                        |      `*italic*`      |
| Code                |                        |     `` `code` ``     |
| Strikeout           |                        |     `~~strike~~`     |
| Subscript           |                        |       `~sub~`        |
| Superscript         |                        |      `^super^`       |
| Heading 1           |                        |         `#`          |
| Heading 2           |                        |         `##`         |
| Heading 3           |                        |        `###`         |
| Heading Attributes  |                        |    `{#id .class}`    |
| Link                |                        |       `<href>`       |
| Blockquote          |                        |         `>`          |
| Code Block          |                        |    ```` ``` ````     |
| R Code Chunk        |                        |   ```` ```{r} ````   |
| Raw Block           |                        | ```` ```{=html} ```` |
| Div                 |                        |        `:::`         |
| Bullet List         |                        |         `-`          |
| Ordered List        |                        |         `1.`         |
| Tight List          |                        |                      |
| List Check          |                        |        `[x]`         |
| Emoji               |                        |      `:smile:`       |
| Definition          |                        |         `:`          |
| Non-Breaking Space  |  Ctrl-SpaceCtrl-Space  |                      |
| Hard Line Break     | Shift-EnterShift-Enter |                      |
| Paragraph           |                        |                      |
| Image               |                        |                      |
| Footnote            |                        |                      |
| Citation            |                        |         `[@`         |
| Table               |                        |                      |
| Editing Comment     |                        |                      |
| Select All          |                        |                      |
| Clear Formatting    |                        |                      |
| Edit Attributes     |          F4F4          |                      |
| Run Code Chunk      |                        |                      |
| Run Previous Chunks |                        |                      |

> **TIP:**
>
> For markdown shortcuts, if you didn’t intend to use a shortcut and want to reverse its effect, just press the backspace key.

## Insert Anything

You can also use the catch-all shortcut to insert just about anything. Just execute the shortcut then type what you want to insert. For example:

![There is a line of text (with a cursor at the end) where someone has typed '/lis'. There is a drop-down menu underneath this with options for 'Bullet List', 'Numbered List', and 'Definition List' arranged vertically. The title of each item is bolded, has a small icon to the left, and a small description in lighter gray text underneath it.](images/visual-editing-omni-list.png)

![There is a line of text (with a cursor at the end) where someone has typed '/ma'. There is a drop-down menu underneath this with options for 'Inline Math', 'Display Math', and 'Image...' arranged vertically. The title of each item is bolded, has a small icon to the left, and a small description in lighter gray text underneath it.](images/visual-editing-omni-math.png)

If you are at the beginning of a line (as displayed above) you can also enter plain `/` to invoke the shortcut.

## Global Options

You can customize visual editing options within **R Markdown -\> Visual** (note that the visual editor was originally created for use with R Markdown so its options are located there — these options are also applicable to usage with Quarto):

![](images/visual-editing-options.png)

| Option | Description |
|----|----|
| Use visual editing by default | Switch to visual mode immediately when creating new documents. |
| Show document outline by default | Show the navigational outline when opening documents in visual mode. |
| Editor content width | Maximum width for editing content. This is intended to keep editing similar to the width that users will see. |
| Editor font size | Base font size for editor content (default: inherit from IDE settings). |
| Show margin column indicator in code blocks | Show vertical line that indicates location of editing margin column (e.g. 80). |
| Default spacing between list items | Whether to use tight or normal spacing between list items by default. See [Tight Lists](../../docs/visual-editor/content.llms.md#tight-lists) for details. |
| Automatic text wrapping (line breaks) | When writing markdown, automatically insert line breaks after sentences or at a specified column (default: flow text; no auto-wrapping). See [Line Wrapping](../../docs/visual-editor/markdown.llms.md#line-wrapping) for details. |
| Write references at end of current | Write references (footnotes) at the end of the block or section where they appear, or at the end of the document. See [References](../../docs/visual-editor/markdown.llms.md#references) for details. |
| Write canonical visual mode markdown in source mode | Use the visual mode markdown writer when saving markdown from source mode (ensure consistency between documents saved from either mode). |

## Citation Options

You can customize visual editor citation options within **R Markdown -\> Citations**:

![](images/visual-editing-options-citations.png)

| Option | Description |
|----|----|
| Zotero Library | Location of [Zotero](../../docs/visual-editor/technical.llms.md#citations-from-zotero) citation library (Local or Web). |
| Zotero Data Directory | Location of Zotero local data directory. |
| Use libraries | Zotero libraries to use as reference sources. |
| Use Better BibTeX for citation keys and BibTeX export. | Optionally use [Better BibTeX](https://retorque.re/zotero-better-bibtex/) to generate citation keys and export BibTeX from Zotero (this option appears only if Better BibTeX is installed). |

## Project Options

Global options that affect the way markdown is written can also be customized on a per-project basis. You can do this using the **R Markdown** pane of the **Project Options** dialog:

![](images/visual-editing-project-options.png)

By default projects inherit the current global settings for markdown writing and Zotero libraries.

## File Options

Global and project options that affect the way markdown is written can also be customized on a per-file basis . You can do this by including an `editor: markdown` key in the YAML front matter of your document. For example:

``` yaml
---
title: "My Document"
author: "Jane Doe"
editor:
  markdown:
    wrap: 72
---
```

You might want to do this to ensure that multiple authors on different workstations use the same markdown writing options.

You can also instruct RStudio to use these same options when saving files from source mode. To do this add the `canonical` option. For example:

``` yaml
---
editor:
  markdown:
    wrap: 72
    canonical: true
---
```

With `canonical: true`, edits in visual mode and source mode will result in identical markdown output. This is especially useful if you have multiple authors collaborating using version control, with a mixture of source and visual mode editing among the authors.

See the documentation on [Writer Options](../../docs/visual-editor/markdown.llms.md#writer-options) for additional details on markdown writing options.
