# Quarto 1.7 Pre-Release

Published

March 3, 2026

Quarto 1.7 includes the following new features:

- Improvements to dark mode:

  - [Dark Brand](../../../docs/authoring/brand.llms.md#dark-brand): Light and dark brands can be specified for a document or project, enabling dark mode via brand.yml.
  - [`renderings`](../../../docs/computations/execution-options.llms.md#cell-renderings): Plots and tables can have `light` and `dark` renderings.
  - [`respect-user-color-scheme`](../../../docs/output-formats/html-themes.llms.md#dark-mode): If enabled, this option detects the user’s operating system / browser preference for whether to show the page in light or dark mode.

- New [`version` shortcode](../../../docs/authoring/version.llms.md) to insert the version of Quarto used to build your document:

  ``` markdown
  Rendered with Quarto {{< version >}}
  ```

  Rendered with Quarto 1.9.28

- Improvements to the `julia` engine:

  - [`juliaup` integration](../../../docs/computations/julia.llms.md#juliaup-integration): Use specific versions of Julia in your notebooks.
  - [R and Python support](../../../docs/computations/julia.llms.md#r-and-python-support): Include `{r}` and `{python}` executable code cells via the RCall and PythonCall packages.
  - [Caching](../../../docs/computations/julia.llms.md#caching-julia): Save time rendering long-running notebooks by caching results.
  - [Revise.jl integration](../../../docs/computations/julia.llms.md#revise.jl-integration): Automatically update function definitions in Julia sessions.

- Updated LaTeX and Beamer template partials:

  - [LaTeX partials](../../../docs/journals/templates.llms.md#latex-partials)
  - [Beamer partials](../../../docs/journals/templates.llms.md#beamer-partials)

  These changes reflect the updates made in Pandoc 3.5 to separate the LaTeX and Beamer document templates and introduce some additional partials for both. If you have custom formats that provide custom templates or partials, you may need to update them to work with the new partials.

- Typst updated to 0.13.0

- Pandoc updated to 3.6.3

See the [Pre-Release Download Page](../../../docs/download/prerelease) for a complete list of all the changes and bug fixes.
