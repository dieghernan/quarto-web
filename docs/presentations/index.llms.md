# Presentations

## Overview

Quarto supports a variety of formats for creating presentations, including:

- `revealjs` — [reveal.js](../../docs/presentations/revealjs/index.llms.md) (HTML)

- `pptx` — [PowerPoint](../../docs/presentations/powerpoint.llms.md) (MS Office)

- `beamer` — [Beamer](../../docs/presentations/beamer.llms.md) (LaTeX/PDF)

There are pros and cons to each of these formats. The most capable format by far is `revealjs`, so it is highly recommended unless you have specific Office or LaTeX output requirements. Note that `revealjs` presentations can be presented as HTML slides or can be printed to PDF for easier distribution.

Below, we’ll describe the basic syntax for presentations that applies to all formats. See the format-specific articles for additional details on their native capabilities.

## Creating Slides

In markdown, slides are delineated using headings. For example, here is a simple slide show with two slides (each defined with a level 2 heading (`##`)):

``` markdown
---
title: "Habits"
author: "John Doe"
format: revealjs
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
format: revealjs
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
format: revealjs
---

- Turn off alarm
- Get out of bed

---

- Get in bed
- Count sheep
```

The examples above all use level 2 headings for slides and level 1 headings for sections/title slides. You can customize this using the `slide-level` option (See the Pandoc documentation on [structuring the slide show](https://pandoc.org/MANUAL.llms.md#structuring-the-slide-show) for additional details).

## Incremental Lists

By default number and bullet lists within slides are displayed all at once. You can override this globally using the `incremental` option. For example:

``` yaml
title: "My Presentation"
format:
  revealjs:
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

## Learning More

See these format-specific articles for additional details on the additional capabilities of each format:

- `revealjs` — [reveal.js](../../docs/presentations/revealjs/index.llms.md) (HTML)

- `pptx` — [PowerPoint](../../docs/presentations/powerpoint.llms.md) (MS Office)

- `beamer` — [Beamer](../../docs/presentations/beamer.llms.md) (LaTeX/PDF)
