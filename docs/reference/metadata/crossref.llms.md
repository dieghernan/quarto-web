# Cross Reference Options

The `crossref` option is used to customize the appearance and behavior of cross-references. You can read more about using [Cross-References in the Guide](../../../docs/authoring/cross-references.llms.md).

``` yaml
---
crossref:
  labels: roman
  title-delim: "-"
---
```

## Crossref

|  |  |
|:---|:---|
| `custom` | A custom cross reference type. See [Custom](https://quarto.org/docs/reference/metadata/crossref.llms.md#custom) for more details. |
| `chapters` | Use top level sections (H1) in this document as chapters. |
| `title-delim` | The delimiter used between the prefix and the caption. |
| `fig-title` | The title prefix used for figure captions. |
| `tbl-title` | The title prefix used for table captions. |
| `eq-title` | The title prefix used for equation captions. |
| `lst-title` | The title prefix used for listing captions. |
| `thm-title` | The title prefix used for theorem captions. |
| `lem-title` | The title prefix used for lemma captions. |
| `cor-title` | The title prefix used for corollary captions. |
| `prp-title` | The title prefix used for proposition captions. |
| `cnj-title` | The title prefix used for conjecture captions. |
| `def-title` | The title prefix used for definition captions. |
| `exm-title` | The title prefix used for example captions. |
| `exr-title` | The title prefix used for exercise captions. |
| `fig-prefix` | The prefix used for an inline reference to a figure. |
| `tbl-prefix` | The prefix used for an inline reference to a table. |
| `eq-prefix` | The prefix used for an inline reference to an equation. |
| `sec-prefix` | The prefix used for an inline reference to a section. |
| `lst-prefix` | The prefix used for an inline reference to a listing. |
| `thm-prefix` | The prefix used for an inline reference to a theorem. |
| `lem-prefix` | The prefix used for an inline reference to a lemma. |
| `cor-prefix` | The prefix used for an inline reference to a corollary. |
| `prp-prefix` | The prefix used for an inline reference to a proposition. |
| `cnj-prefix` | The prefix used for an inline reference to a conjecture. |
| `def-prefix` | The prefix used for an inline reference to a definition. |
| `exm-prefix` | The prefix used for an inline reference to an example. |
| `exr-prefix` | The prefix used for an inline reference to an exercise. |
| `fig-labels` | The numbering scheme used for figures. |
| `tbl-labels` | The numbering scheme used for tables. |
| `eq-labels` | The numbering scheme used for equations. |
| `sec-labels` | The numbering scheme used for sections. |
| `lst-labels` | The numbering scheme used for listings. |
| `thm-labels` | The numbering scheme used for theorems. |
| `lem-labels` | The numbering scheme used for lemmas. |
| `cor-labels` | The numbering scheme used for corollaries. |
| `prp-labels` | The numbering scheme used for propositions. |
| `cnj-labels` | The numbering scheme used for conjectures. |
| `def-labels` | The numbering scheme used for definitions. |
| `exm-labels` | The numbering scheme used for examples. |
| `exr-labels` | The numbering scheme used for exercises. |
| `lof-title` | The title used for the list of figures. |
| `lot-title` | The title used for the list of tables. |
| `lol-title` | The title used for the list of listings. |
| `labels` | The number scheme used for references. |
| `subref-labels` | The number scheme used for sub references. |
| `ref-hyperlink` | Whether cross references should be hyper-linked. |
| `appendix-title` | The title used for appendix. |
| `appendix-delim` | The delimiter beween appendix number and title. |

## Custom

Use the `custom` option to `crossref` to define new types of cross reference. For example:

``` yaml
---
crossref:
  custom:
    - key: vid
      kind: float
      reference-prefix: Video
---
```

|  |  |
|:---|:---|
| `kind` | The kind of cross reference (currently only “float” is supported). |
| `reference-prefix` | The prefix used in rendered references when referencing this type. |
| `caption-prefix` | The prefix used in rendered captions when referencing this type. If omitted, the field `reference-prefix` is used. |
| `space-before-numbering` | If false, use no space between crossref prefixes and numbering. |
| `key` | The key used to prefix reference labels of this type, such as “fig”, “tbl”, “lst”, etc. |
| `latex-env` | In LaTeX output, the name of the custom environment to be used. |
| `latex-list-of-file-extension` | In LaTeX output, the extension of the auxiliary file used by LaTeX to collect names to be used in the custom “list of” command. If omitted, a string with prefix `lo` and suffix with the value of `ref-type` is used. |
| `latex-list-of-description` | The description of the crossreferenceable object to be used in the title of the “list of” command. If omitted, the field `reference-prefix` is used. |
| `caption-location` | The location of the caption relative to the crossreferenceable content. |
