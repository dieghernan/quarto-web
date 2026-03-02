# Project Basics

## Overview

Quarto projects are directories that provide:

- A way to render all or some of the files in a directory with a single command (e.g. `quarto render myproject`).

- A way to share YAML configuration across multiple documents.

- The ability to redirect output artifacts to another directory.

- The ability to freeze rendered output (i.e. don’t re-execute documents unless they have changed).

In addition, projects can have special “types” that introduce additional behavior (e.g. [websites](../../docs/websites/index.llms.md) or [books](../../docs/books/index.llms.md)).

> **NOTE:**
>
> If you are just getting started with Quarto and/or you don’t have previous experience with markdown publishing systems, you probably want to skip learning about projects for now. Once you are comfortable with the basics, come back to this article to learn more.

## Creating Projects

Use the `quarto create project` command to create a new project, using the prompt.

``` bash
quarto create project
```

``` bash
 ? Type
 ❯ default
   website
   blog
   manuscript
   book
   confluence
```

Or define the type and the project name as arguments.

``` bash
quarto create project <type> <name>
```

## Shared Metadata

One of the most important features of Quarto Projects is the ability to share YAML metadata options across multiple documents. Shared metadata can be defined at both the project and directory level.

### Project Metadata

All Quarto projects include a `_quarto.yml` configuration file. Any document rendered within the project directory will automatically inherit the metadata defined at the project level. Here is an example of what the `_quarto.yml` file might look like:

``` yaml
project:
  output-dir: _output

toc: true
number-sections: true
bibliography: references.bib  
  
format:
  html:
    css: styles.css
    html-math-method: katex
  pdf:
    documentclass: report
    margin-left: 30mm
    margin-right: 30mm
```

Note that the project file contains both global options that apply to all formats (e.g. `toc` and `bibliography`) as well as format-specific options.

You can further customize project metadata based on different project profiles (e.g. development vs. production or creating multiple versions of a book or website). See the article on [Project Profiles](../../docs/projects/profiles.llms.md) for additional details.

### Directory Metadata

You can also define metadata that should be inherited by only files within a directory. To do this, add a `_metadata.yml` file to the directory where you want to share metadata. For example, the following `_metadata.yml` sets up default Revealjs options for a series of presentations and disables `search` for documents within the directory:

``` yaml
format:
  revealjs: 
    menu: false
    progress: false
search: false
```

Options provided within these files use the same schema as `_quarto.yml` and are merged with any options you’ve already provided in `_quarto.yml`.

### Metadata Merging

Metadata defined within `_quarto.yml`, `_metadata.yml`, and document-level YAML options are merged together. Document level options take priority, followed by directory options and finally project-level options:

| File                | Role                                                |
|---------------------|-----------------------------------------------------|
| `_quarto.yml`       | Project level default options                       |
| `dir/_metadata.yml` | Directory level default options (overrides project) |
| `dir/document.qmd`  | Document options (overrides directory and project)  |

Note that when metadata is combined, objects and arrays are merged rather than simply overwriting each other. For example, here is how project and directory level options that affect output format and bibliographies would be merged:

[TABLE]

The one exception to metadata merging is `format`. If the document-level YAML defines a format, it must define the complete list of formats to be rendered.

### Metadata Includes

You might find it convenient to break your metadata into multiple files. You can do this using the `metadata-files` option. For example, here we include some website options with a separate `_website.yml` in the `_quarto.yml`:

``` yaml
project:
  type: website
  
metadata-files:
  - _website.yml
```

``` yaml
website:
  navbar:
    background: primary
    left:
      - href: index.qmd
        text: Home
      - about.qmd
```

Files listed in `metadata-files` are merged with the parent file in the same fashion that project, directory, and document options are merged. This means that included files can both provide new options as well as combine with existing options.

### Local Config

Sometimes its useful to define local changes to project configuration that are not checked in to version control. You can do this by creating a `_quarto.yml.local` config file. For example, here we specify that we want to use the execution cache when running locally:

``` yaml
execute:
  cache: true
```

