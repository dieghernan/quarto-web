# Code Cells: Knitr

[Knitr](https://yihui.org/knitr/) is an R package for dynamic document generation. Learn more about using Knitr in the article on [Using R](../../../docs/computations/r.llms.md).

## Overview

Cell options affect the execution and output of executable code blocks. They are specified within comments at the top of a block. For example:

```` markdown
```{r}
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

## Cache

[TABLE]

## Include

|  |  |
|:---|:---|
| `child` | One or more paths of child documents to be knitted and input into the main document. |
| `file` | File containing code to execute for this chunk |
| `code` | String containing code to execute for this chunk |
| `purl` | Include chunk when extracting code with `knitr::purl()` |
