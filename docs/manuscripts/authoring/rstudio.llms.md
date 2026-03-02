# Authoring Manuscripts

- [![](../images/jupyter-logo.png)Jupyter](jupyterlab.llms.md)
- [![](../images/vscode-logo.png)VS Code](vscode.llms.md)
- [![](../images/rstudio-logo.png)RStudio](rstudio.llms.md)

## Overview

On this page, we’ll show you how to author an academic manuscript with Quarto in RStudio. You’ll learn how to:

- Preview your manuscript using RStudio.

- Add scholarly front matter to describe your article.

- Add figures, tables, cross references, and citations with Quarto-specific markdown.

- Include output from computations using inline code or embedded from external notebooks.

The syntax you’ll learn will apply regardless of the tool you are using to edit notebooks. And although we’ll use R code examples, you could use Python or Julia instead.

> **CAUTION:**
>
> You’ll see us refer to Quarto documents (`.qmd`) as notebooks throughout this tutorial. In fact, we’ll use the term “notebook” interchangeably to refer to a Quarto document (`.qmd`) or a Jupyter Notebook (`.ipynb`). Although there are implementation differences these formats are both designed to combine code and narrative - a feature that is central to being a computational notebook.
>
> When Quarto prepares your manuscript for publication, both as website and a submission archive, your Quarto `.qmd` documents and their outputs will be made available as Jupyter notebooks. Jupyter Notebooks have the advantage that computational outputs are included in the notebook file - allowing a record of both your code and its results to travel through the publication process and become part of your manuscript’s document of record.

### Is this tutorial for me?

We will assume you:

- are comfortable using RStudio to open and edit files,
- have a GitHub account, and are comfortable cloning a repo to your computer,
- are comfortable navigating your file system, and executing commands in a Terminal.

## Setup

To follow along, you’ll need to clone the template repository.

