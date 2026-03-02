# Brand

The `brand` option is used to define cross-format branding. You can read more about using [Brand in the Guide](../../../docs/authoring/brand.llms.md).

Set brand options in the `_brand.yml` file:

``` yaml
color:
  palette:
    blue: "#1c84e5"
  foreground: blue
```

You can also specify brand options in a document header under `brand`:

``` yaml
---
brand:
  color:
    palette:
      blue: "#1c84e5"
    foreground: blue
---
```

## Brand

|  |  |
|:---|:---|
| `meta` | Metadata for a brand, including the brand name and important links. See [Meta](#meta) for more information. |
| `logo` | Provide definitions and defaults for brand’s logo in various formats and sizes. See [Logo](#logo) for more information. |
| `color` | The brand’s custom color palette and theme. See [Color](#color) for more information. |
| `typography` | Typography definitions for the brand. See [Typography](#typography) for more information. |
| `defaults` | Default settings |

## Meta

|  |  |
|:---|:---|
| `name` | The brand name. |
| `link` | Important links for the brand, including social media links. If a single string, it is the brand’s home page or website. Additional fields are allowed for internal use. |

## Logo

|  |  |
|:---|:---|
| `images` | A dictionary of named logo resources. |
| `small` | A link or path to the brand’s small-sized logo or icon, or a link or path to both the light and dark versions. |
| `medium` | A link or path to the brand’s medium-sized logo, or a link or path to both the light and dark versions. |
| `large` | A link or path to the brand’s large- or full-sized logo, or a link or path to both the light and dark versions. |

## Color

|  |  |
|:---|:---|
| `palette` | The brand’s custom color palette. Any number of colors can be defined, each color having a custom name. |
| `foreground` | The foreground color, used for text. |
| `background` | The background color, used for the page background. |
| `primary` | The primary accent color, i.e. the main theme color. Typically used for hyperlinks, active states, primary action buttons, etc. |
| `secondary` | The secondary accent color. Typically used for lighter text or disabled states. |
| `tertiary` | The tertiary accent color. Typically an even lighter color, used for hover states, accents, and wells. |
| `success` | The color used for positive or successful actions and information. |
| `info` | The color used for neutral or informational actions and information. |
| `warning` | The color used for warning or cautionary actions and information. |
| `danger` | The color used for errors, dangerous actions, or negative information. |
| `light` | A bright color, used as a high-contrast foreground color on dark elements or low-contrast background color on light elements. |
| `dark` | A dark color, used as a high-contrast foreground color on light elements or high-contrast background color on light elements. |
| `link` | The color used for hyperlinks. If not defined, the `primary` color is used. |

## Typography

|  |  |
|:---|:---|
| `fonts` | Font files and definitions for the brand. See [Font resource definitions](#font-resource-definitions) for more information. |
| `base` | The base font settings for the brand. These are used as the default for all text. See [base](#base) for more information. |
| `headings` | Settings for headings, or a string specifying the font family only. See [headings-unified](#headings-unified) for more information. |
| `monospace` | Settings for monospace text, or a string specifying the font family only. See [monospace-unified](#monospace-unified) for more information. |
| `monospace-inline` | Settings for inline code, or a string specifying the font family only. See [monospace-inline-unified](#monospace-inline-unified) for more information. |
| `monospace-block` | Settings for code blocks, or a string specifying the font family only. See [monospace-block-unified](#monospace-block-unified) for more information. |
| `link` | Settings for links. See [link-unified](#link-unified) for more information. |

### Font resource definitions

#### google

|  |  |
|:---|:---|
| `source` | `"google"` |
| `family` | The font family name, which must match the name of the font on the foundry website. |
| `weight` | The font weights to include. |
| `style` | The font styles to include. |
| `display` | The font display method, determines how a font face is font face is shown depending on its download status and readiness for use. |

#### bunny

|  |  |
|:---|:---|
| `source` | `"bunny"` |
| `family` | The font family name, which must match the name of the font on the foundry website. |
| `weight` | The font weights to include. |
| `style` | The font styles to include. |
| `display` | The font display method, determines how a font face is font face is shown depending on its download status and readiness for use. |

#### file

|  |  |
|:---|:---|
| `source` | `"file"` |
| `family` | The font family name. |
| `files` | The font files to include. These can be local or online. Local file paths should be relative to the `brand.yml` file. Online paths should be complete URLs. |

#### system

|  |  |
|:---|:---|
| `source` | `"system"` |
| `family` | The font family name, which must match the name of the font on the foundry website. |
| `weight` | The font weights to include. |
| `style` | The font styles to include. |
| `display` | The font display method, determines how a font face is font face is shown depending on its download status and readiness for use. |

#### common

|  |  |
|:---|:---|
| `family` | The font family name, which must match the name of the font on the foundry website. |
| `weight` | The font weights to include. |
| `style` | The font styles to include. |
| `display` | The font display method, determines how a font face is font face is shown depending on its download status and readiness for use. |

### base

|               |                                     |
|:--------------|:------------------------------------|
| `family`      | The font family.                    |
| `size`        | The font size.                      |
| `weight`      | The font weight.                    |
| `line-height` | The distance between lines of text. |

### headings-unified

|               |                                     |
|:--------------|:------------------------------------|
| `family`      | The font family.                    |
| `weight`      | The font weight.                    |
| `style`       | The font style.                     |
| `color`       | The text color.                     |
| `line-height` | The distance between lines of text. |

### monospace-unified

|                    |                            |
|:-------------------|:---------------------------|
| `family`           | The font family.           |
| `size`             | The font size.             |
| `weight`           | The font weight.           |
| `color`            | The text color.            |
| `background-color` | The text background color. |

### monospace-inline-unified

|                    |                            |
|:-------------------|:---------------------------|
| `family`           | The font family.           |
| `size`             | The font size.             |
| `weight`           | The font weight.           |
| `color`            | The text color.            |
| `background-color` | The text background color. |

### monospace-block-unified

|                    |                                     |
|:-------------------|:------------------------------------|
| `family`           | The font family.                    |
| `size`             | The font size.                      |
| `weight`           | The font weight.                    |
| `color`            | The text color.                     |
| `background-color` | The text background color.          |
| `line-height`      | The distance between lines of text. |

### link-unified

|                    |                                     |
|:-------------------|:------------------------------------|
| `weight`           | The font weight.                    |
| `color`            | The text color.                     |
| `background-color` | The text background color.          |
| `decoration`       | The text decoration, i.e. underline |
