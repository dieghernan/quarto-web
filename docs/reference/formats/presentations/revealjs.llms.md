# Revealjs Options

Revealjs is an open source HTML presentation framework. To learn more about Revealjs see <https://revealjs.com/>.

See the Revealjs format [user guide](../../../../docs/presentations/revealjs/index.llms.md) for more details on creating Revealjs output with Quarto.

``` yaml
format: revealjs
```

## Title & Author

|  |  |
|:---|:---|
| `title` | Document title |
| `subtitle` | Identifies the subtitle of the document. |
| `date` | Document date |
| `date-format` | Date format for the document |
| `author` | Author or authors of the document |
| `institute` | Author affiliations for the presentation. |
| `order` | Order for document when included in a website automatic sidebar menu. |

## Format Options

[TABLE]

## Table of Contents

[TABLE]

## Numbering

[TABLE]

## Slides

[TABLE]

## Slide Content

[TABLE]

## Slide Tools

|               |                                                     |
|:--------------|:----------------------------------------------------|
| `overview`    | Enable the slide overview mode                      |
| `menu`        | Configuration for revealjs menu.                    |
| `chalkboard`  | Configuration for revealjs chalkboard.              |
| `multiplex`   | Configuration for reveal presentation multiplexing. |
| `scroll-view` | Control the scroll view feature of Revealjs         |

## Transitions

|  |  |
|:---|:---|
| `transition` | Transition style for slides backgrounds. (`none`, `fade`, `slide`, `convex`, `concave`, or `zoom`) |
| `transition-speed` | Slide transition speed (`default`, `fast`, or `slow`) |
| `background-transition` | Transition style for full page slide backgrounds. (`none`, `fade`, `slide`, `convex`, `concave`, or `zoom`) |
| `fragments` | Turns fragments on and off globally |
| `auto-animate` | Globally enable/disable auto-animate (enabled by default) |
| `auto-animate-easing` | Default CSS easing function for auto-animation. Can be overridden per-slide or per-element via attributes. |
| `auto-animate-duration` | Duration (in seconds) of auto-animate transition. Can be overridden per-slide or per-element via attributes. |
| `auto-animate-unmatched` | Auto-animate unmatched elements. Can be overridden per-slide or per-element via attributes. |
| `auto-animate-styles` | CSS properties that can be auto-animated (positional styles like top, left, etc. are always animated). |

## Navigation

[TABLE]

## Print to PDF

|  |  |
|:---|:---|
| `pdf-max-pages-per-slide` | Slides that are too tall to fit within a single page will expand onto multiple pages. You can limit how many pages a slide may expand to using this option. |
| `pdf-separate-fragments` | Prints each fragment on a separate slide |
| `pdf-page-height-offset` | Offset used to reduce the height of content within exported PDF pages. This exists to account for environment differences based on how you print to PDF. CLI printing options, like phantomjs and wkpdf, can end on precisely the total height of the document whereas in-browser printing has to end one pixel before. |

## Media

[TABLE]

## Slide Layout

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

## Links

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

## Library

|                |                                       |
|:---------------|:--------------------------------------|
| `revealjs-url` | Directory containing reveal.js files. |
