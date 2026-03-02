# Custom Formats

## Overview

Quarto format extensions enable you to add new formats to the built-in formats (e.g. `html`, `pdf`, `docx`) already available. Custom formats can provide default document options, style-sheets, header, footer, or logo elements, and even bundle other extensions like [filters](../../docs/extensions/filters.llms.md) and [shortcodes](../../docs/extensions/shortcodes.llms.md). They are a great way to provide a common baseline for authoring documents or presentations within an organization, for a particular type of project or analysis, or for a specific publication.

You can specify a custom format beneath the `format` key just like a built-in format. For example:

``` yaml
---
title: "My Document"
format:
   acm-pdf: 
     toc: true
---
```

Custom formats all derive from one of the base formats, and include that base format as a suffix. Formats can also provide multiple variations that derive from distinct base formats. For example:

``` yaml
---
title: "My Document"
toc: true
format:
   acm-pdf: default
   acm-html: default
---
```

Note that we moved the `toc` option to the top level since it is shared between both of the formats.

Custom formats can also be used with the `--to` argument to `quarto render`. For example:

``` bash
quarto render document.qmd --to acm-html
```

Note that if you are specifically interested in using or creating custom formats for journals and manuscripts, you may want to proceed instead to the documentation on [Journal Articles](../../docs/journals/index.llms.md).

## Quick Start

Here we’ll describe how to create a simple HTML-based format extension. We’ll use the `quarto create` command to do this. If you are using VS Code, Positron, or RStudio you should execute `quarto create` within their respective integrated Terminal panes.

To get started, execute `quarto create extension format:html` within the parent directory where you’d like the format to be created:

``` bash
$ quarto create extension format:html
 ? Extension Name › lexdoc
```

As shown above, you’ll be prompted for an extension name. Type `lexdoc` (a document format for a fictional company named LexCrop) and press Enter—the custom format extension is then created:

``` bash
Creating extension at /Users/jjallaire/quarto/dev/lexdoc:
  - Created README.md
  - Created _extensions/lexdoc/custom.scss
  - Created _extensions/lexdoc/_extension.yml
  - Created template.qmd
```

If you are running within VS Code, Positron, or RStudio a new window will open with the extension project.

> **NOTE:**
>
> Note that this example creates a format that is derivative of the Quarto base `html` format. You can similarly create formats that are derivative of `pdf`, `docx`, and `revealjs` as follows:
>
> ``` bash
> quarto create extension format:pdf
> quarto create extension format:docx
> quarto create extension format:revealjs
> ```

Here’s what the contents of the files in `_extensions/lexdoc/` look like:

``` yaml
title: Lexdoc
author: J.J. Allaire
version: 1.0.0
quarto-required: ">=1.2.222"
contributes:
  formats:
    html:
      toc: true
      theme: [yeti, custom.scss]
```

The custom HTML format defined here is very simple. It takes the base `html` format, turns on the table of contents by default, and sets the theme as `yeti` along with a `custom.scss` file for additional customizations:

``` css
/*-- scss:defaults --*/

/* TODO: Customize appearance with SCSS variables */
/* See [HTML theme](https://quarto.org/docs/output-formats/html-themes.html#theme-options) */

/*-- scss:rules --*/

/* TODO: Provide custom CSS rules */
```

Finally, the `template.qmd` provides a base example article for users of the format:

``` markdown
---
title: "Lexdoc Example"
format:
  lexdoc-html: default
author: J.J. Allaire
date: last-modified
---

## Introduction

*TODO* Create an example file that demonstrates the formatting and features of your format.

## More Information

You can learn more about controlling the appearance of HTML output here: <https://quarto.org/docs/output-formats/html-basics.html>
```

To develop your format, render/preview `template.qmd`, and then make changes to the various files in the `_extensions` directory (the preview will automatically refresh when you change these files).

## Example: Revealjs

Next, we’ll walk through the creation of a custom format that extends the `revealjs` presentation format. Here is what the source code repository of the format extension might look like:

``` default
README.md
LICENSE
template.qmd
_extensions/
  lexconf/
    _extension.yml
    theme.scss
    logo.png
    title.png
```

Note that the format suffix (`revealjs`) is excluded from the directory name (this is to account for the possibility of multiple formats e.g. `lexconf-revealjs`, `lexconf-pptx`, etc.)

As with other types of extensions, the only thing strictly required is the `_extensions` directory (anything above that is for your own purposes and is ignored during format installation). Even so, it’s good practice to include a `README.md` and `LICENSE` file. The `template.qmd` file serves a couple of purposes:

1.  It can be rendered as you develop your format to ensure that things work as expected.
2.  It can serve as the basis for a format template (which helps users gets started with using your format).

Here is what the contents of `_extension.yml` might look like:

``` yaml
title: LexConf 2022 Presentation
author: LexCorp
version: 1.0.0
quarto-required: ">=1.2.0"
contributes:
  formats:
    revealjs:
       theme: [default, theme.scss]
       logo: logo.png
       footer: | 
         Copyright 2022 (c) LexCorp, Inc.
       title-slide-attributes:
          data-background-image: title.png
          data-background-size: contain
       preview-links: auto
       
```

