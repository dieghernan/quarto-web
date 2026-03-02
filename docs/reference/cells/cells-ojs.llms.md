# Code Cells: Observable JS

[Observable JS](https://observablehq.com/@observablehq/observables-not-javascript) is a set of enhancements to vanilla JavaScript created by [Mike Bostock](https://en.wikipedia.org/wiki/Mike_Bostock) (also the author of [D3](https://d3js.org/)). Observable JS is distinguished by its [reactive runtime](https://github.com/observablehq/runtime), which is especially well suited for interactive data exploration and analysis.

Learn more about using Observable JS with Quarto in the articles on [Interactive Documents with Observable JS](../../../docs/interactive/ojs/index.llms.md).

## Overview

Cell options affect the execution and output of executable code blocks. They are specified within comments at the top of a block. For example:

```` markdown
```{ojs}
//| label: fig-polar
//| echo: false
//| fig-cap: "A line plot on a polar axis"
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

|  |  |
|:---|:---|
| `tbl-cap` | Table caption |
| `tbl-subcap` | Table subcaptions |
| `html-table-processing` | If `none`, do not process raw HTML table in cell output and leave it as-is |

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
