# htmlwidgets for R

## Overview

The [htmlwidgets](http://www.htmlwidgets.org) package enables you to use JavaScript visualization libraries like [Leaflet](http://rstudio.github.io/leaflet/), [Plotly](https://plot.ly/r/), [dygraphs](http://rstudio.github.io/dygraphs/), and [threejs](https://bwlewis.github.io/rthreejs/) directly from R.

If you are using the Knitr engine with Quarto this is a great way to incorporate interactivity without learning JavaScript or requiring a Shiny Server to view your document.

## Usage

Including htmlwidgets within a Quarto document is as easy as including an R plot. For example, here is how we embed a [Leaflet](http://rstudio.github.io/leaflet/) map:

```` markdown
```{r}
library(leaflet)
leaflet() %>%
  addTiles() %>%  # Add default OpenStreetMap map tiles
  addMarkers(lng=174.768, lat=-36.852, popup="The birthplace of R")
```
````

    Warning: package 'leaflet' was built under R version 4.1.2

## Layout

You can also use `layout` options with htmlwidgets. For example, here we provide a custom `layout` to arrange three [dygraph](http://rstudio.github.io/dygraphs/) time series plots:

```` markdown
```{r}
#| layout: [[1,1], [1]]
library(dygraphs)
dygraph(fdeaths, "Female Deaths")
dygraph(mdeaths, "Male Deaths")
dygraph(ldeaths, "All Deaths")
```
````

See the article on [Figures](../../../docs/authoring/figures.llms.md#custom-layouts) for additional documentation on custom layouts.

To learn about available htmlwidgets see the [showcase page](http://www.htmlwidgets.org/showcase_leaflet.llms.md) and the [htmlwidget gallery](http://gallery.htmlwidgets.org/).
