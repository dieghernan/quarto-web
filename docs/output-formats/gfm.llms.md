# GitHub (GFM)

## Overview

While markdown is the input format for Quarto, it can also in some cases be an output format (for example, if you have a website or CMS that accepts markdown as input and want to incorporate computations from Python or R).

This article covers using Quarto to generate [GitHub Flavored Markdown](https://github.github.com/gfm/) (GFM). You might want to do this in order to:

- Generate a GitHub README.md from a Jupyter notebook

- Create pages for a GitHub wiki that include computations (e.g. plot output).

## GFM Format

Use the `gfm` format to create GitHub Flavored Markdown from Quarto. For example:

``` yaml
---
title: "My Project"
format: gfm
---
```

See the GFM [format reference](../../docs/reference/formats/markdown/gfm.llms.md) for a complete list of all options available for GFM output.

To create a `README.md` using Quarto, start with a notebook (.ipynb) or computational markdown file (.qmd) that has README as its file name stem, for example:

```` markdown
---
title: "My Project"
format: gfm
jupyter: python3
---

This is a GitHub README that has content dynamically generated from Python:
    
```{python}
1 + 1
```
````

Render the README with:

``` bash
quarto render README.qmd
```

Which will create `README.md` alongside your input file.

## Preview Mode

When you `quarto preview` a GitHub Flavored Markdown document, by default an HTML preview that approximates the look of markdown rendered on GitHub is shown. If you’d prefer to see the raw generated markdown, use the `preview-mode: raw` option. For example:

``` yaml
---
title: "My Project"
format: 
  gfm:
    preview-mode: raw
---
```

## WebTeX Math

The `gfm` format renders LaTeX equations using standard dollar-delimited inline (`$...$`) and display (`$$...$$`) syntax. However, if the web environment you are publishing into doesn’t support dollar-delimited math, you can alternatively use [WebTeX](https://github.com/KTHse/webtex) to display math. This is done by setting the Pandoc `html-math-method` to `webtex`. For example:

``` yaml
format:
  gfm:
    html-math-method: webtex
```

WebTeX works for any web page that can display images, and requires no special JavaScript or CSS. Any inline or display equations contained within your document will be converted to an image URL that requests a rendered version of the equation. For example, the following markdown:

``` markdown
$x + 1$
```

Will be converted to:

``` markdown
![](https://latex.codecogs.com/svg.latex?x%20%2B%201)
```

Which renders as:

### Dark Mode

SVG is used as the default rendering method because it has the best overall appearance. However, if your `gfm` document is being rendered on a dark background, you may want to switch to PNG with a dark background specified. You can do this as follows:

``` yaml
format:
   gfm:
     html-math-method: 
       method: webtex
       url: https://latex.codecogs.com/png.image?%5Cbg_black&space;
```

## GitHub Wikis

If you want to use Quarto to incorporate computations into a GitHub wiki start by [cloning the wiki for local editing](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages#adding-or-editing-wiki-pages-locally).

Then, simply create a computational markdown file (.ipynb, .qmd) for each page in the wiki. You can render all of these files at once into their corresponding .md files using [Quarto Projects](../../docs/projects/quarto-projects.llms.md). For example:

``` bash
quarto render
```

You don’t even strictly need a Quarto project file to do this as `quarto render` will render all input files in a directory by default if there is no project file.
