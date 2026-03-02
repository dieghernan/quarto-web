> **NOTE:**
>
> This post is part of a series highlighting new features in the 1.3 release of Quarto. Get the latest release the [download page](../../../../docs/download/index.llms.md)

Starting in Quarto 1.3, you can include the output of an external Jupyter notebook in a Quarto document with the `embed` shortcode. To embed a notebook cell, provide the path to a Jupyter Notebook and a cell identifier. For example, this notebook called `penguins.ipynb` has a cell labelled `fig-bill-scatter`:

![A screenshot of a Jupyter Notebook with the name 'penguins.ipynb', with a cell highlighted that has the code chunk option label set to fig-bill-scatter. Below the cell is a plot that has been output.](notebook-simple.png)

You can use the following shortcode to embed the output of this cell:

``` markdown
{{< embed penguins.ipynb#fig-bill-scatter >}}
```

This will embed the plot as follows:

Figure 1: A scatterplot of bill dimensions for penguins, made with Altair.

[Source: Palmer Penguins](penguins-preview.llms.md#cell-fig-bill-scatter)

A link to the source notebook is automatically provided beneath the plot. Following the link takes users to a rendered version of the notebook, allowing them to explore the notebook without having to download and run it locally. For example, clicking on the link to `penguins.ipynb` gets you to a page that looks like the following:

![A screenshot of webpage with the title 'penguins.ipynb', a large blue button labelled 'Download Notebook', followed by the notebook contents.](notebook-view.png)

Beyond this basic usage, head to the [Jupyter Cell Embedding highlight docs](../../../../docs/authoring/notebook-embed.llms.md) to learn how to:

- Specify cells in multiple ways, see [Specifying Cells](../../../../docs/authoring/notebook-embed.llms.md#specifying-cells).

- Control the output using code cell options in the source Notebook, including things like figure captions, figure layout, and code display, see [Code Cell Options](../../../../docs/authoring/notebook-embed.llms.md#code-cell-options).

- Include the cell code along with the output by adding an `echo` option to the shortcode, see [Embedding Code](../../../../docs/authoring/notebook-embed.llms.md#embedding-code).

- Customize or exclude the link to the source notebook, see [Links to Source Notebooks](../../../../docs/authoring/notebook-embed.llms.md#linked-source-notebooks).
