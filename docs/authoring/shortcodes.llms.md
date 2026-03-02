# Shortcodes

## Overview

Shortcodes are special markdown directives that generate various types of content. Quarto shortcodes are similar in form and function to [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/) and [WordPress shortcodes](https://codex.wordpress.org/Shortcode).

For example, the following shortcode prints the `title` from document metadata:

``` markdown
{{< meta title >}}
```

## Built-in Shortcodes

Quarto supports several shortcodes natively:

| Shortcode | Description |
|----|----|
| [version](../../docs/authoring/version.llms.md) | Print Quarto CLI version |
| [var](../../docs/authoring/variables.llms.md#var) | Print value from `_variables.yml` file |
| [meta](../../docs/authoring/variables.llms.md#meta) | Print value from document metadata |
| [env](../../docs/authoring/variables.llms.md#url) | Print system environment variable |
| [pagebreak](../../docs/authoring/markdown-basics.llms.md#page-breaks) | Insert a native page-break |
| [kbd](../../docs/authoring/markdown-basics.llms.md#keyboard-shortcuts) | Describe keyboard shortcuts |
| [video](../../docs/authoring/videos.llms.md) | Embed a video in a document |
| [include](../../docs/authoring/includes.llms.md) | Include contents of another qmd |
| [embed](../../docs/authoring/notebook-embed.llms.md) | Embed cells from a Jupyter Notebook |
| [placeholder](../../docs/authoring/placeholder.llms.md) | Add placeholder images to your document |
| [lipsum](../../docs/authoring/lipsum.llms.md) | Add placeholder text to your document |
| [contents](../../docs/authoring/contents.llms.md) | Rearrange content in your document |

If you want to dive in to creating your own shortcode, check out the article on [Creating Shortcodes](../../docs/extensions/shortcodes.llms.md).
