# Dashboard Options

## Format

The following document and format options are either dashboard-specific or have special behavior within dashboards:

| Option | Description |
|----|----|
| `title` | Title (displayed in top left of navigation bar) |
| `author` | Author (displayed alongside title in smaller font) |
| `logo` | Logo (displayed left of the title in the navigation bar) |
| `orientation` | `rows` or `columns` (default: `rows`) |
| `scrolling` | Use scrolling rather than fill layout? (default: `false`) |
| `expandable` | Make card content expandable (default: `true`) |
| `theme` | Dashboard theme (built in or custom scss) |
| `nav-buttons` | Buttons to appear on the right side of the navigation bar. Use `linkedin`, `facebook`, `reddit`, `twitter`, `github`, or a custom [Nav Item](../../../docs/reference/projects/websites.llms.md#nav-items). |

For example:

``` yaml
---
title: "Dashboard"
author: "Acme, Inc."
logo: images/acme.png
format:
  dashboard:
     theme: default
     orientation: rows
     expandable: true
     scrolling: false
     nav-buttons:
      - reddit
      - icon: gitlab
        href: https://gitlab.com/
---
```

### Pages

[Pages](../../../docs/dashboards/layout.llms.md#pages) can specify a custom orientation that is distinct from the global orientation:

| Option        | Description                                         |
|---------------|-----------------------------------------------------|
| `orientation` | `rows` or `columns` (default to global orientation) |
| `scrolling`   | `true` or `false` (defaults to global scrolling)    |

For example:

``` python
---
title: "Dashboard"
format: dashboard
---

# Plots {orientation="columns" scrolling="true"}
```

### Sidebars

Create [Sidebars](../../../docs/dashboards/layout.llms.md#sidebars) by applying the `.sidebar` attribute to a level 1 heading (for global sidebars) or level 2 heading (for page level sidebars).

| Class      | Description                                |
|------------|--------------------------------------------|
| `.sidebar` | Contents should be arranged into a sidebar |

For example:

``` python
---
title: "Dashboard"
format: dashboard
---

# Plots {.sidebar}
```

### Rows & Columns

Rows and columns support options for customizing their layout and sizing behavior. The following classes can be used to modify layout behavior:

| Class | Description |
|----|----|
| `.tabset` | Contents should be arranged into a [Tabset](../../../docs/dashboards/layout.llms.md#tabsets) |
| `.fill` | Contents should fill available layout space |
| `.flow` | Contents should flow to their natural size |

Note that in most dashboards, `.fill` and `.flow` are determined automatically based on the contents of cards and don’t need to be specified manually.

The following attributes can be used for explicit sizing:

| Option | Description |
|----|----|
| `width` | Percentage or absolute pixel width (default distributes space evenly across elements in a row) |
| `height` | Percentage or absolute pixel height (default distributes space evenly across elements in a column) |

For example:

``` python
---
title: "Dashboard"
format: dashboard
---

## Row {height="65%"}

## Row {height="35%"}
```

Note that if some components specify an explicit `width` or `height` and others do not, then remaining space will be distributed evenly across those elements.

### Cards

Card options enable you to specify a title and various layout behaviors:

| Option | Description |
|----|----|
| `title` | Title displayed in card header |
| `padding` | Padding around card content (default: `8px`) |
| `expandable` | Make card content expandable (default: `true`) |
| `width` | Percentage or absolute pixel width (default distributes space evenly across elements in a row) |
| `height` | Percentage or absolute pixel height (default distributes space evenly across elements in a column) |
| `fill` | Whether the card should fill its container or ‘flow’, matching the height of its content. (Quarto determines the default value based upon the card contents) |

For example:

```` python
```{python}
#| title: "Life Expectancy"
#| padding: 3px
#| expandable: false
#| width: 70%
```
````

These same options can be applied to `.card` divs. For example:

``` python
::: {.card title="Life Expectancy" padding="3px"}
This is the content.
:::
```

### Value Boxes

[Value Boxes](../../../docs/dashboards/data-display.llms.md#value-boxes) support the following options:

| Option | Description |
|----|----|
| `title` | Title displayed above value |
| `icon` | Icon identifier from [bootstrap icons](https://icons.getbootstrap.com) |
| `color` | Background color—this can be any CSS color or one of the theme specific color aliases (see below) |
| `value` | Main display value |

Available themed aliases for `color` include:

| Color Alias | Default Theme Color(s) |
|-------------|------------------------|
| `primary`   | Blue                   |
| `secondary` | Gray                   |
| `success`   | Green                  |
| `info`      | Bright Blue            |
| `warning`   | Yellow/Orange          |
| `danger`    | Red                    |
| `light`     | Light Gray             |
| `dark`      | Black                  |

Note that value box options can be specified either as cell options or by printing a `dict()` (for Python) or `list()` (for R) (this is helpful when options need to be dynamic). See the [Value Boxes](../../../docs/dashboards/data-display.llms.md#value-boxes) component documentation for details.

## Title & Author

|  |  |
|:---|:---|
| `title` | Document title |
| `subtitle` | Identifies the subtitle of the document. |
| `date` | Document date |
| `date-format` | Date format for the document |
| `author` | Author or authors of the document |
| `order` | Order for document when included in a website automatic sidebar menu. |

## Dashboard

|  |  |
|:---|:---|
| `logo` | Logo image(s) (placed on the left side of the navigation bar) |
| `orientation` | Default orientation for dashboard content (default `rows`) |
| `scrolling` | Use scrolling rather than fill layout (default: `false`) |
| `expandable` | Make card content expandable (default: `true`) |
| `nav-buttons` | Links to display on the dashboard navigation bar |

## Format Options

[TABLE]

## Table of Contents

[TABLE]

## Numbering

[TABLE]

## Layout

[TABLE]

## Code

[TABLE]

## Execution

Execution options should be specified within the `execute` key. For example:

``` yaml
execute:
  echo: false
  warning: false
```

[TABLE]

## Figures

[TABLE]

## Tables

[TABLE]

## References

[TABLE]

## Footnotes

[TABLE]

## Cross-References

|  |  |
|:---|:---|
| `crossref` | Configuration for cross-reference labels and prefixes. See [Cross-Reference Options](https://quarto.org/docs/reference/metadata/crossref.llms.md) for more details. |
| `crossrefs-hover` | Enables a hover popup for cross references that shows the item being referenced. |

## Citation

[TABLE]

## Language

[TABLE]

## Includes

[TABLE]

## Metadata

|  |  |
|:---|:---|
| `keywords` | List of keywords to be included in the document metadata. |
| `pagetitle` | Sets the title metadata for the document |
| `title-prefix` | Specify STRING as a prefix at the beginning of the title that appears in the HTML header (but not in the title as it appears at the beginning of the body) |
| `description-meta` | Sets the description metadata for the document |
| `author-meta` | Sets the author metadata for the document |
| `date-meta` | Sets the date metadata for the document |

## Rendering

|  |  |
|:---|:---|
| `from` | Format to read from. Extensions can be individually enabled or disabled by appending +EXTENSION or -EXTENSION to the format name (e.g. markdown+emoji). |
| `output-file` | Output file to write to |
| `output-ext` | Extension to use for generated output file |
| `template` | Use the specified file as a custom template for the generated document. |
| `template-partials` | Include the specified files as partials accessible to the template for the generated content. |
| `embed-resources` | Produce a standalone HTML file with no external dependencies, using `data:` URIs to incorporate the contents of linked scripts, stylesheets, images, and videos. The resulting file should be “self-contained,” in the sense that it needs no external files and no net access to be displayed properly by a browser. This option works only with HTML output formats, including `html4`, `html5`, `html+lhs`, `html5+lhs`, `s5`, `slidy`, `slideous`, `dzslides`, and `revealjs`. Scripts, images, and stylesheets at absolute URLs will be downloaded; those at relative URLs will be sought relative to the working directory (if the first source file is local) or relative to the base URL (if the first source file is remote). Elements with the attribute `data-external="1"` will be left alone; the documents they link to will not be incorporated in the document. Limitation: resources that are loaded dynamically through JavaScript cannot be incorporated; as a result, some advanced features (e.g. zoom or speaker notes) may not work in an offline “self-contained” `reveal.js` slide show. |
| `self-contained-math` | Embed math libraries (e.g. MathJax) within `self-contained` output. Note that math libraries are not embedded by default because they are quite large and often time consuming to download. |
| `filters` | Specify executables or Lua scripts to be used as a filter transforming the pandoc AST after the input is parsed and before the output is written. |
| `shortcodes` | Specify Lua scripts that implement shortcode handlers |
| `keep-md` | Keep the markdown file generated by executing code |
| `keep-ipynb` | Keep the notebook file generated from executing code. |
| `ipynb-filters` | Filters to pre-process ipynb files before rendering to markdown |
| `ipynb-shell-interactivity` | Specify which nodes should be run interactively (displaying output from expressions) |
| `plotly-connected` | If true, use the “notebook_connected” plotly renderer, which downloads its dependencies from a CDN and requires an internet connection to view. |
| `extract-media` | Extract images and other media contained in or linked from the source document to the path DIR, creating it if necessary, and adjust the images references in the document so they point to the extracted files. Media are downloaded, read from the file system, or extracted from a binary container (e.g. docx), as needed. The original file paths are used if they are relative paths not containing … Otherwise filenames are constructed from the SHA1 hash of the contents. |
| `resource-path` | List of paths to search for images and other resources. |
| `default-image-extension` | Specify a default extension to use when image paths/URLs have no extension. This allows you to use the same source for formats that require different kinds of images. Currently this option only affects the Markdown and LaTeX readers. |
| `abbreviations` | Specifies a custom abbreviations file, with abbreviations one to a line. This list is used when reading Markdown input: strings found in this list will be followed by a nonbreaking space, and the period will not produce sentence-ending space in formats like LaTeX. The strings may not contain spaces. |
| `dpi` | Specify the default dpi (dots per inch) value for conversion from pixels to inch/ centimeters and vice versa. (Technically, the correct term would be ppi: pixels per inch.) The default is `96`. When images contain information about dpi internally, the encoded value is used instead of the default specified by this option. |
| `html-table-processing` | If `none`, do not process tables in HTML input. |

## Text Output

|  |  |
|:---|:---|
| `strip-comments` | Strip out HTML comments in the Markdown source, rather than passing them on to Markdown, Textile or HTML output as raw HTML. This does not apply to HTML comments inside raw HTML blocks when the `markdown_in_html_blocks` extension is not set. |
| `ascii` | Use only ASCII characters in output. Currently supported for XML and HTML formats (which use entities instead of UTF-8 when this option is selected), CommonMark, gfm, and Markdown (which use entities), roff ms (which use hexadecimal escapes), and to a limited degree LaTeX (which uses standard commands for accented characters when possible). roff man output uses ASCII by default. |
