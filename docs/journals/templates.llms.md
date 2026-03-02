# Article Templates

## Overview

Journal article formats often require fine grained control of generated output as well as the ability to use Journal-specific commands and directives. This can be achieved for Quarto formats by providing custom Pandoc templates (LaTeX and/or HTML). Often these templates are a mix of Journal-specific LaTeX and standard directives required by Pandoc. This article describes how to create custom Journal templates that behave well with Pandoc and produce high-fidelity publisher ready output.

## Templates

Quarto uses [Pandoc templates](https://pandoc.org/MANUAL.llms.md#templates) to generate the rendered output from a markdown file. A Pandoc template is a mix of format specific content and variables. The variables will be replaced with their values from a rendered document. For example, the most basic template looks like:

``` latex
\documentclass{scrartcl}
\begin{document}
$body$
\end{document}
```

In the above template, the `$body$` variable will be replaced with the LaTeX that is generated from the body of the document. If the body text is `Hello **world**!` in Markdown, the value of `$body$` will be `Hello \textbf{world}!`.

By providing your own custom template used when rendering, you have complete control of the final output. You can provide this custom template to be used when rendering like this:

``` yaml
format:
  pdf:
    template: mytemplate.tex
```

For more complete information about template syntax, see [Template syntax](https://pandoc.org/MANUAL.llms.md#template-syntax).

## Template Partials

Replacing an entire template gives you complete control of the rendered output, but many features of Pandoc and Quarto depend upon code and variables that appear in the built in templates. If you replace the entire template and omit these variables, features will not work properly.

It’s therefore recommended that you take one of two approaches when authoring templates:

1.  Selectively [replace partials](#replacing-partials) that exist within the master LaTeX or HTML template.

2.  Replace the entire LaTeX or HTML template, but then [include partials](#including-partials) provided with Quarto to ensure that your template takes advantage of all Pandoc and Quarto features.

Below we’ll cover both of these approaches. Note that after reviewing this documentation you may also want to check out the source code of formats published on [quarto-journals](https://github.com/quarto-journals/) for additional examples.

### Replacing Partials

For LaTeX / PDF and HTML output, Quarto provides built in templates that are composed of a set of ‘partial’ template files. For these formats, you may replace portions of Quarto’s built in template, allowing you to customize just a portion of the template without needing to replace the whole thing. A simple partial to provide custom handling of the document title in LaTeX looks like:

``` latex
\title{$title$}
\author{$for(author)$$author$$sep$ \and $endfor$}
\date{$date$}
```

You provide this partial to Quarto like:

``` yaml
format:
  pdf:
    template-partials:
      - title.tex
```

When Quarto renders a document with a partial, it will use the built in template but replace a portion of the template with the provided partial. In the above case, the LaTeX title will be replaced with the implementation provided as the partial, while the rest of the built in template will be used.

The name of the partial file is important. You choose which portion of the template to replace by providing a partial with that name. Providing an empty file as a partial is a way to opt out of some features without modifying the whole main template.

You can see the list of partials available for each format below: [LaTeX Partials](#latex-partials), [Beamer Partials](#beamer-partials), [Typst Partials](#typst-partials), [HTML Partials](#html-partials) and [Revealjs Partials](#revealjs-partials).

### Including Partials

In addition to replacing built in partials with your own, you may also choose to use built in partials when composing your own template. This allows you to create a template that takes advantage of the capabilities and options provided by Quarto and Pandoc without copying and maintaining the entire template code. For example, you can use the `$pandoc.tex()$` partial to include pandoc configuration for text highlighting, tables, graphics, tight lists, citations, and header includes:

``` latex
\documentclass{scrartcl}
$pandoc.tex()$
\begin{document}
$body$
\end{document}
```

This modular approach means that it is easier to implement templates that:

- Include required elements of Pandoc templates

- Support general Pandoc features and options

- Provide only the minimal LaTeX or HTML rather than being required to provide all of it

## LaTeX Partials

> **NOTE:**
>
> For `format: beamer`, see [Beamer Partials](#beamer-partials)

View the Quarto LaTeX template and partials [source code here](https://github.com/quarto-dev/quarto-cli/tree/main/src/resources/formats/pdf/pandoc).

Starting with Quarto 1.7, which provides Pandoc 3.6.3, there are two sets of partials: those specific to Quarto and those inherited from Pandoc. The source directory contains:

- partials with `.latex` extension that are inherited from Pandoc,
- partials with `.tex` extension that are provided by Quarto directly for more granular customization.

template.tex  
The core LaTeX template which includes the basic document skeleton plus the following partials. This can’t be replaced as a `template-partial`, instead use the `template` option to provide your own template.

passoptions.latex  
Contains declarations using the `\PassOptionsToPackage` command to modify options for packages that may be used later in the template.

doc-class.tex  
Contains the document class declaration and options. By default we provide an identical document class to Pandoc, which implements many features. If you override this (which will be common), you will need to either implement support for the document class options or be aware that those options (e.g. `font-size`, `paper-size`, `classoption`, etc…) will not be supported in your output.

fonts.latex  
Contains declarations to load LaTeX packages useful for fonts

font-settings.latex  
Contains declarations to configure font packages, depending on which packages and LaTeX engine are used.

common.latex  
Contains mostly declarations related to Pandoc features for LaTeX (like `linestretch`, `indent`, `verbatim-in-note`, `listings`, …). Quarto modifies this template from Pandoc to use more specific partials by splitting content between `common.latex` and `pandoc.tex`. You can either replace this partial entirely or a more specific one from `pandoc.tex`. In general, the `common.latex` and `pandoc.tex` partials must always be included within your custom template.

pandoc.tex  
This includes configuration for most Pandoc features like text highlighting, tables, graphics, tight lists, citations, and header includes. In general, this partial must always be included within your custom template. In some circumstances, you may know that certain capabilities will not be needed, so this partial is further composed of the following partials, which could be used if sensible:

tables.tex  
Provides configuration for the output of tables, table captioning, and footnotes within tables.

graphics.tex  
Provides image scaling and placement configuration.

citations.tex  
When using CSL references, provides configuration and commands for outputting the bibliography.

babel-lang.tex  
When `lang` option is used, provides configuration and command for babel support and other language related LaTeX configuration.

tightlist.tex  
Provides the tight list command.

biblio-config.tex  
Provides natbib or biblatex configurations. To opt-out of these configurations (e.g. for a custom format where a specific documentclass handles it already), rather than provide an empty partial, use `biblio-config: false` for your document configuration.

after-header-includes.latex  
Contains what needs to be inserted after user specific header includes, like bookmark configuration.

hypersetup.latex  
Contains the `\hypersetup` command configuration.

before-title.tex  
Appears in the document premable just before the title block. By default, this partial is empty.

title.tex  
Provides configuration of document metadata for writing the title block. Note that in addition to these templates and partials, Quarto will also make normalized authors and affiliations data available to the template, making is easy to write custom title blocks against a standard schema.

before-body.tex  
Implements the frontmatter, title page, and abstract.

toc.tex  
Creates the table of contents, list of figures, and list of tables.

before-bib.tex  
Placed after the content of the document, but before the bibliography. By default contains nothing.

biblio.tex  
Creates the bibliography using either natbib or biblatex if used.

after-body.tex  
Provides a placeholder to attach content at the end of the body, right before `\end{document}`

A copy of some of Pandoc’s original files are also kept in Quarto’s source as a reference. These files are: `latex.template`, the main template used as `template.tex` containing all the partials; and `latex.common` the original version of `common.latex`, which is tweaked to support Quarto’s more specific partials.

See the [full source code](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/formats/pdf/pandoc/template.tex) for the Quarto LaTeX template to see how these partials are invoked by default.

## Beamer Partials

> **NOTE:**
>
> New from Quarto 1.7: `format: beamer` now uses its own template and partials.

View the Quarto Beamer template and partials [source code here](https://github.com/quarto-dev/quarto-cli/tree/main/src/resources/formats/beamer/pandoc).

Starting with Quarto 1.7, which provides Pandoc 3.6.3, there are two sets of partials: those specific to Quarto and those inherited from Pandoc. The source directory contains:

- partials with `.latex` extension that are inherited from Pandoc,
- partials with `.tex` extension that are provided by Quarto directly for more granular customization.

template.tex  
The core LaTeX template which includes the basic document skeleton plus the following partials. This can’t be replaced as a `template-partial`, instead use the `template` option to provide your own template.

passoptions.latex  
Contains declarations using the `\PassOptionsToPackage` command to modify options for packages that may be used later in the template.

doc-class.tex  
Contains the document class declaration and options. By default we provide an identical document class to Pandoc, which implements many features. If you override this (which will be common), you will need to either implement support for the document class options or be aware that those options (e.g. `font-size`, `paper-size`, `classoption`, etc…) will not be supported in your output.

fonts.latex  
Contains declarations to load LaTeX packages useful for fonts

font-settings.latex  
Contains declarations to configure font packages, depending on which packages and LaTeX engine are used.

common.latex  
Contains mostly declarations related to Pandoc features for LaTeX (like `linestretch`, `indent`, `verbatim-in-note`, `listings`, …). Quarto modifies this template from Pandoc to use more specific partials by splitting content between `common.latex` and `pandoc.tex`. You can either replace this partial entirely or a more specific one from `pandoc.tex`. In general, the `common.latex` and `pandoc.tex` partials must always be included within your custom template.

pandoc.tex  
This includes configuration for most Pandoc features like text highlighting, tables, graphics, tight lists, citations, and header includes. In general, this partial must always be included within your custom template. In some circumstances, you may know that certain capabilities will not be needed, so this partial is further composed of the following partials, which could be used if sensible:

tables.tex  
Provides configuration for the output of tables, table captioning, and footnotes within tables.

graphics.tex  
Provides image scaling and placement configuration.

citations.tex  
When using CSL references, provides configuration and commands for outputting the bibliography.

babel-lang.tex  
When `lang` option is used, provides configuration and command for babel support and other language related LaTeX configuration.

tightlist.tex  
Provides the tight list command.

biblio-config.tex  
Provides natbib or biblatex configurations. To opt-out of these configurations (e.g. for a custom format where a specific documentclass handles it already), rather than provide an empty partial, use `biblio-config: false` for your document configuration.

after-header-includes.latex  
Contains what needs to be inserted after user specific header includes, like bookmark configuration.

hypersetup.latex  
Contains the `\hypersetup` command configuration.

before-title.tex  
Appears in the document premable just before the title block. By default, this partial is empty.

title.tex  
Provides configuration of document metadata for writing the title block. Note that in addition to these templates and partials, Quarto will also make normalized authors and affiliations data available to the template, making is easy to write custom title blocks against a standard schema.

before-body.tex  
Implements the frontmatter, title page, and abstract.

toc.tex  
Creates the table of contents, list of figures, and list of tables.

before-bib.tex  
Placed after the content of the document, but before the bibliography. By default contains nothing.

biblio.tex  
Creates the bibliography using either natbib or biblatex if used.

after-body.tex  
Provides a placeholder to attach content at the end of the body, right before `\end{document}`

A copy of some of Pandoc’s original files are also kept in Quarto’s source as a reference. These files are: `beamer.template`, the main template used as `template.tex` containing all the partials; and `latex.common` the original version of `common.latex`, which is tweaked to support Quarto’s more specific partials.

See the [full source code](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/formats/beamer/pandoc/template.tex) for the Quarto Beamer template to see how these partials are invoked by default.

## Typst Partials

View the Quarto Typst template and partials [source code here](https://github.com/quarto-dev/quarto-cli/tree/main/src/resources/formats/typst/pandoc/quarto).

template.typ  
The core Typst template file which includes the basic document skeleton plus the following partials. This can’t be replaced as a `partial`, instead use the `template` option to provide your own template.

definitions.typ  
Definitions for Pandoc and Quarto features like block quotes, callouts, subfloats etc. In general, this partial must always be included within your custom template.

typst-template.typ  
The definition of the Typst template function that will be called on the entire document contents. In the default template this function is called `article()` and generates a title block and author list, followed by the document content, optionally laid out in columns.

page.typ  
Sets properties of the page such as size, margin, numbering, and background logo.

typst-show.typ  
A show rule for the entire document that captures document metadata and passes it to the function defined in `typst-template.typ`.

notes.typ  
Creates footnotes.

biblio.typ  
Creates the bibliography.

## HTML Partials

View the Quarto html template and partials [source code here](https://github.com/quarto-dev/quarto-cli/tree/main/src/resources/formats/html/pandoc). Note that `html.template` is a copy of the complete Pandoc template that the Quarto template and partials is based upon.

Quarto’s HTML template is broken down into the following components:

template.html  
The core HTML template which includes the basic document skeleton plus the following partials. This can’t be replaced as a `partial`, instead use the `template` option to provide your own template.

metadata.html  
Populates basic document metadata into the HTML document head. More advanced metadata elements are not currently implemented within this template (e.g. social media, academic metadata) but are implemented as post processors.

title-block.html  
Provides the title block for the document. 

toc.html  
Provide the table of contents target for the document

## Revealjs Partials

View the Quarto Revealjs template and partials [source code here](https://github.com/quarto-dev/quarto-cli/tree/main/src/resources/formats/revealjs/pandoc). Note that `revealjs.template` is a copy of the complete Pandoc template that the Quarto template and partials is based upon.

template.html  
The core Revealjs templates which includes the basic presentation skeleton plus the following partials. This can’t be replaced as a `partial`, instead use the `template` option to provide your own template.

title-slide.html  
HTML used for the presentation title slide. By default, Quarto uses a fancy `title-slide.html` partial that leverages [Authors & Affiliations](../../docs/journals/authors.llms.md) handling. Use the `title-slide.html` [source code](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/formats/revealjs/pandoc/title-fancy/title-slide.llms.md) as a starter if you want to tweak this partial.

toc-slide.html  
HTML used for the presentation table of contents.
