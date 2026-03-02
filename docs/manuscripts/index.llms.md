# Quarto Manuscripts

## Overview

Quarto manuscript projects provide a framework for writing and publishing scholarly articles. A Quarto manuscript lets you:

- Use one or more notebooks or `.qmd` documents as the source of content and computations, and then publish these computations alongside the manuscript, allowing readers to dive into your code.

- Produce manuscripts in multiple formats (including LaTeX or MS Word formats required by journals), and give readers easy access to all of the formats through a manuscript website.

The output of a Quarto manuscript is a website ([live example](https://quarto-ext.github.io/manuscript-template-jupyter/)). The article itself appears as the content of the website, and can include all the elements common to scholarly writing like figures, tables, equations, cross references and citations. The website also makes available other formats (e.g. PDF, Docx) as well as links to all of the computations used to create the article.

![A screenshot of the content area on the manuscript webpage. Content shows a title block including the article title, authors, and abstract, body text, and an image with a caption.](images/article-content.png)

Article Content

![A screenshot of the menu on the right hand side of the manuscript webpage. The menu has headings: Table of contents, Other Formats, Notebooks and Other Links.](images/webpage-menu.png)

Navigation

On the right, you’ll see navigation: a table of contents for the article itself followed by links to **Other Formats**, **Notebooks** and **Other Links**.

### Other Formats

These links allow a reader to download alternative formats of your article. In this example, there is an MS Word version that may be useful for a reviewer to provide feedback and a PDF version that uses the American Geophysical Union’s (AGU) template. Additionally, there is a MECA archive, a zip file that is designed to capture your article and its supporting documents into a single file suitable for sending to a publisher.

### Notebooks

These are links to notebooks included in the manuscript. The “Article Notebook” is the notebook version of the article itself. In this example, “Data Screening” is a notebook from which a single cell is embedded in the article. Any other notebooks that are included in the project, even if they are not directly used in the article will also appear here.

When a reader visits any of these notebook links, they are served an HTML version of the notebook, allowing them to view the code and output without leaving their browser. In addition, a link to download the source code of the notebook is also provided.

![Screenshot of the notebook view of data-screening.ipynb. The top of the page has a link Back to the Article and a button to Download Notebook. The content of the page includes some text and a cell displaying code.](images/notebook-view.png)

HTML view of the Data Screening notebook

### Other Links

Links that leave the manuscript webpage, for example to take a reader to the manuscript’s GitHub Repo.

## Get Started

### Install Quarto

Manuscripts are a feature in the 1.4 release of Quarto. Before you get started, make sure you install the **latest release** version of Quarto.

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

### Choose Your Tool

You can author Quarto manuscripts in any tool or notebook editor. The tutorials below walk you through authoring Quarto manuscripts with a few common tools.

Choose your tool to start learning:

[![Jupyter logo.](images/jupyter-logo.png)Jupyter](authoring/jupyterlab.llms.md)

[![VS Code logo.](images/vscode-logo.png)VS Code](authoring/vscode.llms.md)

[![RStudio logo.](images/rstudio-logo.png)RStudio](authoring/rstudio.llms.md)