Note that Quarto automatically writes an entry to `.gitignore` to ensure that `.local` files are not committed (note that [environment variables](../../docs/projects/environment.llms.md#local-environment) can also be defined in a similar `.local` file).

## Rendering Projects

You can render files within a project either one-by-one or all at once (in either case, shared project metadata will be used).

To render all of the documents within a project, just use `quarto render` within the project directory (or target a specific directory with a command line argument):

``` bash
# render project in current dir
quarto render 

# render project in 'myproject'
quarto render myproject
```

You can also render only the files within a sub-directory of a project. For example, if the current directory contains a project with sub-directories `tutorials`, `how-to`, and `articles`, you can render just the contents of `articles` as follows:

``` bash
# render only documents in the 'articles' sub-directory
quarto render articles
```

Note that when rendering a project, command line arguments you pass to `quarto render` will be used for each file in the project. For example, this command will render only the PDF format:

``` bash
quarto render --to pdf
quarto render myproject --to pdf
```

If you are working with Quarto from R, you can also render a project from the R console using the **quarto** R package.

``` r
library(quarto)
quarto_render()
```

## Render Targets

By default, all valid Quarto input files (.qmd, .ipynb, .md, .Rmd) in the project directory will be rendered, save for ones with:

1.  A file or directory prefix of `.` (hidden files)

2.  A file or directory prefix of `_` (typically used for non top-level files, e.g. ones [included](../../docs/authoring/includes.llms.md) in other files)

3.  Files named `README.md` or `README.qmd` (which are typically not actual render targets but rather informational content about the source code to be viewed in the version control web UI).

If you don’t want to render all of the target documents in a project, or you wish to control the order of rendering more precisely, you can add a `project: render: [files]` entry to your project metadata. For example:

``` yaml
project:
  render:
    - section1.qmd
    - section2.qmd
```

Note that you can use wildcards when defining the `render` list. For example:

``` yaml
project:
  render:
    - section*.qmd
```

You can also use the prefix `!` to ignore some files or directories in the `render` list. Note that in that case you need to start by specifying everything you *do* want to render. For example:

``` yaml
project:
  render:
    - "*.qmd"
    - "!ignored.qmd"
    - "!ignored-dir/"
```

> **NOTE:**
>
> If the name of your output file needs to start with `.` or `_` (for instance `_index.md` for Hugo users), you must name the Quarto input file without the prefix (for instance `index.qmd`) and add an explicit `output-file` parameter in the YAML such as
>
> ``` yaml
> ---
> output-file: _index.md
> ---
> ```

### Engine prioritization

Quarto supports different engines to execute code. Historically, the R, Python and Julia languages were only supported by one engine, each, so there was no need to choose an execution engine. With the addition of the native Julia engine, this changed.

When determining which execution engine to use for a given notebook, Quarto checks the available engines in a predefined order, which means that the Jupyter engine is always preferred for Julia over the native engine.

Starting with Quarto 1.7, instead of specifying `engine: julia` in the frontmatter of every notebook in a project, you can set a different prioritization order in your project file using the `engines` key.

All the engines you list there will be checked first in the order you provide. The remaining engines will be checked by Quarto in the usual predefined order. To enable the native Julia engine project-wide, it is therefore enough to add this line to your project file:

``` yaml
engines: ['julia']
```

## Learning More

These articles provide additional documentation on more advanced features of Quarto projects:

- [Managing Execution](../../docs/projects/code-execution.llms.md) covers various techniques you can use to minimize the time required to rebuild a site that has expensive computations.

- [Project Profiles](../../docs/projects/profiles.llms.md) describes how you can adapt both the options and content of your projects for different scenarios (e.g. development vs. production or creating multiple versions of a book or website).

- [Environment Variables](../../docs/projects/environment.llms.md) covers how to define environment variables that should be set whenever your project is rendered (including how to vary those variables by project profile and/or for use in local development).

- [Project Scripts](../../docs/projects/scripts.llms.md) describes how to add periodic or pre/post render scripts to projects for special processing of input data and project outputs.

- [Virtual Environments](../../docs/projects/virtual-environments.llms.md) explores how to create project-specific package libraries, which helps with faithfully reproducing your environment over time as well as ensuring that upgrading a package in one project doesn’t break other projects.
