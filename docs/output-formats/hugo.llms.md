# Hugo

## Overview

[Hugo](https://gohugo.io/) is a very popular open source website publishing system. Pages in Hugo websites are typically written in plain markdown, so don’t have a straightforward way to automatically and reproducibly incorporate computational output.

Using the Quarto `hugo-md` format, you can incorporate computational output (e.g. R or Python code that produces plots) into Hugo websites. This article explains how.

It’s important to note that many of the Quarto features related to theming, page layout, and navigation are not applicable when you are using Quarto with Hugo. Hugo has its own theming system, syntax highlighting, table of contents, page layout, navigational menus, and full text search. You’ll use Quarto to execute code and generate markdown that is rendered within the Hugo HTML publishing framework rather than Quarto’s own.

## Site Config

There are a couple of changes you should make to your Hugo `config.toml` in preparation for using Quarto with Hugo. First, make sure that `.qmd` and `.ipynb` files and other source code or data files are not published as part of the site. For example:

``` toml
ignoreFiles = [ "\\.qmd$", "\\.ipynb$", "\\.py$" ]
```

Next, configure Hugo’s markdown renderer to allow raw HTML (as many R and Python packages will produce computational output using raw HTML rather than markdown):

``` toml
[markup.goldmark.renderer]
unsafe= true
```

## Creating a Page

Hugo articles and posts that use Quarto should live in their own directory (taking advantage of the Hugo [Page Bundles](https://gohugo.io/content-management/page-bundles/) feature). This allows any content generated/referenced by the page (e.g. plot output) to live right alongside the markdown source.

To add Quarto documents to a Hugo site:

1.  Create a directory within `content` that will hold your Quarto article.

2.  Add an `index.qmd` document to the directory. When rendered this will create an `index.md`, which in turn will ensure that Hugo treats it as a [Page Bundle](https://gohugo.io/content-management/page-bundles/) (automatically copying images and other referenced resources to the publish directory).

3.  Add the requisite Hugo [front matter](https://gohugo.io/content-management/front-matter/), then also specify `format: hugo-md` and any other required Quarto options.

For example, let’s say we wanted to create a new article named `hello-quarto` within the `content` directory. The filesystem would look like this:

``` ini
mysite/
  content/
    hello-quarto/
      index.qmd
```

Here’s what the source code of `index.qmd` might look like:

```` markdown
---
title: Hello, Quarto
date: "2012-04-06"
categories: 
  - Matplotlib
  - Coordinates
format: hugo-md
jupyter: python3
---

## Polar Axis

For a demonstration of a line plot on a polar axis, see @fig-polar.

```{python}
#| label: fig-polar
#| fig-cap: "A line plot on a polar axis"

import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

## Workflow

The basic concept of using Quarto with Hugo is that you take *computational* markdown documents (`.qmd`) or Jupyter notebooks (`.ipynb`) and use them to generate plain markdown files (`.md`) that are rendered to HTML by Hugo.

**index.qmd**   *quarto =\>*   **index.md**   *hugo =\>*   **index.html**

The `quarto render` and `quarto preview` commands are used to transform `.qmd` or `.ipynb` files to Hugo compatible markdown (`.md`). The computational files are located in the same place you would also locate ordinary markdown files (e.g. the `blog` directory).

After rendering, a plain `.md` file is written right alongside the computational document. This markdown file is then processed by Hugo.

### Live Preview

The `quarto preview` command will automatically recognize when it is run from a directory that contains a Hugo website:

``` bash
cd my-hugo-website
quarto preview
```

This will automatically run `hugo` on your behalf to bring up a local preview server. In addition, it will monitor the filesystem for changes to `.qmd` and `.ipynb` inputs and automatically re-render them to Hugo compatible `.md` files when they change.

Note that this also works for the integrated Preview command within the Quarto VS Code Extension in [VS Code](../../docs/tools/vscode/index.llms.md) or [Positron](../../docs/tools/positron/index.llms.md).

### Rendering

If you are not previewing and want to render all of the Quarto documents (`.qmd`) and notebooks (`.ipynb`) in your site, call `quarto render` from the root directory of the site:

``` bash
cd my-hugo-website
quarto render 
```

Typically you’ll want to do a `quarto render` at the site level before you build the site for publishing:

``` bash
quarto render && hugo
```

You can also render individual documents or notebooks:

``` bash
quarto render blog/2022-07-26/hello-quarto/index.qmd
```

If you have computationally expensive documents you may want to consider using Quarto’s [freeze](../../docs/projects/code-execution.llms.md#freeze) feature to only re-execute code when your document source code changes.

Note that if aren’t ever rendering at the project level and just have individual files that you want to render with Quarto, you should specify the `hugo-md` format as follows:

``` yaml
---
title: "My Blog Post"
format: hugo-md
---
```

### Configuration

While Quarto works well within a Hugo site that has no `_quarto.yml` project config file, you can add one if you want to customize the default behavior, add a bibliography, etc. For example, here is what a simple customized `_quarto.yml` file might look like:

``` yaml
project:
  type: hugo
      
format: 
  hugo-md:
    code-fold: true
  
execute: 
  warning: false

bibliography: references.bib
```

It’s important to note that if you do provide an explicit `_quarto.yml` file you need to explicitly specify the project type (`type: hugo`) as shown above.

#### External Directory

You might decide that you prefer to keep all of your Quarto documents and/or notebooks in their own directory, separate from the Hugo website. In this configuration you would mirror the directory structure of your site in the Quarto directory, and then set the `output-dir` in the project file to point to the Hugo directory. For example:

``` yaml
project:
  type: hugo
  output-dir: ../hugo-site
```

## Shortcodes

Note that Hugo [shortcodes](https://gohugo.io/content-management/shortcodes/) and Quarto [shortcodes](../../docs/extensions/shortcodes.llms.md) share the same basic syntax (e.g. `{{< var foo >}}`). This is normally not a problem as shortcodes not recognized by Quarto are passed through unmodified to Hugo.

However, in some cases the use of a Hugo shortcode throws off Pandoc markdown processing, and its necessary to “protect” the Hugo shortcode from processing by Pandoc. This can typically be handled by escaping the shortcode with an extra brace. For example:

``` default
{{{< ref "foo/index.md" >}}}
```

It’s possible that this won’t be enough if the presence of the shortcode changes how Pandoc processes the surrounding markdown (e.g. this is currently known to occur for links). In this case you need to use a markdown raw block around the entire construct. For example:

```` default
```{=markdown}
[click here]({{< ref "foo/index.md" >}})
```
````

Or for inline content, use a markdown raw inline:

``` default
For more info, `[click here]({{< ref "foo/index.md" >}})`{=markdown}
```

## WebTeX Math

The `hugo` format renders LaTeX equations using standard dollar-delimited inline (`$...$`) and display (`$$...$$`) syntax. However, if the web environment you are publishing into doesn’t support dollar-delimited math, you can alternatively use [WebTeX](https://github.com/KTHse/webtex) to display math. This is done by setting the Pandoc `html-math-method` to `webtex`. For example:

``` yaml
format:
  hugo:
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

SVG is used as the default rendering method because it has the best overall appearance. However, if your `hugo` document is being rendered on a dark background, you may want to switch to PNG with a dark background specified. You can do this as follows:

``` yaml
format:
   hugo:
     html-math-method: 
       method: webtex
       url: https://latex.codecogs.com/png.image?%5Cbg_black&space;
```
