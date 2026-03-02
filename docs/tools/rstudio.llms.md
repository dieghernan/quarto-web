# RStudio IDE

## Overview

RStudio v2022.07 and later includes support for editing and preview of Quarto documents (the documentation below assumes you are using this build or a later version).

If you are using Quarto within RStudio it is **strongly** recommended that you use the [latest release](https://posit.co/download/rstudio-desktop/) of RStudio.

You can download RStudio from <https://posit.co/download/rstudio-desktop/>.

### Creating Documents

Use the **File :** **New File : Quarto Document…** command to create new Quarto documents:

![The 'New Quarto Document' dialog menu in RStudio.](../../docs/tools/images/new-quarto-doc.png)

### Render and Preview

Use the **Render** button to preview documents as you edit them:

![The top section of a qmd file as displayed in RStudio. There is a toolbar right above the document containing various options, including 'Render.' There is a stylized, segmented blue arrow pointing at the word.](../../docs/tools/images/rstudio-render.png)

If you prefer to automatically render whenever you save you can check the **Render on Save** option on the editor toolbar.

The preview will appear alongside the editor:

![An RStudio window. On the left half of the page is a Quarto document and the 'Jobs' pane open underneath that. There is messages in green text in the 'Jobs' pane that say: 'Watching files for changes. Browse at http://localhost:4064'. On the right half of the window is the Quarto output of the document on the left, as rendered by Knitr.](../../docs/tools/images/rstudio-preview.png)

The preview will update whenever you re-render the document. Side-by-side preview works for both HTML and PDF output.

### Projects

If you want to create a new project for a Quarto document or set of documents, use the **File : New Project…** command, specify **New Directory**, then choose **Quarto Project**:

![A section of the 'New Project Wizard' menu from Rstudio. This section is titled 'Create Quarto Project'. The Quarto logo is displayed on the left. ON the right are fields for 'Type', 'Directory name', and 'Create project as subdirectory of:'. Underneath that are options for 'Engine', 'Create a git repository', and 'Use renv with this project'. The option for 'Engine' is set to 'Knitr'. There are buttons for 'Create Project' and 'Cancel' arranged side-by-side in the bottom right of the window. There is an option to 'Open in new session' in the button left corner.](../../docs/tools/images/rstudio-new-knitr-project.png)

You can use this UI to create both vanilla projects as well as [websites](../../docs/websites/index.llms.md) and [books](../../docs/books/index.llms.md). Options are also provided for creating a [git](https://git-scm.com/) repository and initializing an [renv](https://rstudio.github.io/renv/) environment for the project.

## Visual Editor

RStudio IDE includes a visual editor for Quarto markdown, including support for tables, citations, cross-references, footnotes, divs/spans, definition lists, attributes, raw HTML/TeX, and more:

[![An RMarkdown file opened in the RStudio visual editor. The page is titled 'Filter joins'. Underneath is a table containing R syntax, mathematical notation, and definitions for the semi- and anti-joins. Underneath this table is an R code chunk that displays a graphical representation of a semi-join.](../visual-editor/images/visual-editing.png)](../../docs/visual-editor/index.llms.md)

To learn more, see the documentation on [Using the Visual Editor](../../docs/visual-editor/index.llms.md) with RStudio.

## Knitr Engine

Quarto is designed to be highly compatible with existing [R Markdown](https://rmarkdown.rstudio.com/) documents. You should generally be able to use Quarto to render any existing Rmd document without changes.

One important difference between R Markdown documents and Quarto documents is that in Quarto chunk options are typically included in special comments at the top of code chunks rather than within the line that begins the chunk. For example:

```` markdown
```{r}
#| echo: false
#| fig-cap: "Air Quality"

library(ggplot2)
ggplot(airquality, aes(Temp, Ozone)) + 
  geom_point() + 
  geom_smooth(method = "loess", se = FALSE)
```
````

Quarto uses this approach to both better accommodate longer options like `fig-cap`, `fig-subcap`, and `fig-alt` as well as to make it straightforward to edit chunk options within more structured editors that don’t have an easy way to edit chunk metadata (e.g. most traditional notebook UIs).

> **NOTE:**
>
> Note that if you prefer it is still possible to include chunk options on the first line (e.g. ```` ```{r, echo = FALSE} ````). That said, we recommend using the comment-based syntax to make documents more portable and consistent across execution engines.

Chunk options included this way use YAML syntax rather than R syntax for consistency with options provided in YAML front matter. You can still however use R code for option values by prefacing them with `!expr`. For example:

``` r
#| fig-cap: !expr 'paste("Air", "Quality")'
```

> **CAUTION:**
>
> the `!expr` syntax is an example of a YAML “tag” literal, and it can be unintuitive. `!expr` needs to be followed by a *single YAML “flow scalar”*: see the [YAML spec](https://yaml.org/spec/1.2.2/#73-flow-scalar-styles) for details on how double-quoted, single-quoted, and unquoted strings work.

## Jupyter Engine

You can also work with Quarto markdown documents that target the Jupyter engine within RStudio. These files will typically include a `jupyter` option in the YAML front matter indicating which kernel to use. For example:

``` yaml
---
title: "Matplotlib Demo"
author: "Norah Smith"
jupyter: python3
---
```

If you want to work within a virtual environment ([venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment)), use the **File :** **New Project…** command, specify the **Jupyter** engine with a venv, and specify which packages you’d like to seed the venv with:

![A section of the 'New Project Wizard' menu from Rstudio. This section is titled 'Create Quarto Project'. The Quarto logo is displayed on the left. ON the right are fields for 'Type', 'Directory name', and 'Create project as subdirectory of:'. Underneath that are options for 'Engine' and 'Kernel'. The option for 'Engine' is set to 'Jupyter,' and the option for 'Kernel' is set to 'Python 3'. Underneath these are options for 'Create a git repository', and 'Use venv with this project'. The button for 'Use venv...' is selected, and there is a text box to the right with the Python package names 'matplotlib' and 'pandas' filled in. There are buttons for 'Create Project' and 'Cancel' arranged side-by-side in the bottom right of the window. There is an option to 'Open in new session' in the button left corner.](images/rstudio-new-jupyter-project.png)

RStudio will automatically activate this virtual environment whenever you open the project. You can install additional Python packages into the environment using the RStudio **Terminal** tab. For example:

![An RStudio terminal window. The prompt is prefixed by the word '(env)', indicating that this prompt is taking place in a Python virtual environment named 'env.' The first line is empty and the second line contains the command 'python3 -m pip install scikit-learn.'](images/rstudio-pip-install.png)

## YAML Intelligence

YAML code completion is available for project files, YAML front matter, and executable cell options:

![Quarto document with YAML being edited. Next to the cursor code completion helper is open showing YAML options beginning with the letters preceding the cursor ('to').](images/rstudio-yaml-completion.png)

If you have incorrect YAML it will also be highlighted when documents are saved:

![Quarto document YAML metadata with an incorrect option underlined in red.](images/rstudio-yaml-diagnostics.png)

## R Package

If you are not using RStudio and/or you prefer to render from the R console, you can do so using the **quarto** R package. To install the R package:

``` r
install.packages("quarto")
```

Then, to render a document:

``` r
library(quarto)
quarto_render("document.qmd")
```

To render a website (ie; all qmd in a directory organized as a website):

``` r
library(quarto)
quarto_render()
```

To live preview (automatically render & refresh the browser on save) for a document you are working on, use the `quarto_preview()` function:

``` r
library(quarto)
quarto_preview("document.qmd")
```

If you are working on a [website](../../docs/websites/index.llms.md) or [book](../../docs/books/index.llms.md) project, you can also use `quarto_preview()` on a project directory:

``` r
library(quarto)
quarto_preview()
```
