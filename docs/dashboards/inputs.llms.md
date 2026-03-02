# Dashboard Input Layout

## Overview

There are several ways to layout inputs within interactive dashboards:

- [Sidebars](#sidebars) provide a collapsible vertical panel for inputs.

- [Toolbars](#toolbars) provide a horizontal panel for inputs.

- [Card Inputs](#card-inputs) provide a panel for card-specific inputs.

These techniques all create regions for inputs with a special background color to distinguish them from ordinary content. You can also locate inputs anywhere else you wish within a dashboard (i.e. in a standard card).

## Sidebars

Sidebars are a great place to group inputs for dashboards. To include a sidebar, add the `.sidebar` class to a level 2 heading. For example:

```` python
---
title: "Sidebar"
format: dashboard
server: shiny
---
    
## {.sidebar}

```{python}
```

## Column 

```{python}
```

```{python}
```
````

Here’s how a sidebar would appear (note there is a button in the top right that enables the user to optionally close the sidebar):

![A screenshot of a Penguin Bills dashboard. A sidebar on the left contains two dropdown menus, one for Variable and one for Distribution and a checkbox to show rugmarks. On the right there are two plots: a histogram of bill_length_mm colored by species and a histogram of bill_depth_mm colored by species.](../../docs/dashboards/images/sidebar.png)

### Global Sidebar

If you have a dashboard with [multiple pages](../../docs/dashboards/layout.llms.md#pages), you may want the sidebar to be global (i.e. visible across all pages). To do this, add the `.sidebar` class to a level 1 heading:

```` python
---
title: "Sidebar"
format: dashboard
---
    
# {.sidebar}

Sidebar content

# Plots

```{python}
```

# Data

```{python}
```
````

### Inline Sidebar

While sidebars are often laid out at the page level (i.e. spanning the dashboard from top to bottom) you can actually include them anywhere within a layout. For example, here we have a sidebar that is within a row (rather than spanning all rows):

```` python
---
title: "Palmer Penguins"
format: dashboard
server: shiny
---

## Row

### {.sidebar}

```{python}
```

### Column

```{python}
```

## Row

```{python}
```
````

![A screenshot of a Penguin Bills dashboard. A sidebar on the left side of the top row contains two dropdown menus, one for Variable and one for Distribution and a checkbox to show rugmarks. On the right there is a histogram of bill_length_mm colored by species. In the second row there is a table displaying the raw penguins data.](../../docs/dashboards/images/inline-sidebar.png)

### Location and Size

Sidebars can be located on either the left or right side. Layout a sidebar on the right by including it *after* the column(s) it is adjacent to. You can also modify the size of sidebars using the `width` attribute. This example demonstrates both of these techniques:

```` python
---
title: "Sidebar"
format: dashboard
server: shiny
---
    
## Column 

```{python}
```

```{python}
```

## {.sidebar width="300px"}

```{python}
```
````

![A screenshot of a Penguin Bills dashboard. A sidebar on the right contains two dropdown menus, one for Variable and one for Distribution and a checkbox to show rugmarks. On the left there are two plots: a histogram of bill_length_mm colored by species and a histogram of bill_depth_mm colored by species.](../../docs/dashboards/images/sidebar-right.png)

## Toolbars

Toolbars are similar to sidebars, but provide a horizontal layout. Create a toolbar by adding the `.toolbar` class to a level 2 row heading. For example:

```` python
---
title: "Toolbar"
format: dashboard
server: shiny
---
    
## {.toolbar}
    
```{python}
```

## Row

```{python}
```
````

![](../../docs/dashboards/images/toolbar.png)

### Global Toolbar

If you have a dashboard with [multiple pages](../../docs/dashboards/layout.llms.md#pages), you may want the toolbar to be global (i.e. visible across all pages). To do this, add the `.toolbar` class to a level 1 heading:

```` python
---
title: "Toolbar"
format: dashboard
server: shiny
---
    
# {.toolbar}

Toolbar content

# Page 1 

```{python}
```

# Page 2

```{python}
```
````

### Inline Toolbar

While toolbars are often laid out at the page level (i.e. spanning the dashboard from left to right) you can actually include them anywhere within a layout. For example, here we have a toolbar that is within a column (rather than spanning all columns):

```` python
---
title: "Palmer Penguins"
format: 
  dashboard:
    orientation: columns
server: shiny
---

## Column 

### {.toolbar}

```{python}
```

### Row

```{python}
```

## Column

```{python}
```
````

![](../../docs/dashboards/images/toolbar-inline.png)

### Location

Toolbars can be located on either the top or bottom of content. Layout a toolbar on the bottom by including it *after* the rows(s) it is adjacent to. For example:

```` python
---
title: "Penguin Bills"
format: dashboard
server: shiny
---

## Row

```{python}
```

## {.toolbar}

```{python}
```
````

![](../../docs/dashboards/images/toolbar-bottom.png)

## Card Inputs

In some cases you may want to connect inputs more directly to a single output. You can do this using either a card toolbar or card sidebar.

### Card Toolbars

To add a toolbar to a card, define it immediately above or below the cell that generates the output. You can do this by either adding the `content: card-toolbar` option to a cell or by creating a div with the `.card-toolbar` class. For example:

```` python
```{python}
#| content: card-toolbar

```

```{python}
#| title: Penguin Bills

```
````

![A screenshot of a Penguin Bills card. The card toolbar contains two dropdown menus, one for Variable and one for Distribution and a checkbox to show rugmarks. Below, a plot shows a histogram of bill_length_mm colored by species.](../../docs/dashboards/images/card-toolbar.png)

Note that the `title` attribute is optional for cells with toolbars (if there is no `title` then the inputs will be left rather than right aligned).

### Card Sidebars

To add a sidebar to a card, define it immediately to the left or the right of the cell that generates the output. You can do this either by adding the `content: card-sidebar` option to a cell or by creating a div with the `.card-sidebar` class. For example:

```` python
```{python}
#| content: card-sidebar

```

```{python}
#| title: Penguin Bills

```
````

![A screenshot of a Penguin Bills card. The card sidebar on the left contains two dropdown menus, one for Variable and one for Distribution and a checkbox to show rugmarks. To the right, a plot shows a histogram of bill_length_mm colored by species.](../../docs/dashboards/images/card-sidebar.png)