> **IMPORTANT:**
>
> If you haven’t already, make sure you’ve installed the latest release version of Quarto, as described in the [Manuscript Overview](../../../docs/manuscripts/index.llms.md#install).

### Clone the Template Repository

To follow this tutorial you’ll need your own copy of the [template repository](https://github.com/quarto-ext/manuscript-template-rstudio), including all of its branches.

1.  Head to [GitHub to create a new repository from the template](https://github.com/quarto-ext/manuscript-template-rstudio/generate).

    Provide a **Repository Name** and make sure you check **Include all branches**. Then **Create repository from template**. ![Screenshot of GitHub's create a new repo from a template page. Repository name has been filled with manuscript-template, and the box labelled Include all branches is checked.](images/github-create-from-template.png)

2.  Once your repository is created, clone it to your local computer.

    You can do this any way you are comfortable, but one approach is to use **File** \> **New Project**. In the **New Project** dialog, select **From Version Control**, then **Git**, and copy and paste the repo URL from GitHub.

![Screenshot of the RStudio IDE with a project called manuscript-template-rstudio-test open. The File pane shows the folders: \_extensions, \_freeze, .github, images, and notebooks; and the files: \_quarto.yml, .gitignore, index.ipynb, README.md and references.bib.](images/rstudio-open.png)

Template manuscript open in RStudio

## Project Files

At its simplest, a Quarto manuscript project has two files:

- A notebook file where you write your article: `index.qmd`. This file contains:
  - document metadata, including article front matter (authors, affiliations, etc.) and Quarto options,
  - the article body, written using special Quarto markdown syntax that allows you to add things like cross references and citations, and
  - optionally, code, where you control if, or how, the code and its output appear in the article.
- A configuration file `_quarto.yml` that identifies the project as a Quarto manuscript and controls how your manuscript is put together.

This particular manuscript project includes some other files and folders, you’ll learn about these files as you work through this tutorial.

## Workflow

The basic workflow for writing a manuscript in Quarto is to make changes to your article content in `index.qmd`, preview the changes with Quarto, and repeat. Let’s try it out.

Open `index.qmd`.

Render and preview the manuscript by hitting the **Render** button located in the menu bar of the editor:

![Screenshot of the source editor menu bar with the Render button highlighted.](images/rstudio-render-button.png)

You’ll see some output from Quarto in the Background Jobs pane and then a live preview will appear in the Viewer pane.

![Screenshot of the RStudio IDE. Open in the Source pane is a file called index.qmd. In the Viewer pane, a website starting with the header La Palma Earthquakes.](images/rstudio-preview.png)

You’ll dive into the details of this `index.qmd` next, but for now let’s make a change and see what happens.

Find the line:

``` yaml
title: La Palma Earthquakes
```

Change the line to:

``` yaml
title: La Palma Earthquake Mechanisms
```

Save the notebook, re-render, and you’ll see the preview update.

![Screenshot of the RStudio IDE. Open in the Source pane is a file called index.qmd with the text, title: La Palma Earthquake Mechanisms. In the Viewer pane is an article webpage with the title La Palma Earthquake Mechanisms.](images/rstudio-edit.png)

## Visual Editor

The RStudio visual editor provides a [WYSIWYM](https://en.wikipedia.org/wiki/WYSIWYM) editing interface for Quarto notebooks. Some tasks, like adding citations, or creating tables, are easier in the visual editor - we’ll point these out as we introduce them.

![Screenshot of the file \`index.qmd\` open in the Source Editor. File shows line numbers and the raw markdown for inserting a figure and table.](images/source-editor-rstudio.png)

Source Editor

![Screenshot of the file \`index.qmd\` open in the Visual Editor. File shows a figure and table.](images/visual-editor-rstudio.png)

Visual Editor

To toggle between source and visual editor modes, toggle the “Source” and “Visual” menu items at the top of the Source Editor window, or use the keyboard shortcut .

![Screenshot of the Source Editor pane in RStudio. The Visual button in the toolbar at the top of the Editor pane is highlighted.](images/source-visual-buttons-rstudio.png)

You can read more about RStudio’s visual editor at [Visual Editing in RStudio](../../../docs/visual-editor/index.llms.md).

You can switch between the source and visual editor at any time - the location of your cursor and undo/redo history is preserved.

## Notebook Structure

The file `index.qmd` is a Quarto markdown file. It contains three types of content:

- It starts with a YAML header that is used to set document metadata, including scholarly front matter. The YAML header starts and ends with a line of three dashes (`---`), and within these lines, content is parsed as YAML.

- It may include executable code chunks which start with three backticks followed by the code language in curly braces (e.g. ```` ```{r} ```` or ```` ```{python} ````). These code chunks may include Quarto comments at the top which start with `#|`. These comments set Quarto options that control how the code and its output appear in the article.

- The rest of the document is interpreted as Quarto specific markdown, which allows you to include things like figures, tables, equations, cross references and citations.

The rest of this page walks you through this article from top to bottom, introducing you to the Quarto features you’ll most likely need to write a scholarly article.

## Front Matter

The YAML header consists of key-value pairs set using the syntax `key: value`. The header is often extensive for articles because it is used to specify much of the scholarly front matter, like the authors and their affiliations, and the abstract.

> **TIP:**
>
> ``` yaml
> title: La Palma Earthquakes
> author:
>   - name: Steve Purves
>     orcid: 0000-0002-0760-5497
>     corresponding: true
>     email: steve@curvenote.com
>     roles:
>       - Investigation
>       - Project administration
>       - Software
>       - Visualization
>     affiliations:
>       - Curvenote
>   - name: Rowan Cockett
>     orcid: 0000-0002-7859-8394
>     corresponding: false
>     roles: []
>     affiliations:
>       - Curvenote
> keywords:
>   - La Palma
>   - Earthquakes
> abstract: |
>   In September 2021, a significant jump in seismic activity on the island of La Palma (Canary Islands, Spain) signaled the start of a volcanic crisis that still continues at the time of writing. Earthquake data is continually collected and published by the Instituto Geográphico Nacional (IGN). ...
> plain-language-summary: |
>   Earthquake data for the island of La Palma from the September 2021 eruption is found ...
> key-points:
>   - A web scraping script was developed to pull data from the Instituto Geogràphico Nacional into a machine-readable form for analysis
>   - Earthquake events on La Palma are consistent with the presence of both mantle and crustal reservoirs.
> date: last-modified
> bibliography: references.bib
> citation:
>   container-title: Earth and Space Science
> number-sections: true
> ```

For example, at the top level the header in `index.qmd` sets the following keys: `title`, `author`, `keywords`, `abstract`, `plain-language-summary`, `key-points`, `date`, `bibliography`, `citation`, and `number-sections`.

You’ve seen how editing the `title` key updated the title of the article on the manuscript webpage. The `title` key is also used by the PDF and Word formats, but not all of the keys are used in all formats.

You can read more about setting the front matter for your article in [Scholarly Front Matter](../../../docs/authoring/front-matter.llms.md).

## Markdown

Markdown cells in the document will be processed by Quarto’s specific markdown syntax. Quarto’s markdown syntax is based on [Pandoc Markdown](https://pandoc.org/MANUAL.llms.md#pandocs-markdown), which in turn is based on John Gruber’s [Markdown](https://daringfireball.net/projects/markdown/).

As an example, the markdown to create the heading for the article’s introduction is:

``` markdown
## Introduction
```

First-level headings are reserved for the article title, so you’ll use second-level and deeper headings to structure the sections in your article.

If Markdown syntax is unfamiliar, you might want to read about Quarto [Markdown Basics](../../../docs/authoring/markdown-basics.llms.md).

## Computations

> **TIP:**
>
> This section uses R code examples, but Quarto also supports Python, Julia and Observable.

Your article can include executable code. By default, code itself will not display in the article, but any output including tables and figures will. When you include code in your article, you’ll also get an additional link to the “Article Notebook” under Notebooks on the manuscript webpage. This is a rendered version of your article notebook that includes the code.

For example, `index.qmd`, includes:

``` r
eruptions <- c(1492, 1585, 1646, 1677, 1712, 1949, 1971, 2021)
n_eruptions <- length(eruptions)
```

This code doesn’t appear in the rendered article, but does in the “Article Notebook”.

![Screenshot of the rendered article with a section starting with 'Let x denote'. No code is visible.](images/code-webpage.png)

Rendered Article

![Screenshot of the Article Notebook with a section starting with 'Let x denote'. Code is visible in two blocks. The first block starts 'eruptions \<-'](images/code-article-notebook-r.png)

Article Notebook

You can add Quarto options to code cells by adding a `#|` comment to the top, followed by the option in YAML syntax. For example, adding the `echo` option with the value `true` would look like this:

```` markdown
```{r}
#| echo: true
eruptions <- c(1492, 1585, 1646, 1677, 1712, 1949, 1971, 2021)
n_eruptions <- length(eruptions)
```
````

The `echo` option describes whether the code is included in the rendered article. If you make this change and save `index.qmd`, you’ll see this code now appears in the article.

You can find a list of all the code cell options available on the [Knitr Code Cell](../../../docs/reference/cells/cells-knitr.llms.md) reference page.

The next code cell creates a figure:

```` markdown
```{r}
#| label: fig-timeline
#| fig-cap: Timeline of recent earthquakes on La Palma
#| fig-alt: An event plot of the years of the last 8 eruptions on La Palma.
#| fig-height: 1.5
#| fig-width: 6
par(mar = c(3, 1, 1, 1) + 0.1)
plot(
  eruptions, rep(0, n_eruptions), 
  pch = "|", axes = FALSE
)
axis(1)
box()
```
````

The `label` option is used to add an identifier to code cell and its output, for example to allow cross referencing. The prefix `fig-` is required for figure cross references, but the suffix, in this case `timeline`, is up to you. You’ll learn more about [Cross References](#cross-ref) below.

The option `fig-cap` provides the caption text displayed below the figure in the manuscript, and `fig-alt` provides alt text for the figure, helping your manuscript webpage to meet accessibility guidelines.

Computations are also a good way to include tables based on data. You can read more about doing this in the Quarto documentation on [Tables from Computations](../../../docs/authoring/tables.llms.md#computations).

If you have code output you don’t want to include in your article you can use `output: false`. For example, you may have a value that is helpful for writing your content, but you don’t want it to appear in the article itself. The next code cell is an example:

```` markdown
```{r}
#| output: false
avg_years_between_eruptions <- mean(diff(eruptions[-n_eruptions]))
avg_years_between_eruptions
```
````

If you are viewing the rendered “Article Notebook”, you’ll see the value of `avg_years_between_eruptions` displayed below this code, but the value does not appear in the rendered article.

If you’d like to exclude a cell and its output from both the article and the rendered notebook, you could use `include: false` instead:

```` markdown
```{r}
#| include: false
avg_years_between_eruptions <- mean(diff(eruptions[-n_eruptions]))
avg_years_between_eruptions
```
````

You can use computed values directly in your article text using the syntax `` `{r} expr` ``. For example, consider this line in `index.qmd`:

``` markdown
Based on data up to and including 1971, eruptions on La Palma happen every `{r} round(avg_years_between_eruptions, 1)` years on average.
```

When rendered, it displays as:

> Based on data up to and including 1971, eruptions on La Palma happen every 79.8 years on average.

You can read more about using code inline at [Inline Code](../../../docs/computations/execution-options.llms.md#inline-code).

Rather than including computations directly in your article you can also embed outputs from other notebooks, read more below in [Embedding Notebooks](#embed).

### When is code executed?

By default, Quarto will execute code in a `.qmd` notebook during the rendering process. This means, as you edit `index.qmd` you may notice messages that indicate code is being run.

This manuscript template uses Quarto’s freeze feature, which allows us to avoid having to set up a computational environment on GitHub during the publishing process. Freeze saves the rendered versions of notebooks so that they are not re-rendered, and consequently, the code is not re-evaluated unless their source changes.

You may not have noticed, but the first time you rendered the manuscript no code was evaluated. This was because the template repo included the `_freeze/` folder, and the contents of `index.qmd` had not changed since the freeze was generated. As you change `index.qmd`, code will be re-evaluated, and the contents of `_freeze/` will be updated. Remember when you come to publish, you’ll need to commit the changes in `_freeze/` as well.

## Citations

> **TIP:**
>
> This section describes adding citations in the text of your article. The citation for your own article that is displayed at the bottom of the article webpage is controlled using [Front Matter](#front-matter).

To add citations you need a bibliography file, `.bib`, containing the citation data. You can specify this file in the document YAML with the `bibliography` option. For example, the citation data for `index.qmd` is stored in `references.bib`:

``` yaml
bibliography: references.bib
```

The file `references.bib` contains only one citation:

``` bib
@article{marrero2019,
  author = {Marrero, Jos{\' e} and Garc{\' i}a, Alicia and Berrocoso, Manuel and Llinares, {\' A}ngeles and Rodr{\' i}guez-Losada, Antonio and Ortiz, R.},
  journal = {Journal of Applied Volcanology},
  year = {2019},
  month = {7},
  pages = {},
  title = {Strategies for the development of volcanic hazard maps in monogenetic volcanic fields: the example of {La} {Palma} ({Canary} {Islands})},
  volume = {8},
  doi = {10.1186/s13617-019-0085-5},
}
```

To cite an article from the bibliography in your text, you use `@` followed by the citation identifier, e.g. `marrero2019`. For example, the article includes this line citing this reference:

``` markdown
Studies of the magma systems feeding the volcano, such as @marrero2019, have proposed ...
```

This renders as:

> Studies of the magma systems feeding the volcano, such as Marrero et al. (2019), have proposed …

Hovering over the citation text reveals the full reference details. Clicking on the citation takes a reader to the reference in the References section at the end of the article:

![Screenshot of the rendered article showing a section titled References. Below the title is a full reference starting 'Marrero, José, '.](images/article-references.png)

The above citation is an example where the author’s names are incorporated into the sentence itself. Another common style is to place the citation within parentheses, often at the end of a sentence. You can achieve this by enclosing the citation syntax in square brackets `[`. For example,

``` markdown
A prior study of the magma systems feeding the volcano proposed that there are two main magma reservoirs feeding the Cumbre Vieja volcano [@marrero2019].
```

This renders as:

> A prior study of the magma systems feeding the volcano proposed that there are two main magma reservoirs feeding the Cumbre Vieja volcano (Marrero et al. 2019).

There are many other syntax variations to include page numbers, chapters, or exclude the author names. You can read more in the [Citations](../../../docs/authoring/citations.llms.md) documentation.

The Visual Editor **Insert -\> Citation** dialog has utilities for adding citations from their DOI, your Zotero library, and public databases like Crossref, PubMed and DataCite. This provides an easy way to build the bibliography file (`.bib`) and generate the markdown citation syntax.

## Cross References

Quarto can generate cross references that keep track of numbering and linking for you. The general syntax for a cross reference is an `@` followed by a label. For example, to reference the timeline figure, you could write:

``` markdown
@fig-timeline
```

When rendered, cross references include a word to indicate the type of object being referenced, like “Figure” or “Table”. So for instance, this line in `index.qmd`:

``` markdown
Eight eruptions have been recorded since the late 1400s (@fig-timeline).
```

Results in the text:

> Eight eruptions have been recorded since the late 1400s (Figure 1).

Where “Figure 1” is also a link to the appropriate figure.

The labels you add to elements must have the appropriate prefix to allow cross referencing:

| Element  | Label Prefix | Rendered Cross Reference |
|----------|--------------|--------------------------|
| Figure   | `fig-`       | Figure 1                 |
| Table    | `tbl-`       | Table 1                  |
| Equation | `eq-`        | Equation 1               |
| Section  | `sec-`       | Section 1                |

You’ve already seen you can add a label to output generated by code using the `label` code chunk option. You’ll see how to add labels to non-code generated elements, like [equations](#equations), [tables](#tables), and [static figures](#static-figures), as you learn about them below.

To cross reference sections your document YAML header must also include:

``` yaml
number-sections: true
```

You can add a label to a section heading in curly braces after the heading, e.g:

``` markdown
## Data & Methods {#sec-data-methods}
```

You can then reference this section in the text, like:

``` markdown
Data and methods are discussed in @sec-data-methods.
```

Which will be rendered as:

> Data and methods are discussed in Section 2.

You can read more about the types of objects that can be referenced, including code listings, and mathematical theorems, as well as some of the options to control how references appear in the Quarto [Cross References](../../../docs/authoring/cross-references.llms.md) documentation.

In the Visual Editor, you can use **Insert -\> Cross Reference** to get a dialog box with the available labels in your document and quickly generate the syntax needed for a cross reference.

## Equations

Quarto markdown can include equations specified in LaTeX notation. Use single dollar signs (`$`) to add an equation inline or double dollar signs (`$$`) to add a display equation. Both of these are illustrated in the following paragraph in `index.qmd`:

``` markdown
Let $x$ denote the number of eruptions in a year. Then, $x$ can be modeled by a Poisson distribution

$$
p(x) = \frac{e^{-\lambda} \lambda^{x}}{x !}
$$ {#eq-poisson}

where $\lambda$ is the rate of eruptions per year. Using @eq-poisson, the probability of an eruption in the next $t$ years can be calculated.
```

Notice the display equation has a label added in curly braces after the closing `$$`. This allows it to be referenced using `@eq-poisson` in the text.

When rendered, this displays as:

> Let \\x\\ denote the number of eruptions in a year. Then, \\x\\ can be modeled by a Poisson distribution \\ p(x) = \frac{e^{-\lambda} \lambda^{x}}{x !} \tag{1}\\ where \\\lambda\\ is the rate of eruptions per year. Using [Equation 1](#eq-poisson), the probability of an eruption in the next \\t\\ years can be calculated.

## Tables

Tables can be added inline with what is known as pipe syntax. As an example, in `index.qmd` a table of earthquakes is specified as:

``` markdown
| Name                 | Year   |
| -------------------- | ------ |
| Current              | 2021   |
| Teneguía             | 1971   |
| Nambroque            | 1949   |
| El Charco            | 1712   |
| Volcán San Antonio   | 1677   |
| Volcán San Martin    | 1646   |
| Tajuya near El Paso  | 1585   |
| Montaña Quemada      | 1492   |

: Recent historic eruptions on La Palma {#tbl-history}
```

Columns are separated by pipes (`|`), and the dashes (`-`) in the second row separate the header row from the rest of the table. A caption can be provided with a line starting with `:`. A label that can be used for cross references is added at the end of the caption inside curly braces. Like figures, the label prefix `tbl-` is required for cross references, but the suffix is up to you.

Inserting and editing tables using markdown syntax can be cumbersome. The Visual Editor provides tools for editing existing tables, and inserting new tables. Use the Table menu in the visual editor toolbar or right-click inside a table to bring up the options.

Read more about working with tables in the RStudio Visual Editor at [Editing Tables](../../../docs/visual-editor/content.llms.md#editing-tables).

You can learn more about tables in Quarto, including an alternative syntax known as grid tables, on the [Tables](../../../docs/authoring/tables.llms.md) page in the Quarto documentation.

## Static Figures

To include a figure from a file, the markdown syntax looks like:

``` markdown
![Caption](file_path_to_image)
```

For example, to include the `la-palma-map.png` image from the `images/` folder in the project, along with the caption “Map of La Palma”, you would write:

``` markdown
![Map of La Palma](images/la-palma-map.png)
```

> **TIP:**
>
> You don’t have to store your images in a folder called `images/`, although it is a common convention. Your images can be anywhere **inside** your manuscript project directory, just make sure you include the full path to the image, relative to the location of `index.qmd`.

The actual markdown in `index.qmd` includes a further attribute, `#fig-map` inside curly braces following the image path to provide a label for cross references:

``` markdown
![Map of La Palma](images/la-palma-map.png){#fig-map}
```

Another attribute that you may wish to add is `fig-alt`, the alt text to be provided for the image. For example:

``` markdown
![Map of La Palma](images/la-palma-map.png){#fig-map fig-alt="A map of the Canary Islands. The second most west island, La Palma, is highlighted."}
```

You can read more about including figures in Quarto documents, including how to resize figures and arrange multiple figures, on the Quarto docs [Figures](../../../docs/authoring/figures.llms.md) page.

## External Embeds

> **NOTE:**
>
> This section covers embedding outputs from Quarto documents (`.qmd`). You can also [embed outputs from Jupyter Notebooks (`.ipynb`)](../../../docs/authoring/notebook-embed.llms.md).

An alternative to including computations directly in the article notebook is to embed output from other notebooks. This manuscript project includes the notebook `explore-earthquakes.qmd` in the `notebooks/` folder.

To embed output from a notebook, you can use the `embed` shortcode. Quarto shortcodes are special markdown directives that generate content. The `embed` shortcode is used in main article file in the line:

``` markdown
{{< embed notebooks/explore-earthquakes.qmd#fig-spatial-plot >}}
```

The double curly braces (`{{`) and angle brackets (`<`) indicate this is a shortcode. The `embed` shortcode requires a path to a notebook chunk. In this case, it’s the file path to a source notebook, `explore-earthquakes.qmd`, followed by `#` and a chunk label. The chunk label is set using the Quarto chunk option `label` in `explore-earthquakes.qmd` notebook:

```` markdown
```{r}
#| label: fig-spatial-plot
#| fig-cap: "Locations of earthquakes on La Palma since 2017"
#| fig-alt: "A scatterplot of earthquake locations plotting latitude 
#|   against longitude."
la_palma |> 
  ggplot(aes(Longitude, Latitude)) +
  geom_point(aes(color = Magnitude, size = 40-`Depth(km)`)) +
  scale_color_viridis_c(direction = -1) + 
  scale_size(range = c(0.5, 2), guide = "none") +
  theme_bw()
```
````

Just like any figure, using a label starting with `fig-` allows it to be cross referenced in the text. Any other options, like the figure caption (`fig-cap`) and alt text (`fig-alt`), can also be set in the source notebook.

Whenever you change the content of `explore-earthquakes.qmd`, including updating chunk options like the caption, it will be re-rendered. Consequently, the code in `explore-earthquakes.qmd` will also be re-run.

To re-run the code in this notebook, you’ll need to have the tidyverse package:

``` r
install.packages("tidyverse")
```

For example, if you edit the caption to:

``` r
#| fig-cap: "Earthquakes on La Palma since 2017."
```

You’ll notice in the background `quarto preview` re-renders the file:

``` bash
processing file: explore-earthquakes.qmd
                                                                                    output file: explore-earthquakes.qmd

Rendering output notebook [notebooks/explore-earthquakes.qmd]
Rendering HTML preview [notebooks/explore-earthquakes.qmd]
```

And then the caption in the main article preview updates.

## Up Next

You’ve now covered the main features of Quarto for authoring a manuscript. You’ve edited `index.qmd`, added resources like figures, notebooks or bibliographic data, and previewed the result.

Once, you are happy with the changes you’ve made, you’ll need update your public manuscript webpage.

Head on to [Publishing](../../../docs/manuscripts/publishing.llms.md) to learn how to publish and share your manuscript with the world.
