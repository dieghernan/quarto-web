# Text Editors

## Overview

If you are editing plain markdown documents (with no embedded computations) you may want to use your favorite text editor (Vim, Emacs, Sublime, etc.) to author Quarto documents. This articles provides some guidance on the optimal workflow when using text editors with Quarto.

Note that if you are using either the [Jupyter](https://jupyter.org/) or [Knitr](https://yihui.org/knitr/) computational engine you will likely be better off using [JupyterLab](../../docs/tools/jupyter-lab.llms.md) or [VS Code](../../docs/tools/vscode/index.llms.md) (for .ipynb notebooks) or [Positron](../../docs/tools/positron/index.llms.md) or [RStudio](../../docs/tools/rstudio.llms.md) (for .qmd documents) as these environments provide code-completion, incremental cell execution, and other useful tools for working with executable code.

## Workflow

The ideal workflow for authoring Quarto markdown documents is to run the `quarto preview` command from within a terminal:

``` bash
quarto preview document.qmd
```

The document will be rendered and a web browser with a “live preview” opened. Position this browser so that you can see it as you edit and save the document:

![Two application windows arranged side by side. A Quarto document that contains the contents of the Welcome page of this website is open on the right. The contents of this document are rendered in a web browser by Quarto in the window on the right.](images/vim-preview.png)

Every time you save the preview will be automatically updated. You can use `quarto preview` for both HTML and PDF output.

Preview uses the default format specified within the document—to use an alternate format pass the `--to` option to `quarto preview`. For example:

``` bash
quarto preview notebook.qmd --to pdf
```

> **NOTE:**
>
> Note that if you are authoring a book or website you can also use [`quarto preview`](../../docs/websites/index.llms.md#workflow) on the project directory, which will create a live preview for the entire project.

#### Render without Preview

You can render a document (or group of documents) without previewing them using the `quarto render` command:

``` bash
quarto render document.qmd
```

Use the `--to` argument to render to a specific format:

``` bash
quarto render document.qmd --to docx
```

### File Extension

Most text editors have a syntax highlighting mode that applies to markdown files (typically with the `.md` extension). You will likely want to configure your editor to also recognize the `.qmd` extension as having markdown content.
