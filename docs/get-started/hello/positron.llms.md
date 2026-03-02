# Tutorial: Hello, Quarto

- ### Choose your tool

- [![](../images/positron-logo.svg)Positron](positron.llms.md)

- [![](../images/vscode-logo.png)VS Code](vscode.llms.md)

- [![](../images/jupyter-logo.png)Jupyter](jupyter.llms.md)

- [![](../images/rstudio-logo.png)RStudio](rstudio.llms.md)

- [![](../images/neovim-logo.svg)Neovim](neovim.llms.md)

- [![](../images/text-editor-logo.png)Editor](text-editor.llms.md)

> **TIP:**
>
> You can work through this tutorial using R or Python code examples. Select your preferred language:
>
> ## R
>
> You’ve selected to see examples in R. You can toggle to Python whenever you like throughout the guide.
>
> ## Python
>
> You’ve selected to see examples in Python. You can toggle to R whenever you like throughout the guide.

## Overview

Quarto is an open-source scientific and technical publishing system that weaves together code and narrative to produce high-quality documents, presentations, websites, and more. In this tutorial, you’ll learn how to use Positron with Quarto.

Positron comes ready to work with Quarto out-of-the-box — it includes both the Quarto command line interface and the [Quarto VS Code extension](https://open-vsx.org/extension/quarto/quarto).

It includes many tools that enhance working with Quarto, including:

- Integrated render and preview for Quarto documents

- Completion and diagnostics for Quarto options

- Positron’s full R and Python support for code that is inside a Quarto document, including interactive execution of code in the Console, code completion, help, and diagnostics.

Here’s a sample Quarto document, `hello.qmd`, open in Positron, demonstrating the seamless side-by-side editing and preview experience:

## R

![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-r-dark.png)![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-r.png)

## Python

![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-python-dark.png)![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-python.png)

On this page, you’ll learn:

- The basic edit, then preview, workflow for Quarto documents in Positron.

- The three components a Quarto document—header, code cells, and markdown—and how they combine to produce a rendered output.

## Setup

If you would like to follow along with this tutorial in your own environment, follow the steps outlined below.

## R

1.  Be sure that you have installed the `rmarkdown`, `tidyverse` and `palmerpenguins` packages:

    ``` r
    install.packages("rmarkdown")
    install.packages("tidyverse")
    install.packages("palmerpenguins")
    ```

2.  Download the Quarto document (`hello.qmd`) below and open it in Positron.

    > **NOTE:**
    > [Download hello.qmd](../../../docs/get-started/hello/_positron/r/hello.qmd)

## Python

1.  Install the `jupyter` and `plotnine` packages using your preferred method. For example, with `pip`:

    ``` bash
    pip install jupyter plotnine
    ```

2.  Download the Quarto document (`hello.qmd`) below and open it in Positron.

    > **NOTE:**
    > [Download hello.qmd](../../../docs/get-started/hello/_positron/python/hello.qmd)

## Basic Workflow

Quarto documents with the extension `.qmd` are a plain text format and will open in Positron’s Editor pane.

## R

![Positron with a file called \`hello.qmd\` open in the Editor.](images/positron-editor-r-dark.png)![Positron with a file called \`hello.qmd\` open in the Editor.](images/positron-editor-r.png)

## Python

![Positron with a file called \`hello.qmd\` open in the Editor.](images/positron-editor-python-dark.png)![Positron with a file called \`hello.qmd\` open in the Editor.](images/positron-editor-python.png)

To preview the document, execute the **Quarto: Preview** command. You can alternatively use the keyboard shortcut , or the **Preview** button (![Preview icon](../../../docs/tools/images/vscode-preview-icon.svg)![Preview icon](../../../docs/tools/images/vscode-preview-icon-white.svg)) in the editor toolbar:

![The top of the Positron code editor. The left side of the editor tab area includes a Preview button.](images/positron-editor-toolbar-dark.png)![The top of the Positron code editor. The left side of the editor tab area includes a Preview button.](images/positron-editor-toolbar.png)

Quarto will process the document, and the output will preview in the Viewer pane.

## R

![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-r-dark.png)![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-r.png)

## Python

![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-python-dark.png)![Positron with a Quarto document titled "Penguins, meet Quarto!" open on the left side and the rendered version of the document on the right side.](images/positron-hello-python.png)

The preview will update whenever you rerun the **Quarto: Preview** command. For example, change the section heading `## Meet the penguins` to `## Meet the Palmer penguins` and rerun the **Quarto: Preview** command. The preview in the Viewer will update to reflect the change.

## R

![Positron with \`hello.qmd\` open in the Editor, and a preview open in the Viewer. The Editor shows a markdown section updated to 'Meet the Palmer penguins', the Viewer shows the same updated section title.](images/positron-update-r-dark.png)![Positron with \`hello.qmd\` open in the Editor, and a preview open in the Viewer. The Editor shows a markdown section updated to 'Meet the Palmer penguins', the Viewer shows the same updated section title.](images/positron-update-r.png)

## Python

![Positron with \`hello.qmd\` open in the Editor, and a preview open in the Viewer. The Editor shows a markdown section updated to 'Meet the Palmer penguins', the Viewer shows the same updated section title.](images/positron-update-python-dark.png)![Positron with \`hello.qmd\` open in the Editor, and a preview open in the Viewer. The Editor shows a markdown section updated to 'Meet the Palmer penguins', the Viewer shows the same updated section title.](images/positron-update-python.png)

If you prefer the preview to update whenever you save the document, you can check the **Render on Save** box in the editor toolbar.

## Rendering

The document, `hello.qmd`, is a combination of markdown and executable code cells. Quarto uses the term *render* to describe the process of taking this source document and producing a new file that combines the output from the executed code cells with the markdown. When `hello.qmd` is rendered, the new output is `hello.html`, an [HTML](../../../docs/output-formats/all-formats.llms.md) document, but it could be a [PDF](../../../docs/output-formats/pdf-basics.llms.md), [MS Word](../../../docs/output-formats/ms-word.llms.md) document, [presentation](../../../docs/presentations/index.llms.md), [website](../../../docs/websites/index.llms.md), [book](../../../docs/books/index.llms.md), [interactive document](../../../docs/interactive/index.llms.md), or [other format](../../../docs/output-formats/all-formats.llms.md).

This is the basic model for Quarto publishing—take a source document that combines code and narrative, and render it to a variety of output formats.

The **Quarto: Preview** command encompasses two actions: rendering the document, and previewing the resulting file. HTML and PDF formats will open in Positron’s Viewer pane resulting in a side-by-side preview. Other formats, like MS Word, will open externally.

You can also render the document without previewing it by executing the **Quarto: Render Document** command.

> **TIP:**
>
> When you run the **Quarto: Preview** command, you will notice the Terminal executes `quarto preview`:
>
> ![The Positron Terminal pane showing the command 'quarto preview hello.qmd'.](images/positron-terminal-dark.png)![The Positron Terminal pane showing the command 'quarto preview hello.qmd'.](images/positron-terminal.png)
>
> The Quarto extension provides Positron commands as convenient alternatives to running `quarto` commands in the Terminal, but you can also run the commands directly if you prefer.

## Authoring

Let’s turn our attention to the contents of our Quarto document. The file contains three types of content: a header, executable code cells, and markdown text.

### Document header

At the top of the file is the document header demarcated by three dashes (`---`) on either end:

``` yaml
---
title: Hello, Quarto
format: html
---
```

Inside the header, document-level options are specified using YAML. The basic syntax of YAML uses key-value pairs in the format `key: value`.

In this case, the `title` is set to `"Hello, Quarto"` and the `format` is set to `html`. When rendered, the `title`, will appear at the top of the rendered document with a larger font size than the rest of the document. The `format` field denotes the target format for the output.

Other options commonly found in headers of documents include metadata like `author`, `subtitle`, and `date`, as well as customizations like `theme`, `fontcolor`, `fig-width`, etc. The available options depend on the output format and are listed in the [Reference](../../../docs/reference) e.g.: [HTML options](../../../docs/reference/formats/html.llms.md), [PDF options](../../../docs/reference/formats/pdf.llms.md) and [MS Word options](../../../docs/reference/formats/docx.llms.md).

### Code cells

Code cells contain executable code to be run during render, with the output (and optionally the code) included in the rendered document.

## R

Code cells are identified with `{r}`:

```` markdown
```{r}
#| label: load-packages
#| include: false
library(tidyverse)
library(palmerpenguins)
```
````

## Python

Code cells are identified with `{python}`:

```` markdown
```{python}
#| label: load-packages
#| include: false
from plotnine import *
from plotnine.data import penguins
```
````

Code cell options are set at the top of a code cell using special comments that start with `#|`. The options themselves are specified using YAML syntax. In this case, the `label` of the code cell is `load-packages`, and `include` is set to `false` to indicate that neither the code nor any of its outputs should appear in the rendered document. There are a wide variety of code cell options you can apply to tailor your output, you can learn more in the next tutorial on [Computations](../../../docs/get-started/computations/positron.llms.md).

In addition to rendering the complete document to view the results of code cells, you can also run each code cell interactively. Use the command: **Quarto: Run Cell**, the keyboard shortcut (), or click Run Cell directly above the cell in the Editor. Positron executes the code in the Console and displays the results.

## R

![A Positron session with \`hello.qmd\` open in the Editor. An orange box highlights the button 'Run Cell' above a code cell with the label \`plot-penguins\`. The Console shows an executed line of code ending in \`theme_minimal()\` and the Plots pane shows a scatterplot of penguin flipper and bill length.](images/positron-run-cell-r-dark.png)![A Positron session with \`hello.qmd\` open in the Editor. An orange box highlights the button 'Run Cell' above a code cell with the label \`plot-penguins\`. The Console shows an executed line of code ending in \`theme_minimal()\` and the Plots pane shows a scatterplot of penguin flipper and bill length.](images/positron-run-cell-r.png)

## Python

![A Positron session with \`hello.qmd\` open in the Editor. An orange box highlights the button 'Run Cell' above a code cell with the label \`plot-penguins\`. The Console shows an executed line of code ending in \`theme_minimal()\` and the Plots pane shows a scatterplot of penguin flipper and bill length.](images/positron-run-cell-python-dark.png)![A Positron session with \`hello.qmd\` open in the Editor. An orange box highlights the button 'Run Cell' above a code cell with the label \`plot-penguins\`. The Console shows an executed line of code ending in \`theme_minimal()\` and the Plots pane shows a scatterplot of penguin flipper and bill length.](images/positron-run-cell-python.png)

### Markdown text

Narrative content is written using markdown. For example, the following excerpt includes a section heading (`## heading`), text formatted as code (`` `code` ``) and a link (`[text](url)`):

## R

``` markdown
## Meet the Palmer penguins

The `penguins` data from the [**palmerpenguins**](https://allisonhorst.github.io/palmerpenguins) package contains...
```

## Python

``` markdown
## Meet the Palmer penguins

The `penguins` data from the [plotnine](https://plotnine.org/reference/penguins.html) package contains...
```

Quarto supports markdown syntax for basic text formatting, tables, and images, as well as advanced features like citations, cross-references, and equations. You can learn more about markdown in the [Markdown Basics](../../../docs/authoring/markdown-basics.llms.md) documentation.

## How it works

## R

When you render a Quarto document, first [knitr](http://yihui.name/knitr/) executes all of the code cells and creates a new markdown (.md) document, which includes the code and its output.

The markdown file generated is then processed by [pandoc](http://pandoc.org/), which creates the finished format.

![Workflow diagram starting with a qmd file, then knitr, then md, then pandoc, then PDF, MS Word, or HTML.](images/rstudio-qmd-how-it-works.png)

## Python

When you render a Quarto document, first [jupyter](https://jupyter.org) executes all of the code cells and creates a new markdown (.md) document, which includes the code and its output.

The markdown file generated is then processed by [pandoc](http://pandoc.org/), which creates the finished format.

![Workflow diagram starting with a qmd file, then Jupyter, then md, then pandoc, then PDF, MS Word, or HTML.](images/qmd-how-it-works.png)

> **TIP:**
>
> When a Quarto document includes executable code cells, Quarto uses what is known as an *engine* to execute them. If you’re following along with this tutorial with R, you have been using the `knitr` engine. If you’re following along with Python, you have been using the `jupyter` engine. You can read more about how Quarto chooses an engine in [Engine Binding](../../../docs/computations/execution-options.llms.md#engine-binding).
>
> Quarto supports other languages in addition to R and Python for code cells like [Julia](../../../docs/computations/julia.llms.md) (via the `julia` engine or the `jupyter` engine) and [Observable JS](../../../docs/computations/ojs.llms.md).

## Next Up

You now know the basics of creating and authoring Quarto documents. The following tutorials explore Quarto in more depth:

- [Tutorial: Computations](../../../docs/get-started/computations/positron.llms.md) — Learn how to tailor the behavior and output of executable code blocks.

- [Tutorial: Authoring](../../../docs/get-started/authoring/positron.llms.md) — Learn more about output formats and technical writing features like citations, crossrefs, and advanced layout.
