# Interactive Dashboards

## Overview

Adding interactivity to a dashboard helps users explore the concepts and data you are presenting more deeply. There are several ways to add interactive components to Quarto dashboards:

- [Shiny for Python](../../../docs/dashboards/interactivity/shiny-python/index.llms.md) for dashboards that use Jupyter for computations (requires a server component for deployment).

- [Shiny for R](../../../docs/dashboards/interactivity/shiny-r.llms.md) for dashboards that use Knitr for computations (requires a server component for deployment).

- [Observable JS](../../../docs/dashboards/interactivity/observable.llms.md) for client-side interactivity using the Observable dialect of JavaScript.

- [Jupyter Widgets](../../../docs/interactive/widgets/jupyter.llms.md) or [htmlwidgets](../../../docs/interactive/widgets/htmlwidgets.llms.md) for client-side interactivity based on standard Python and R JavaScript widget frameworks.

> **NOTE:**
>
> Using Shiny-based interactivity is generally much more flexible and capable than client-only interactivity, however requires a server for deployment.

## Input Layout

No matter which type of interactivity you choose, you’ll want to present user inputs in a clear, accessible fashion. While you can locate inputs anywhere within a dashboard, there are some special containers that are tuned for this purpose:

- [Sidebars](../../../docs/dashboards/inputs.llms.md#sidebars) provide a collapsible, full height panel for inputs.

- [Toolbars](../../../docs/dashboards/inputs.llms.md#toolbars) provide a full page width horizontal panel for inputs.

- [Card Inputs](../../../docs/dashboards/inputs.llms.md#card-inputs) are directly embedded in the cards either as a card toolbar or as a card sidebar.

The article on [Inputs](../../../docs/dashboards/inputs.llms.md) covers these methods in depth along with tips on doing more sophisticated layout of groups of inputs.
