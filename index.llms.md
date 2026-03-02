# Welcome to Quarto^(​®)

### An open-source scientific and technical publishing system

- Author using [Jupyter](https://jupyter.org) notebooks or with plain text markdown in your favorite editor.
- Create dynamic content with [Python](docs/computations/python.llms.md), [R](docs/computations/r.llms.md), [Julia](docs/computations/julia.llms.md), and [Observable](docs/computations/ojs.llms.md).
- Publish reproducible, production quality articles, presentations, dashboards, websites, blogs, and books in HTML, PDF, MS Word, ePub, and more.
- Share knowledge and insights organization-wide by publishing to [Posit Connect](docs/publishing/rstudio-connect.llms.md), [Confluence](docs/publishing/confluence.llms.md), or other publishing systems.
- Write using [Pandoc](https://pandoc.org) markdown, including equations, citations, crossrefs, figure panels, callouts, advanced layout, and more.

### Analyze. Share. Reproduce. You have a story to tell with data—tell it with Quarto.

[Get Started](docs/get-started/index.llms.md)

[Guide](./docs/guide/)

# Hello, Quarto

- Python
- R
- Julia
- Observable

Combine Jupyter notebooks with flexible options to produce production quality output in a wide variety of formats. Author using traditional notebook UIs or with a plain text markdown representation of notebooks.

![Example Jupyter notebook entitled Palmer Penguins with code cells, text, and a scatterplot.](images/demo-jupyter-plain.png)

![Output of example Jupyter notebook, Palmer Penguins, in HTML showing title, metadata, text, code, and scatterplot. At the top there is a dropdown option to show or hide the code.](images/demo-jupyter-output.png)

Quarto is a multi-language, next generation version of R Markdown from Posit, with many new features and capabilities. Like R Markdown, Quarto uses [knitr](https://yihui.org/knitr/) to execute R code, and is therefore able to render most existing Rmd files without modification.

```` markdown
---
title: "ggplot2 demo"
author: "Norah Jones"
date: "5/22/2021"
format: 
  html:
    fig-width: 8
    fig-height: 4
    code-fold: true
---

## Air Quality

@fig-airquality further explores the impact of temperature on ozone level.

```{r}
#| label: fig-airquality
#| fig-cap: "Temperature and ozone level."
#| warning: false

library(ggplot2)
ggplot(airquality, aes(Temp, Ozone)) + 
  geom_point() + 
  geom_smooth(method = "loess")
```
````

![Example output with title (ggplot2 demo), author (Norah Jones), and date (5/22/2021). Below is a header reading Air Quality followed by body text (Figure 1 further explores the impact of temperature on ozone level.) with a toggleable code field, and figure with caption Figure 1 Temperature and ozone level.](images/hello-knitr.png)

Combine markdown and Julia code to create dynamic documents that are fully reproducible. Quarto executes Julia code either via the [`julia` engine](#using-the-julia-engine) using [QuartoNotebookRunner.jl](https://github.com/PumasAI/QuartoNotebookRunner.jl/) or via the [`jupyter` engine](#using-the-jupyter-engine) using the [IJulia](https://github.com/JuliaLang/IJulia.jl) Jupyter kernel, enabling you to author in plain text (as shown below) or render existing Jupyter notebooks.

```` markdown
---
title: "Plots Demo"
author: "Norah Jones"
date: "5/22/2021"
format:
  html:
    code-fold: true
engine: julia
---

## Parametric Plots

Plot function pair (x(u), y(u)). 
See @fig-parametric for an example.

```{julia}
#| label: fig-parametric
#| fig-cap: "Parametric Plots"

using Plots

plot(sin, 
     x->sin(2x), 
     0, 
     2π, 
     leg=false, 
     fill=(0,:lavender))
```
````

![Example Plots Demo output with title, author, date published and main section on Parametric plots which contains text, a toggleable code field, and the output of the plot, with the caption Figure 1 Parametric Plots.](images/hello-julia.png)

Quarto includes native support for Observable JS, a set of JavaScript enhancements created by Mike Bostock (the author of D3). Observable JS uses a reactive execution model, and is especially well suited for interactive data exploration and analysis.

```` markdown
---
title: "observable plot"
author: "Norah Jones"
format: 
  html: 
    code-fold: true
---

## Seattle Precipitation by Day (2012 to 2016)

```{ojs}
data = FileAttachment("seattle-weather.csv")
  .csv({typed: true})
  
Plot.plot({
  width: 800, height: 500, padding: 0,
  color: { scheme: "blues", type: "sqrt"},
  y: { tickFormat: i => "JFMAMJJASOND"[i] },
  marks: [
    Plot.cell(data, Plot.group({fill: "mean"}, {
      x: d => new Date(d.date).getDate(),
      y: d => new Date(d.date).getMonth(),
      fill: "precipitation", 
      inset: 0.5
    }))
  ]
})
```
````

![Example output with title, author, and date. Below, the main section reads Seattle Precipitation by Day (2012 to 2016) with a toggleable section to show code and a heatmap of the precipitation by day.](images/hello-observable.png)

### Dynamic Documents

Generate dynamic output using Python, R, Julia, and Observable. Create reproducible documents that can be regenerated when underlying assumptions or data change.

[Learn more »](docs/computations/python.llms.md)

### Beautiful Publications

Publish high-quality articles, reports, presentations, websites, and books in HTML, PDF, MS Word, ePub, and more. Use a single source document to target multiple formats.

[Learn more »](docs/output-formats/all-formats.llms.md)

### Scientific Markdown

Pandoc markdown has excellent support for LaTeX equations and citations. Quarto adds extensions for cross-references, figure panels, callouts, advanced page layout, and more.

[Learn more »](docs/authoring/markdown-basics.llms.md)

### Authoring Tools

Use your favorite tools including Positron, VS Code, RStudio, Jupyter Lab, or any text editor. Use the Quarto visual markdown editor for long-form documents.

[Learn more »](docs/get-started/index.llms.md)

### Interactivity

Engage readers by adding interactive data exploration to your documents using Jupyter Widgets, htmlwidgets for R, Observable JS, and Shiny.

[Learn more »](./docs/interactive/)

### Websites and Books

Publish collections of documents as a blog or full website. Create books and manuscripts in both print formats (PDF and MS Word) and online formats (HTML and ePub).

[Learn more »](./docs/websites/)

[Get Started](docs/get-started/index.llms.md)
