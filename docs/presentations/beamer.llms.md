# Beamer

## Overview

You can create [Beamer](https://ctan.org/pkg/beamer) (LaTeX/PDF) presentations using the `beamer` format. Beamer presentations support core presentation features like incremental content and 2-column layouts, and also provide facilities for customizing column layout, specifying frame attributes, and using Beamer themes.

By default, the Beamer format has `echo: false` and `warning: false`. As a result, executable code cells in standard Beamer documents won’t show their source or warnings generated. As with other options, you can override this behavior in the document metadata or individually in each executable cell.

See the Beamer [format reference](../../docs/reference/formats/presentations/beamer.llms.md) for a complete list of all options available for Beamer output.

## Creating Slides

In markdown, slides are delineated using headings. For example, here is a simple slide show with two slides (each defined with a level 2 heading (`##`)):

``` markdown
---
title: "Habits"
author: "John Doe"
format: beamer
---

## Getting up

- Turn off alarm
- Get out of bed

## Going to sleep

- Get in bed
- Count sheep
```

You can also divide slide shows into sections with title slides using a level 1 heading (`#`). For example:

``` markdown
---
title: "Habits"
author: "John Doe"
format: beamer
---

# In the morning

## Getting up

- Turn off alarm
- Get out of bed

## Breakfast

- Eat eggs
- Drink coffee

# In the evening

## Dinner

- Eat spaghetti
- Drink wine

## Going to sleep

- Get in bed
- Count sheep
```

Finally, you can also delineate slides using horizontal rules (for example, if you have a slide without a title):

``` markdown
---
title: "Habits"
author: "John Doe"
format: beamer
---

- Turn off alarm
- Get out of bed

---

- Get in bed
- Count sheep
```

The examples above all use level 2 headings for slides and level 1 headings for sections/title slides. You can customize this using the `slide-level` option (See the Pandoc documentation on [structuring the slide show](https://pandoc.org/MANUAL.llms.md#structuring-the-slide-show) for additional details).

In Beamer, headings below `slide-level` will place content inside a `block` environment:

``` markdown
---
title: "Habits"
author: "John Doe"
format: 
  beamer:
    slide-level: 2
---

## Slide

### Simple block

Content
```

Add the `.alert` or `.example` class to place content inside an `alertblock` or `exampleblock` environment respectively:

``` markdown
---
title: "Habits"
author: "John Doe"
format: 
  beamer:
    slide-level: 2
---

## Slide

### Alert block {.alert}

Content

### Example block {.example}

Content
```

## Incremental Lists

By default number and bullet lists within slides are displayed all at once. You can override this globally using the `incremental` option. For example:

``` yaml
title: "My Presentation"
format:
  beamer:
    incremental: true   
```

You can also explicitly make any list incremental or non-incremental by surrounding it in a div with an explicit class that determines the mode. To make a list incremental do this:

``` markdown
::: {.incremental}

- Eat spaghetti
- Drink wine

:::
```

To make a list non-incremental do this:

``` markdown
::: {.nonincremental}

- Eat spaghetti
- Drink wine

:::
```

You can also insert a pause within a slide (keeping the content after the pause hidden) by inserting three dots separated by spaces:

``` markdown
## Slide with a pause

content before the pause

. . .

content after the pause
```

Note this only works below headings that are creating slides (see [Creating slides](#creating-slides)).

## Multiple Columns

To put material in side by side columns, you can use a native div container with class `.columns`, containing two or more div containers with class `.column`and a `width` attribute:

``` markdown
:::: {.columns}

::: {.column width="40%"}
contents...
:::

::: {.column width="60%"}
contents...
:::

::::
```

The div containers with classes `columns` and `column` can optionally have an `align` attribute. The class `columns` can optionally have a `totalwidth` attribute or an `onlytextwidth` class.

``` markdown
:::: {.columns align=center totalwidth=8em}

::: {.column width="40%"}
contents...
:::

::: {.column width="60%" align=bottom}
contents...
:::

:::: 
```

The `align` attributes on `columns` and `column` can be used with the values `top`, `top-baseline`, `center` and `bottom` to vertically align the columns. It defaults to `top` in `columns`.

The `totalwidth` attribute limits the width of the columns to the given value.

``` markdown
::::  {.columns align=top .onlytextwidth}

::: {.column width="40%" align=center}
contents...
:::

::: {.column width="60%"}
contents...
:::

:::: 
```

The class `onlytextwidth` sets the `totalwidth` to `\textwidth`.

See Section 12.7 of the [Beamer User’s Guide](http://mirrors.ctan.org/macros/latex/contrib/beamer/doc/beameruserguide.pdf) for more details.

### Panel Layout

In addition to using the presentation-native `columns`/`column` syntax described above, you can also use Quarto’s [panel layout](../../docs/authoring/figures.llms.md#complex-layouts) features using divs with the `layout` class. Quarto will convert those to Beamer columns as if they were written with the above syntax.

## Beamer Options

Set additional options to change the appearance of PDF slides using `beamer`:

``` yaml
---
title: "Presentation"
format: 
  beamer: 
    aspectratio: 32
    navigation: horizontal
    theme: AnnArbor
    colortheme: lily
---
```

The options available are:

| Option | Description |
|----|----|
| `aspectratio` | Slide aspect ratio: `43` for 4:3 \[default\], `169` for 16:9, `1610` for 16:10, `149` for 14:9, `141` for 1.41:1, `54` for 5:4, `32` for 3:2 |
| `beamerarticle` | Produce an article from Beamer slides |
| `beameroption` | Extra beamer options provided to `\setbeameroption{}` |
| `institute` | Author affiliations: can be a list when there are multiple authors |
| `logo` | Logo image for slides |
| `navigation` | Controls navigation symbols (default is `empty` for no navigation symbols; other valid values are `frame`, `vertical`, and `horizontal`) |
| `section-titles` | Enables “title pages” for new sections (default is true) |
| `theme, colortheme, fonttheme, innertheme, outertheme` | Beamer themes |
| `themeoptions` | Options for LaTeX beamer themes (a list) |
| `titlegraphic` | Image for title slide |

## Frame Attributes

Sometimes it is necessary to add the LaTeX `[fragile]` option to a frame in beamer (for example, when using the `minted` environment). This can be forced by adding the `fragile` class to the heading introducing the slide:

``` markdown
# Fragile slide {.fragile}
```

All of the other frame attributes described in Section 8.1 of the [Beamer User’s Guide](http://mirrors.ctan.org/macros/latex/contrib/beamer/doc/beameruserguide.pdf) may also be used: `allowdisplaybreaks`, `allowframebreaks`, `b`, `c`, `t`, `environment`, `label`, `plain`, `shrink`, `standout`, `noframenumbering`.

## Background Images

To provide a common background image for all slides in a Beamer presentation, use the `background-image` format option. For example:

``` yaml
---
format:
  beamer:
    background-image: background.png
---    
```
