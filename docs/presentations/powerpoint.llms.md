# PowerPoint

## Overview

You can create [PowerPoint](https://en.wikipedia.org/wiki/Microsoft_PowerPoint) presentations using the `pptx` format. PowerPoint presentations support core presentation features like incremental bullets, 2-column layouts, and speaker notes, and can also be rendered using custom [PowerPoint templates](#powerpoint-templates).

See the PowerPoint [format reference](../../docs/reference/formats/presentations/pptx.llms.md) for a complete list of all options available for PowerPoint output.

## Creating Slides

In markdown, slides are delineated using headings. For example, here is a simple slide show with two slides (each defined with a level 2 heading (`##`)):

``` markdown
---
title: "Habits"
author: "John Doe"
format: pptx
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
format: pptx
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
format: pptx
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
  pptx:
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

To put material in side by side columns, you can use a native div container with class `.columns`, containing two or more div containers with class `.column`:

``` markdown
:::: {.columns}

::: {.column}
contents...
:::

::: {.column}
contents...
:::

::::
```

## Speaker Notes

You can add speaker notes to a slide using a div with class `.notes`. For example:

``` markdown
## Slide with speaker notes

Slide content

::: {.notes}
Speaker notes go here.
:::
```

## PowerPoint Templates

By default PowerPoint output uses a fairly plain looking template. You can customize what template is used via the `reference-doc` option. For example:

``` yaml
---
title: "Presentation"
format:
  pptx:
    reference-doc: template.pptx
---
```

Nearly all templates included with recent versions of PowerPoint (either with `.pptx` or `.potx` extension) are known to work, as are most templates derived from these.

The specific requirement is that the template should contain layouts with the following names (as seen within PowerPoint, click on `Layout` under the `Home` menu to check):

- Title Slide
- Title and Content
- Section Header
- Two Content
- Comparison
- Content with Caption
- Blank

For each name, the first layout found with that name will be used. If no layout is found with one of the names, Pandoc will output a warning and use the layout with that name from the default `reference-doc` instead.

### Creating a Template

To create a template from scratch, start with the default PowerPoint template as follows:

``` bash
quarto pandoc -o template.pptx --print-default-data-file reference.pptx 
```

Then edit the `template.pptx` file within PowerPoint as desired, and use it as the value for `reference-doc` (as shown above) when rendering your slides:

## Slide Layouts

When creating slides, the pptx writer chooses from a number of pre-defined layouts, based on the content of the slide:

**Title Slide**  
This layout is used for the initial slide, which is generated and filled from the metadata fields `date`, `author`, and `title`, if they are present.

**Section Header**  
This layout is used for what pandoc calls “title slides”, i.e. slides which start with a header which is above the slide level in the hierarchy.

**Two Content**  
This layout is used for two-column slides, i.e. slides containing a div with class `columns` which contains at least two divs with class `column`.

**Comparison**  
This layout is used instead of “Two Content” for any two-column slides in which at least one column contains text followed by non-text (e.g. an image or a table).

**Content with Caption**  
This layout is used for any non-two-column slides which contain text followed by non-text (e.g. an image or a table).

**Blank**  
This layout is used for any slides which only contain blank content, e.g. a slide containing only speaker notes, or a slide containing only a non-breaking space.

**Title and Content**  
This layout is used for all slides which do not match the criteria for another layout.

These layouts are chosen from the default `pptx` reference doc included with Pandoc, unless an alternative reference doc is specified using `reference-doc`.

## Background Images

To provide a common background image for multiple slides in a PowerPoint presentation, include the background image within the relevant slide layouts of a custom PowerPoint template (see [Creating a Template](#creating-a-template) for details on creating templates).

To add a background image to an individual slide, add the `background-image` attribute to the slide’s heading. For example:

``` markdown
## Slide Title {background-image="background.png"}
```

Note that this also works even if you don’t have slide heading text. For example:

``` markdown
## {background-image="background.png"}
```

For background images, only the “stretch” mode is supported, and the background image is centred around the slide in the image’s larger axis, matching the observed default behaviour of PowerPoint.
