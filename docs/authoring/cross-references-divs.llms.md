# Cross-Reference Div Syntax

## Overview

Cross-referenceable [figures](#figures), [tables](#tables) and [code listings](#listings) are known as *float* cross-references. Floats can appear in the rendered document at locations other than where they are defined, i.e. they float, and usually have captions.

Along with compact syntax for the most common uses of cross-references, Quarto also provides a more general div syntax for declaring floats that can be cross-referenced. To declare a cross-referenceable float, place the content inside a fenced div with the reference identifier as an attribute. The last paragraph inside the fenced div will be treated as the caption.

> **WARNING:**
>
> Quarto currently only supports this alternative syntax for **floats**, as described above. Some cross-referenceable elements like theorems, proofs, etc naturally use this div syntax, but note that Quarto does not support the use of the div syntax for block-level equations.

As a minimal example, consider the following QMD snippet:

``` markdown
::: {#fig-example}

CONTENT

Caption

:::
```

This produces the following (admittedly silly) figure:

CONTENT

Figure 1: Caption

Now, this figure can be cross-referenced with `@fig-example`, see [Figure 1](#fig-example).

To be recognized as a cross-reference the identifier must begin with one of the built-in float reference types (Figures (`fig-`), Tables (`tbl-`) and Listings (`lst-`)), or be defined as a [custom float cross-reference](../../docs/authoring/cross-references-custom.llms.md) type.

You can then refer to the element as usual with the `@` syntax, e.g. 

``` markdown
@fig-example shows...
```

The content can be any Quarto markdown. For example, [Figure 2](#fig-table) is a markdown table treated like a figure:

``` markdown
::: {#fig-table}

| A | B |
|---|---|
| C | D |

A table treated like a figure 

:::
```

| A   | B   |
|-----|-----|
| C   | D   |

Figure 2: A table treated like a figure

[Table 1](#tbl-table) is an image treated like a table:

``` markdown
::: {#tbl-table}

![](table.png)

An image treated like a table

:::
```

![](images/crossref-div-table.png)

Table 1: An image treated like a table

[Figure 3](#fig-code) is a code cell treated like a figure:

```` markdown
::: {#fig-code}

```r
library(tidyverse)
starwars |> 
  ggplot(aes(height, mass)) + 
  geom_point()
```

A code cell treated like a figure.

:::
````

``` r
library(tidyverse)
starwars |> 
  ggplot(aes(height, mass)) + 
  geom_point()
```

Figure 3: A code cell treated like a figure.

On this page, we illustrate common use cases for [Figures](#figures), [Tables](#tables) and [Code Listings](#listings) then some applications of the div syntax to:

- [Cross-reference a video](#videos)
- [Cross-reference a diagram](#diagrams)
- [Produce subreferences to mixed content](#subreferences)
- [Use computed values in a caption](#computed-captions)

## Figures

To create a cross-reference to a figure using div syntax, create a fenced div with an id starting with `fig-`, include the image followed by the caption inside the div:

``` markdown
::: {#fig-elephant}

![](elephant.png)

An Elephant
:::
```

You can cross-reference a figure created by an executable code cell by including the code cell as the content:

```` markdown
::: {#fig-line-plot}

```{python}
import matplotlib.pyplot as plt
plt.plot([1,23,2,4])
plt.show()
```

A line plot
:::
````

In the above example, you can reference the figure with `@fig-line-plot`, but not the code, which appears inline. If you would also like to be able to refer to the code, you can do so using code chunk options rather than the div syntax, see [Cross-References for Executable Code Blocks](../../docs/authoring/cross-references.llms.md#code-listings) for details.

## Tables

To create a cross-reference to a table using div syntax, create a fenced div with an id starting with `tbl-`, include the table followed by the caption inside the div:

``` markdown
::: {#tbl-letters}

| Col1 | Col2 | Col3 |
|------|------|------|
| A    | B    | C    |
| E    | F    | G    |
| A    | G    | G    |

My Caption

::: 
```

If the table is produced by an executable code cell, put the cell inside the div as content, e.g:

```` markdown
::: {#tbl-planets}

```{python}
from IPython.display import Markdown
from tabulate import tabulate
table = [["Sun","696,000",1.989e30],
         ["Earth","6,371",5.972e24],
         ["Moon","1,737",7.34e22],
         ["Mars","3,390",6.39e23]]
Markdown(tabulate(
  table, 
  headers=["Astronomical object","R (km)", "mass (kg)"]
))
```

Astronomical object

:::
````

In the above example, you can reference the table with `@tbl-planets`, but not the code, which appears inline. If you would also like to be able to refer to the code, you can do so using code chunk options rather than the div syntax, see [Cross-References for Executable Code Blocks](../../docs/authoring/cross-references.llms.md#code-listings) for details.

## Listings

To create a cross-reference to a code listing using div syntax, create a fenced div with an id starting with `lst-`, include the code cell followed by the caption inside the div:

```` markdown
::: {#lst-customers}

```{.sql}
SELECT * FROM Customers
```

Customers Query

:::
````

This also works for executable code cells that produce no output:

```` markdown
::: {#lst-assign}

```{r}
x <- 1
```

Assignment in R

:::
````

However, if any output is produced, it is assumed the output should be the content of the cross-reference, and the code is lifted out and placed inline. For example, the code cell here produces output:

```` markdown
::: {#lst-assign-output}

```{r}
x <- 1
x
```

Assignment in R

:::

@lst-assign-output
````

When rendered the above results in output being the contents of the listing, with the code appearing before the listing:

![Screenshot of a listing cross-reference. A code cell comes first, followed by Listing 1 which contains code output.](images/crossrefs-listing-output.png)

If you need to reference both the code its output, use a combination of a display block and a code block with the code cell option `echo: false`:

```` markdown
::: {#lst-assign-both}

```r
x <- 1
x
```

```{r}
#| echo: false
x <- 1
x
```

Assignment in R

:::
````

When the output is a figure or table, you can reference the code and the output individually by using code cell options, rather than the div syntax, as described in [Cross-References for Executable Code Blocks](../../docs/authoring/cross-references.llms.md#code-listings).

## Diagrams

To create a cross-references to a diagram using div syntax, treat it like a figure. For example, [Figure 4](#fig-simple) is created using:

```` markdown
::: {#fig-simple}

```{dot}
graph {
  A -- B
}
```

This is a simple graphviz graph
:::
````

![](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQ0IiBoZWlnaHQ9IjQ4MCIgdmlld2JveD0iMC4wMCAwLjAwIDYyLjAwIDExNi4wMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgc3R5bGU9IjsgbWF4LXdpZHRoOiBub25lOyBtYXgtaGVpZ2h0OiBub25lIj4KPGcgaWQ9ImdyYXBoMCIgY2xhc3M9ImdyYXBoIiB0cmFuc2Zvcm09InNjYWxlKDEgMSkgcm90YXRlKDApIHRyYW5zbGF0ZSg0IDExMikiPgo8cG9seWdvbiBmaWxsPSJ3aGl0ZSIgc3Ryb2tlPSJ0cmFuc3BhcmVudCIgcG9pbnRzPSItNCw0IC00LC0xMTIgNTgsLTExMiA1OCw0IC00LDQiPjwvcG9seWdvbj4KPCEtLSBBIC0tPgo8ZyBpZD0ibm9kZTEiIGNsYXNzPSJub2RlIj4KPHRpdGxlPkE8L3RpdGxlPgo8ZWxsaXBzZSBmaWxsPSJub25lIiBzdHJva2U9ImJsYWNrIiBjeD0iMjciIGN5PSItOTAiIHJ4PSIyNyIgcnk9IjE4Ij48L2VsbGlwc2U+Cjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjI3IiB5PSItODUuOCIgZm9udC1mYW1pbHk9IlRpbWVzLHNlcmlmIiBmb250LXNpemU9IjE0LjAwIj5BPC90ZXh0Pgo8L2c+CjwhLS0gQiAtLT4KPGcgaWQ9Im5vZGUyIiBjbGFzcz0ibm9kZSI+Cjx0aXRsZT5CPC90aXRsZT4KPGVsbGlwc2UgZmlsbD0ibm9uZSIgc3Ryb2tlPSJibGFjayIgY3g9IjI3IiBjeT0iLTE4IiByeD0iMjciIHJ5PSIxOCI+PC9lbGxpcHNlPgo8dGV4dCB0ZXh0LWFuY2hvcj0ibWlkZGxlIiB4PSIyNyIgeT0iLTEzLjgiIGZvbnQtZmFtaWx5PSJUaW1lcyxzZXJpZiIgZm9udC1zaXplPSIxNC4wMCI+QjwvdGV4dD4KPC9nPgo8IS0tIEEmIzQ1OyYjNDU7QiAtLT4KPGcgaWQ9ImVkZ2UxIiBjbGFzcz0iZWRnZSI+Cjx0aXRsZT5BLS1CPC90aXRsZT4KPHBhdGggZmlsbD0ibm9uZSIgc3Ryb2tlPSJibGFjayIgZD0iTTI3LC03MS43QzI3LC02MC44NSAyNywtNDYuOTIgMjcsLTM2LjEiIC8+CjwvZz4KPC9nPgo8L3N2Zz4=)

Figure 4: This is a simple graphviz graph

If you would rather give diagrams a label and counter distinct from figures, consider defining [Custom Cross-Reference Types](../../docs/authoring/cross-references-custom.llms.md).

## Videos

To add a cross-reference to a video, use the [cross-reference div syntax](../../docs/authoring/cross-references-divs.llms.md) and treat it like a figure. For example,

``` markdown
::: {#fig-cern}

{{< video https://www.youtube.com/embed/wo9vZccmqwc >}}

The video "CERN: The Journey of Discovery"

:::

In @fig-cern...
```

Which renders as:

![Screenshot that shows a YouTube video followed by the caption, 'Figure 1: The video CERN: The Journey of Discovery'. Below the caption is the text 'In Figure 1 ...'.](images/crossrefs-video.png)

If you would rather give videos a label and counter distinct from figures, consider defining [Custom Cross-Reference Types](../../docs/authoring/cross-references-custom.llms.md).

## Subreferences

> **NOTE:**
>
> When your sub-content is either all figures or all tables there is abbreviated syntax, see the Cross References page for [Subfigures](../../docs/authoring/cross-references.llms.md#subfigures) and [Subtables](../../docs/authoring/cross-references.llms.md#subtables) for details.

Cross-reference divs can be nested to create elements with subreferences. For example, the outer div here defines the `fig-subrefs` reference along with the main caption, while the inner divs define `fig-first` and `fig-second` along with their respective captions:

``` markdown
:::: {#fig-subrefs}

::: {#fig-first}

CONTENT 1

First caption
:::

::: {#fig-second}

CONTENT 2

Second caption
:::

Main caption
::::
```

This renders as:

CONTENT 1

\(a\) First caption

CONTENT 2

\(b\) Second caption

Figure 5: Main caption

Both the main element and the sub elements can be referenced directly in the text, e.g. 

``` markdown
@fig-subrefs, @fig-first, @fig-second
```

This renders as: [Figure 5](#fig-subrefs), [Figure 5 (a)](#fig-first), [Figure 5 (b)](#fig-second).

Combined with layout attributes, you can create complex layouts of mixed content where each element can be referenced. For example:

```` markdown
:::: {#fig-complex layout="[[1, 1], [1]]"}

::: {#fig-elephant}

![](images/elephant.jpg)

An image file
:::

::: {#fig-scatterplot}

```{r}
#| echo: false
plot(1:10)
```

A computational figure
:::

::: {#fig-diagram}

```{dot}
//| fig-height: 2
digraph {
  rankdir = "LR";
  Transform -> Visualize
}
```

A diagram
:::

Example figure combining different types of content
::::
````

This renders as:

![A screenshot of a figure layout with two rows. The top row has two columns: on the left an image of an elephant silhouetted against a sunset with the caption (a) An image file; on the right a scatterplot with the caption (b) A computational figure. In the bottom row is a flow chart with a node Transform linked to the node Visualize with the caption (c) A diagram. Below the layout is the caption: Figure 1: Example figure combining different types of content.](images/crossrefs-complex-layout.png)

## Computed Captions

If you want to include computed values in a caption, use the cross-reference div syntax, along with an [inline code expression](../../docs/computations/execution-options.llms.md#inline-code). For example:

## Python

```` markdown
::: {#fig-box}

```{python}
#| echo: false
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5, 10]
p = plt.boxplot(x)
plt.show()
```

This dataset has `{python} len(x)` observations.

:::
````

## R

```` markdown
::: {#fig-box}

```{r}
#| echo: false


x <- c(1, 2, 3, 4, 5, 10)
boxplot(x)

```

This dataset has `{r} length(x)` observations.

:::
````

## Conditional Content

The cross-reference div syntax combined with [conditional content](../../docs/authoring/conditional.llms.md) allows the content of your reference to vary by format. For example, you might want an interactive JavaScript based plot when the format is HTML, but otherwise produce a static plot:

```` markdown

::: {#fig-scatterplot}  
  
:::: {.content-visible when-format="html"}

```{r}
# Code to produce JavaScript based plot
```
::::

:::: {.content-visible unless-format="html"}

```{r}
# Code to produce static plot
```
::::

Scatterplot

:::

@fig-scatterplot
````
