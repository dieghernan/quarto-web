# Code Cells: Jupyter

[Jupyter](https://jupyter.org) is an open document format that supports computations in many languages including Python, R, and Julia. Learn more about using Jupyter with Quarto in the articles on [Using Python](../../../docs/computations/python.llms.md) and [Using Julia](../../../docs/computations/julia.llms.md).

## Overview

Cell options affect the execution and output of executable code blocks. They are specified within comments at the top of a block. For example:

```` markdown
```{python}
#| label: fig-polar
#| echo: false
#| fig-cap: "A line plot on a polar axis"
```
````

## Attributes

|  |  |
|:---|:---|
| `label` | Unique label for code cell. Used when other code needs to refer to the cell (e.g. for cross references `fig-samples` or `tbl-summary`) |
| `classes` | Classes to apply to cell container |
| `renderings` | Array of rendering names, e.g. `[light, dark]` |
| `tags` | Array of tags for notebook cell |
| `id` | Notebook cell identifier. Note that if there is no cell `id` then `label` will be used as the cell `id` if it is present. See [https://jupyter.org/enhancement-proposals/62-cell-id/cell-id.html](https://jupyter.org/enhancement-proposals/62-cell-id/cell-id.llms.md) for additional details on cell ids. |

## Code Output

[TABLE]

## Cell Output

[TABLE]

## Figures

[TABLE]

## Tables

[TABLE]

## Panel Layout

[TABLE]

## Page Columns

|  |  |
|:---|:---|
| `column` | [Page column](https://quarto.org/docs/authoring/article-layout.llms.md) for output |
| `fig-column` | [Page column](https://quarto.org/docs/authoring/article-layout.llms.md) for figure output |
| `tbl-column` | [Page column](https://quarto.org/docs/authoring/article-layout.llms.md) for table output |
| `cap-location` | Where to place figure and table captions (`top`, `bottom`, or `margin`) |
| `fig-cap-location` | Where to place figure captions (`top`, `bottom`, or `margin`) |
| `tbl-cap-location` | Where to place table captions (`top`, `bottom`, or `margin`) |
