# Quarto Dashboards

## Overview

Quarto Dashboards make it easy to create interactive dashboards using Python, R, Julia, and Observable:

- Publish a group of related data visualizations as a dashboard. Use a wide variety of components including [Plotly](https://plotly.com/python/), [Leaflet](https://ipyleaflet.readthedocs.io/en/latest/), [Jupyter Widgets](../../docs/interactive/widgets/jupyter.llms.md), [htmlwidgets](https://www.htmlwidgets.org/); static graphics (Matplotlib, Seaborn, ggplot2, etc.); tabular data; value boxes; and text annotations.

- Flexible and easy to specify row and column-based [Layouts](../../docs/dashboards/layout.llms.md). Components are intelligently re-sized to fill the browser and adapted for display on mobile devices.

- Author using any notebook editor ([JupyterLab](../../docs/tools/jupyter-lab.llms.md), etc.) or in plain text markdown with any text editor ([VS Code](../../docs/tools/vscode/index.llms.md), [Positron](../../docs/tools/positron/index.llms.md), [RStudio](../../docs/tools/rstudio.llms.md), [Neovim](../../docs/tools/neovim.llms.md), etc.)

- Dashboards can be deployed as static web pages (no special server required) or you can optionally integrate a backend [Shiny Server](../../docs/dashboards/interactivity/shiny-python/index.llms.md) for enhanced interactivity.

## Examples

You can create highly customized layouts and use a wide variety of dashboard themes as illustrated in these examples (click to see them in more detail):

[![Screenshot of a Stock Trader dashboard: a row of three values boxes, then a row with a stock ticker graph and a table of closing values. Navy blue and green theme.](../../docs/dashboards/examples/thumbnails/stock-explorer-dashboard.png)](../../docs/dashboards/examples/thumbnails/stock-explorer-dashboard.png)

[![Screenshot of a Customer Churn dashboard: a row of three values boxes, then a row with two plots, then a row with a table. Light blue and yellow theme.](../../docs/dashboards/examples/thumbnails/customer-churn-dashboard.png)](../../docs/dashboards/examples/thumbnails/customer-churn-dashboard.png)

[![Screenshot of a Palmer Penguins dashboard: a sidebar with checkboxes and a dropdown, and two plots in main panel. Blue theme.](../../docs/dashboards/examples/thumbnails/penguins-dashboard.png)](../../docs/dashboards/examples/thumbnails/penguins-dashboard.png)

For live versions of these dashboards, source code, and additional examples see the [dashboard section of the gallery](../../docs/gallery/index.llms.md#dashboards).

## Walkthrough

Here we’ll walk through a simple example to illustrate the basics. Then, we’ll provide detailed instructions on how to get started with building your own dashboards.

This simple single-page Python dashboard uses interactive Plotly visualizations to explore development indicators in the [Gapminder](http://www.gapminder.org/data/) dataset. The dashboard includes two rows, the second of which includes two columns:

[![Screenshot of a Development Indicators dashboard: a row titled GDP and Life Expectancy with a single plot, then a row with two plots arranged side by side titled Population and Life Expectancy.](images/gapminder.png)](images/gapminder.png)

Dashboards consist of several components:

1.  **Navigation Bar** — Icon, title, and author along with links to sub-pages (if more than one page is defined).

2.  **Pages, Rows, Columns, and Tabsets** — Pages, rows and columns are defined using markdown headings (with optional attributes to control height, width, etc.). Tabsets can be used to further divide content within a row or column.

3.  **Cards, Sidebars, and Toolbars** — Cards are containers for plots, data display, and free form content. The content of cards typically maps to *cells* in your notebook or source document. Sidebars and toolbars are used to present inputs within interactive dashboards.

Dashboards can be created either using Jupyter notebooks (`.ipynb`) or using plain text markdown (`.qmd`). Here is the code for the notebook version of the above example (click the image for a zoomed view):

[![Screenshot of a gapminder-notebook.ipynb open in Jupyter Lab. After cells for Quarto settings and python setup, there is a markdown cell containing the heading Row, followed by a python code cell generating a plot. Then another markdown cell containing the heading Row, followed by two python code cells each generating a plot.](images/gapminder-jupyter.png)](images/gapminder-jupyter.png)

Here is the plain text `.qmd` version of the dashboard (click on the numbers on the far right for additional explanation of syntax and mechanics):

```` python
--- 
title: "Development Indicators by Continent" # <1>
author: "Gapminder Analytics Group" # <1>
format: dashboard # <1>
--- 

```{{python}}
import plotly.express as px
df = px.data.gapminder()
```

## Row {height=60%} # <2>

```{{python}}  # <3>
#| title: GDP and Life Expectancy 
px.scatter(  
  df, x="gdpPercap", y="lifeExp", 
  animation_frame="year", animation_group="country", 
  size="pop", color="continent", hover_name="country",
  facet_col="continent", log_x=True, size_max=45, 
  range_x=[100,100000], range_y=[25,90] 
)  
``` # <3>

## Row {height=40%}

```{{python}} # <4>
#| title: Population
px.area(
  df, x="year", y="pop", 
  color="continent", line_group="country"
)
```

```{{python}}
#| title: Life Expectancy
px.line(
  df, x="year", y="lifeExp", 
  color="continent", line_group="country"
)
``` # <4>
````

1.  The document options define the `title` and `author` for the navigation bar as well as specifying the use of the `dashboard` format.
2.  Rows and columns are defined using headings. In this example we define two rows and specify their relative sizes using the `height` option.
3.  Computational cells become cards that live within rows or columns. Cards can have an optional title (which here we specify using the `title` option).
4.  The second row includes two computational cells, which are automatically split into two side by side cards.

## Getting Started

### Step 1: Install Quarto

Dashboards are a feature in the Quarto v1.4. Before you get started, make sure you install the **latest release** version of Quarto.

[\_](_ "Download Quarto") Find your operating system in the table below

### Highlights

Quarto 1.8 includes the following new features:

- Improvements to brand support:

  - [Light and dark colors](../../docs/authoring/brand.llms.md#light-and-dark-colors): Specify `light` and `dark` for any color in a brand specification.
  - [Light and dark logos](../../docs/authoring/brand.llms.md#light-and-dark-logos): Specify `light` and `dark` versions of logos in a brand specification.
  - [Brand extensions](../../docs/extensions/brand.llms.md): Share brand definitions and assets across Quarto projects.
  - [Dark brand for `format: revealjs`](../../docs/authoring/brand.llms.md#brand-mode): Specify `brand-mode: dark` to apply your dark brand to your presentation.

- [HTML Accessibility Checks](../../docs/output-formats/html-accessibility.llms.md): Add the `axe` option to HTML formats to perform accessibility checks with the [Axe-core engine](https://github.com/dequelabs/axe-core).

- [Access execution settings from code cells](../../docs/advanced/quarto-execute-info.llms.md): Read the `QUARTO_EXECUTE_INFO` environment variable to access information about execution context.

- Access [metadata](../../docs/extensions/lua-api.llms.md#metadata-access) and [variables](../../docs/extensions/lua-api.llms.md#variables-access) in filters and shortcodes: Use the new `quarto.variables.get()` and `quarto.metadata.get()` APIs.

- The default LaTeX engine is now `lualatex`.

Dependency updates:

- `mermaidjs` updated to 11.6.0.
- Bootstrap icons updated to v1.13.1
- `QuartoNotebookRunner` in `julia` engine updated to 0.17.3

### Release Notes

You can find release notes and installers for all platforms in the [download page](../../docs/download/prerelease.llms.md).

### Step 2: Learn the Basics

Start by learning how to lay out your dashboard and populate it with content:

[Dashboard Layout](../../docs/dashboards/layout.llms.md) shows you how to control the navigation bar, and how to arrange your content across pages, rows, columns, tabsets, and cards.

[Data Display](../../docs/dashboards/data-display.llms.md) shows you how to display data in your dashboard as plots, tables, value boxes, and text.

### Step 3: Explore Further

Once you’ve mastered the basics, check out these additional articles to learn more.

[Examples](../../docs/gallery/index.llms.md#dashboards) provides a gallery of example dashboards you can use as inspiration for your own.

[Inputs](../../docs/dashboards/inputs.llms.md) demonstrates various ways to layout inputs for interactive dashboards (sidebars, toolbars, attaching inputs directly to cards, etc.)

[Theming](../../docs/dashboards/theming.llms.md) describes the various way to customize the fonts, colors, layout and other aspects of dashboard appearance.

[Parameters](../../docs/dashboards/parameters.llms.md) explains how to create dashboard variants by defining parameters and providing distinct values for them on the command line.

[Deployment](../../docs/dashboards/deployment.llms.md) covers how to deploy both static dashboards (which require only a web host, but not a server) and Shiny dashboards (which require a Shiny Server).

[Interactivity](../../docs/dashboards/interactivity/index.llms.md) explores the various ways to create interactive dashboards that enable more flexible data exploration.