This format mostly provides organization-level content and theming. As mentioned above, formats can also include filters which allow for adding custom markdown constructs and rendering behavior.

Here is what the contents of `template.qmd` might look like:

``` markdown
---
title: "Presentation"
subtitle: "LexConf 2022"
author: "Your Name"
date: today
format: lexconf-revealjs
---

# Overview
```

Extension repositories are structured in such a way that you can test your extension and the template by simply rendering the `template.qmd` file right in the root of your repository. The `template.qmd` will be able to load your extension just as it would when installed, so testing and iterating should be as simple as working within your extension directory until you’re satisfied (without the need to repeatedly install or update the extension in order to test it).

## Format Templates

Above we described including a `template.qmd` alongside your extension and then installing the template and format together with:

``` bash
quarto use template <gh-organization>/<extension>
```

The `template.qmd` should demonstrate the functionality of the format and serve as a sound starting point for the user. When the extension template is copied into the target directory, the `template.qmd` will automatically be renamed to match the name that the user provided for the directory.

You can also include other files alongside `template.qmd` and they will be copied as well. Note that by default, Quarto will exclude common Github repository files when copying an extension template. This includes any file name or directory starting with a `.` (e.g. `.gitignore`), `README.md`, `LICENSE`, etc.. If you’d like, you can place a `.quartoignore` file in the root of your repository with each line of the file being a glob describing file(s) to ignore (using syntax like a `.gitignore` file).

## Distributing Formats

You can distribute format extensions in one of two ways:

1.  As a template that includes both the format in the `_extensions` directory and the `template.qmd` (which is automatically renamed to match the name of the enclosing directory).

2.  As a plain format with no template scaffolding (this is useful for adding the format to an existing document or project).

If you have a GitHub repository containing the files enumerated above in the `lexconf` example, users could install your extension and associated template as follows (where `lexcorp` is the GitHub organization hosting the repo):

``` bash
quarto use template lexcorp/lexconf
```

This is often the preferred way to get started with a format as it provides the user with a working document right out of the box. It’s also possible to install *only* the format if you are working with an existing project:

``` bash
quarto add lexcorp/lexconf
```

Note that it is possible to bundle and distribute extensions as simple gzip archives (as opposed to using a GitHub repository as described above). See the article on [Distributing Extensions](../../docs/extensions/distributing.llms.md) for additional details.

## Multiple Formats

A single format extension can support more than one output format. For example, an extension may target `html` and `pdf` output. To support multiple formats in your extension, you can add additional base formats to the `contributes / format` key like so:

``` yaml
contributes:
  format:
    html:
      # html-specific options
    pdf:
      # pdf-specific options
```

## Common Metadata

If you have metadata that is common to any output format when your format extension is targeted, you can place that metadata under the `common` key. For example:

``` yaml
contributes:
  format:
    common:
      filters:
        - filter.lua
      shortcodes:
        - quarto-ext/fancy-text
    html:
      # html-specifc
    pdf:
      # pdf-specifc
```

## Format Resources

You can usually include other files and resources within a format extension by placing those files within the extension directory and using relative paths to reference them in your `_extension.yml` metadata file. These relative paths will be properly handled as your extension’s metadata is merged with the rendered document metadata.

If there are resources that you need to have copied to the input directory as a part of rendering the document (for example, a `bst` file for LaTeX bibliographies or a logo or other file referenced from a LaTeX template), you can provide `format-resources`, which is a list of file paths[^1]. Each of these files will be copied into the directory containing the input that is being rendered when the document is rendered. For example:

``` yaml
contributes:
  format:
    pdf:
      format-resources:
        - plos2015.bst
```

## Extension Embedding

In some cases format extensions will want to make use of other extensions. This is permitted, but adding extensions for use within a custom format must be done with a special command line flag to ensure they are embedded correctly.

``` bash
quarto create extension format:pdf myformat
cd myformat
quarto add quarto-ext/fancy-text --embed myformat
```

For example, here we want to make the [fancy-text](https://github.com/quarto-ext/fancy-text) extension (which provides special formatting for the words \\\LaTeX\\ and BIBT_(E)X) available for users of the [jss](https://github.com/quarto-journals/jss) custom format:

``` bash
quarto add quarto-ext/fancy-text --embed jss
```

This will produce the following output:

``` bash
quarto-journals/jss
└── _extensions
    └── jss
        ├── _extensions
        │   └── quarto-ext
        │       └── fancy-text
        └── partials
```

This will add the `quarto-ext/fancy-text` extension into the `jss` extension in the `_extensions` folder. By embedding an extension you make it available without creating the potential for conflict with other versions of the extension that users might already have installed.

## Footnotes

[^1]: This is most common in the the case of PDF based formats which have a secondary step of converting the LaTeX produced by Pandoc into a PDF. If there are files that are referenced indirectly by the LaTeX, they will need to be discoverable and should typically be copied into the same directory that contains the LaTeX input.
