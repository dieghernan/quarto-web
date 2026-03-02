# VS Code Notebook Editor

In addition to editing Quarto documents as plain-text `.qmd` files, you can also use the VS Code Notebook Editor to author `.ipynb` notebooks that are rendered with Quarto. In this article we’ll review the basics of editing `.ipynb` notebooks for use with Quarto.

## Render and Preview

![](../../../docs/tools/images/vscode-notebook.png)

After you’ve done an initial **Quarto: Preview**, the preview will automatically update every time you save the notebook.

## YAML Front Matter

The first cell of your notebook should be a **Raw** cell that contains the document title, author, and any other options you need to specify. Note that you can switch the type of a cell to **Raw** using the cell type menu at the bottom right of the cell:

![The top section of an ipynb file open in VS. There is a Raw cell containing yaml front matter.](../../../docs/tools/images/vscode-raw.png)

In this example we specify that we want code to appear collapsed by default. There are YAML options to control many other aspects of document rendering. See the documentation on [Authoring](../../../docs/authoring/markdown-basics.llms.md) and [Output Formats](../../../docs/output-formats/html-basics.llms.md) for additional details.

## Markdown Cells

Here’s the underlying code for the markdown cell:

![A snippet of an ipynb document containing a Markdown cell. The cell contains some text written in Markdown.](../../../docs/tools/images/vscode-markdown.png)

Note that a Quarto cross-reference (`@fig-polar`) is included in the markdown. Any valid Pandoc markdown syntax can be included in markdown cells.

## Output Options

Quarto uses leading comments with a special prefix (`#|`) to denote cell options. Here we specify the `label` and `fig-cap` options so that the plot generated from the cell can be cross-referenced.

![A snippet of a JupyterLab document containing a code cell. At the top of cell, before the code, are the Quarto chunk options '#\| label: fig-polar' and '#\| fig-cap: A line plot on a polar axis.'](../../../docs/tools/images/vscode-cell-options.png)

Note that options must appear at the very beginning of the cell. As with document front-matter, option names/values use YAML syntax.

There are many output options available, including options to optionally hide code, warnings, and/or output. See the documentation on [Output Options](../../../docs/computations/execution-options.llms.md#output-options) for additional details.

## Cell Execution

Note that when rendering an `.ipynb` Quarto **will not** execute the cells within the notebook by default (the presumption being that you have already executed them while editing the notebook). If you want to execute the cells you can pass the `--execute` flag to render:

``` bash
quarto render notebook.ipynb --execute
```

You can also specify this behavior within the notebook’s YAML front matter:

``` yaml
---
title: "My Notebook"
execute: 
  enabled: true
---
```

There are many other execution options available (e.g. to control caching, optimizing kernel start-up time, etc.). Learn more about these options in [Execution Options](../../../docs/computations/execution-options.llms.md).

## Converting Notebooks

You can convert between .ipynb and .qmd representations of a notebook using the `quarto convert` command. For example:

``` bash
quarto convert basics-jupyter.ipynb
quarto convert basics-jupyter.qmd
```

See `quarto convert help` for additional details on converting notebooks.
