# Tutorial: Hello, Quarto

- ### Choose your tool

- [![](../images/positron-logo.svg)Positron](positron.llms.md)

- [![](../images/vscode-logo.png)VS Code](vscode.llms.md)

- [![](../images/jupyter-logo.png)Jupyter](jupyter.llms.md)

- [![](../images/rstudio-logo.png)RStudio](rstudio.llms.md)

- [![](../images/neovim-logo.svg)Neovim](neovim.llms.md)

- [![](../images/text-editor-logo.png)Editor](text-editor.llms.md)

## Overview

In this tutorial we’ll show you how to use Jupyter Lab with Quarto. You’ll edit code and markdown in Jupyter Lab, just as you would with any notebook, and preview the rendered document in a web browser as you work.

Below is an overview of how this will look.

![On the left: A Jupyter notebook titled Quarto Basics containing some text, a code cell, and the result of the code cell, which is a line plot on a polar axis. On the right: Rendered version of the same notebook.](images/jupyter-quarto-preview.png)

The notebook on the left is *rendered* into the HTML version you see on the right. This is the basic model for Quarto publishing—take a source document (in this case a notebook) and render it to a variety of [output formats](../../../docs/output-formats/all-formats.llms.md), including HTML, PDF, MS Word, etc.

> **NOTE:**
>
> Note that while this tutorial uses Python, using Julia (via the [IJulia](https://julialang.github.io/IJulia.jl/stable/) kernel) is also well supported. See the article on [Using Julia](../../../docs/computations/julia.llms.md) for additional details.

## Rendering

We’ll start out by opening a notebook (`hello.ipynb`) in Jupyter Lab and rendering it to a couple of formats. If you want to follow along step-by-step in your own environment, download the notebook below.

> **NOTE:**
>
> [Download hello.ipynb](_hello.ipynb)

Then, create a new directory to work within, copy the notebook into this directory, and switch to this directory in a Terminal.

Next, execute these commands to install JupyterLab along with the packages used in the tutorial (`matplotlib` and `plotly),` and to open the tutorial notebook:

[TABLE]

Here is our notebook in Jupyter Lab.

```` markdown
---
title: "Quarto Basics"
format:
  html:
    code-fold: true
jupyter: python3
---

For a demonstration of a line plot on a polar axis, see @fig-polar.

```{python}
#| label: fig-polar
#| fig-cap: "A line plot on a polar axis"

import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(
  subplot_kw = {'projection': 'polar'} 
)
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

![A Jupyter notebook titled Quarto Basics containing some text, a code cell, and the result of the code cell, which is a line plot on a polar axis.](images/jupyter-basics.png)

Next, create a new Terminal within Jupyter Lab to use for Quarto commands.

![Screenshot of menu items in Jupuyter Lab: File \> New \> Terminal.](images/jupyter-terminal.png)

And finally, render the notebook to a couple of formats.

``` bash
quarto render hello.ipynb --to html
quarto render hello.ipynb --to docx
```

Note that the target file (in this case `hello.ipynb`) should always be the very first command line argument.

When you render a Jupyter notebook with Quarto, the contents of the notebook (code, markdown, and outputs) are converted to plain markdown and then processed by [Pandoc](http://pandoc.org/), which creates the finished format.

![Workflow diagram starting with a Jupyter notebook, then md, then pandoc, then PDF, MS Word, or HTML.](images/ipynb-how-it-works.png)

## Authoring

The `quarto render` command is used to create the final version of your document for distribution. However, during authoring you’ll use the `quarto preview` command. Try it now from the Terminal with `hello.ipynb`.

``` bash
quarto preview hello.ipynb
```

This will render your document and then display it in a web browser.

![Rendered version of the earlier notebook in a web browser.](images/quarto-preview.png)

You might want to position Jupyter Lab and the browser preview side-by-side so you can see changes as you work.

![Side-by-side preview of notebook on the left and live preview in the browser on the right.](images/jupyter-quarto-preview.png)

To see live preview in action:

1.  Change the line of code that defines `theta` as follows:

    ``` python
    theta = 4 * np.pi * r
    ```

2.  Re-run the code cell to generate a new version of the plot.

3.  Save the notebook (the preview will update automatically).

This is the basic workflow for authoring with Quarto. Once you are comfortable with this, we also recommend installing the [Quarto JupyterLab Extension](../../../docs/tools/jupyter-lab-extension.llms.md) which provides additional tools for working with Quarto in JupyterLab.

There are few different types of cells in our notebook, let’s work a bit with each type.

## YAML Options

You are likely already familiar with markdown and code cells, but there is a new type of cell (“Raw”) that is used for document-level YAML options.

``` yaml
---
title: "Quarto Basics"
format:
  html:
    code-fold: true
jupyter: python3
---
```

![YAML of the notebook with the fields title, format, and jupyter. Title is set to Quarto Basics with title: "Quarto Basics". Format is defined as html in the next line, and within the html format, code-fold is set to true. Jupyter is set to python3 with jupyter: python3.](images/jupyter-yaml.png)

Try changing the `code-fold` option to `false`.

``` yaml
format: 
  html:
    code-fold: false
```

Then save the notebook. You’ll notice that the code is now shown above the plot, where previously it was hidden with a **Code** button that could be used to show it.

## Markdown Cells

Markdown cells contain raw markdown that will be passed through to Quarto during rendering. You can use any valid Quarto [markdown syntax](../../../docs/authoring/markdown-basics.llms.md) in these cells. Here we specify a heading and a cross-reference to the figure created in the code cell below.

``` markdown
## Polar Axis

For a demonstration of a line plot on a polar axis, see @fig-polar.
```

![A Markdown cell with the title Polar Axis as a second level header and text that reads 'For a demonstration of a line plot on a polar axis, see @fig-polar.'](images/jupyter-markdown.png)

Try changing the heading and saving the notebook—the preview will update with the new heading text.

## Code Cells

You are likely already familiar with code cells, like the one shown below.

```` markdown
```{python}
#| label: fig-polar
#| fig-cap: "A line plot on a polar axis"

import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(
  subplot_kw = {'projection': 'polar'} 
)
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

![A code cell with cell options for label and fig-cap and the code required to create the line plot on a polar axis.](images/jupyter-cell.png)

But there are some new components at the top of the code cell: `label` and `fig-cap`options. Cell options are written in YAML using a specially prefixed comment (`#|`).

In this example, the cell options are used to make the figure cross-reference-able. Try changing the `fig-cap` and/or the code, running the cell, and then saving the notebook to see the updated preview.

There are a wide variety of [cell options](../../../docs/reference/cells/cells-jupyter.llms.md) that you can apply to tailor your output. We’ll delve into these options in the next tutorial.

> **NOTE:**
>
> One particularly useful cell option for figures is `fig-alt`, which enables you to add alternative text to images for users with visual impairments. See Amy Cesal’s article on [Writing Alt Text for Data Visualization](https://medium.com/nightingale/writing-alt-text-for-data-visualization-2a218ef43f81) to learn more.

## Next Up

You now know the basics of creating and authoring Quarto documents. The following tutorials explore Quarto in more depth:

- [Tutorial: Computations](../../../docs/get-started/computations/jupyter.llms.md) — Learn how to tailor the behavior and output of executable code blocks.

- [Tutorial: Authoring](../../../docs/get-started/authoring/jupyter.llms.md) — Learn more about output formats and technical writing features like citations, crossrefs, and advanced layout.

Additionally, you may want to install the [Quarto JupyterLab Extension](../../../docs/tools/jupyter-lab-extension.llms.md) which provides additional tools for working with Quarto in JupyterLab.
