# Revealjs

## Overview

You can create [Revealjs](https://revealjs.com/) presentations using the `revealjs` format. The best way to get a sense for the capabilities of Revealjs is this [demo](demo/) presentation:

If you prefer to view the demo in a standalone browser you can do that [here](demo/). Check out the [source code](https://github.com/quarto-dev/quarto-web/blob/main/docs/presentations/revealjs/demo/index.qmd) for the demo to see how the slides were created.

See the Revealjs [format reference](../../../docs/reference/formats/presentations/revealjs.llms.md) for a comprehensive overview of all options supported for Revealjs output.

## Creating Slides

In markdown, slides are delineated using headings. For example, here is a simple slide show with two slides (each defined with a level 2 heading (`##`):

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

The examples above all use level 2 headings for slides and level 1 headings for sections/title slides. You can customize this using the `slide-level` option (See the Pandoc documentation on [structuring the slide show](https://pandoc.org/MANUAL.llms.md#structuring-the-slide-show) for additional details.

### Title Slide

You’ll notice in the above examples that a title slide is automatically created based on the `title` and `author` provided in the document YAML options. However, sometimes you don’t want an explicit title slide (e.g. if your first slide consists entirely of a background image). It’s perfectly valid to create a presentation without a title slide, just exclude the `title` and `author` options:

``` markdown
---
format: revealjs
---

## Getting up

- Turn off alarm
- Get out of bed

## Going to sleep

- Get in bed
- Count sheep
```

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

You can also insert a pause within a slide (keeping the content after the pause hidden) by inserting three dots separated by spaces:

``` markdown
## Slide with a pause

content before the pause

. . .

content after the pause
```

Note this only works below headings that are creating slides (see [Creating slides](#creating-slides)).

## Multiple Columns

To put material in side by side columns, you can use a native div container with class `.columns`, containing two or more div containers with class `.column` and a `width` attribute:

``` markdown
:::: {.columns}

::: {.column width="40%"}
Left column
:::

::: {.column width="60%"}
Right column
:::

::::
```

## Content Overflow

If you have a slide that has more content than can be displayed on a single frame there are two slide-level classes you can apply to mitigate this:

1.  Use the `.smaller` class to use a smaller typeface so that more text fits on the slide. For example:

    ``` markdown
    ## Slide Title {.smaller}
    ```

2.  Use the `.scrollable` class to make off-slide content available by scrolling. For example:

    ``` markdown
    ## Slide Title {.scrollable}
    ```

Both of these options can also be applied globally to all slides as follows:

``` yaml
---
format:
  revealjs:
    smaller: true
    scrollable: true
---
```

Please note that section title slides are centered by default which prevents them from being scrollable. If you want to make title slides scrollable, you need to make them non-centered.

``` yaml
---
format:
  revealjs:
    scrollable: true
    center-title-slide: false
---
```

> **NOTE:**
>
> When a slide is [scrollable](../../../docs/presentations/revealjs/index.llms.md#content-overflow) the image size calculations used by [auto-stretch](../../../docs/presentations/revealjs/advanced.llms.md#stretch) may not work well and images may not appear. Two solutions depending on your needs are:
>
> - Disable auto-stretch at the presentation level, `auto-stretch: false`, and use `.r-stretch` on individual images only where needed.
>
> - On slides that are scrollable, add the `.nostretch` class to disable auto-stretch on the slide.

## Speaker Notes

You can add speaker notes to a slide using a div with class `.notes`. For example:

``` markdown
## Slide with speaker notes

Slide content

::: {.notes}
Speaker notes go here.
:::
```

This is a Revealjs feature from [built-in plugin](https://revealjs.com/plugins/#built-in-plugins) which brings limitation: the content cannot rely on external dependencies. For instance, if you want to include a mermaid diagram that typically needs mermaid.js, it will need to be embed as an SVG or PNG image.

Press the S key (or use the [Navigation Menu](../../../docs/presentations/revealjs/presenting.llms.md#navigation-menu)) to show the presentation speaker view:

![Screenshot of reveal.js presentation in Speaker View. On the right, the active slide is shown. The left column contains three sections which show (from top to bottom): the upcoming slide, time (both elapsed and clock time), and a section where speaker notes go.](images/speaker-view.png)

You’ll typically use this view on one screen (e.g. your laptop) while presenting the slides on another screen.

## Themes

There are 11 built-in themes provided for Reveal presentations (you can also create your own themes). The `default` and `dark` themes use fairly classic typography and color schemes and are a good place to start.

The `default` theme is used automatically — use the `theme` option to switch to an alternate theme. For example

``` yaml
---
title: "Presentation"
format:
  revealjs: 
    theme: dark
---
```

Here is the full list of available themes:

- `beige`
- `blood`
- `dark`
- `default`
- `dracula`
- `league`
- `moon`
- `night`
- `serif`
- `simple`
- `sky`
- `solarized`

See the article on [Reveal Themes](../../../docs/presentations/revealjs/themes.llms.md) for additional details on customizing themes and creating brand new themes of your own.

## Asides & Footnotes

Asides contain content of more peripheral interest, and are displayed in a smaller, lighter font at the bottom of the slide. Creates asides using a div with the `aside` class. For example:

``` markdown
## Slide Title

Slide content

::: aside
Some additional commentary of more peripheral interest.
:::
```

Footnotes have a similar visual treatment to asides, but include a footnote number. For example, here we use a footnote and an aside on a single slide:

``` markdown
## Slide Title

- Green ^[A footnote]
- Brown
- Purple

::: aside
Some additional commentary of more peripheral interest.
:::
```

Which looks like this when rendered:

![Rendered slide with title at the top, followed by a bulleted list (the first item of which has a footnote). The bottom of the slide shows the aside (Some additional commentary of more peripheral interest.), and below that the footnote.](images/footnote.png)

If you prefer that footnotes be included at the end of the document, specify the `reference-location: document` option:

``` yaml
---
format:
  revealjs:
    reference-location: document
---
```

Note that when specifying this option footnotes can still be viewed while on the slide by hovering over the footnote number.

## Footer & Logo

You can include footer text and a logo at the bottom of each slide using the `footer` and `logo` options. For example:

``` yaml
---
format:
  revealjs:
    logo: logo.png
    footer: "Footer text"
---
```

Using `{footer=false}` on a slide heading allows to remove the presentation footer for this slide.

``` yaml
---
format:
  revealjs:
    footer: "Footer text"
---

## Slide with default footer

Content

## No footer {footer=false}

No footer is shown on this slide
```

You can also include a custom footer per-slide by adding a footer div at the bottom of the slide.

``` markdown
## Slide Title

Slide content

::: footer
Custom footer text
:::
```

## Code Blocks

Most of the core capabilities of Quarto [HTML Code Blocks](../../../docs/output-formats/html-code.llms.md) are available for Reveal slides, including code folding, code copy, and the ability to pick a custom syntax highlighting theme. Note that if you choose a dark Reveal theme then the default Quarto dark syntax highlighting theme will be used.

### Line Highlighting

You may want to highlight specific lines of code output (or even highlight distinct lines over a progression of steps). You can do this using the `code-line-numbers` attribute of code blocks. For example:

```` java
```{.python code-line-numbers="6-8"}
import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

Note that you can also highlight disparate ranges of lines by separating them with a comma. For example:

```` java
```{.python code-line-numbers="7,9"}
import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

Finally, you can highlight different line ranges progressively by separating them with `|`. For example, here we start by showing all lines, then progress to highlighting line 6, and finally to highlighting line 9:

```` java
```{.python code-line-numbers="|6|9"}
import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

You can use this same option within an executable code cell by using the `code-line-numbers` cell options:

```` java
```{python}
#| code-line-numbers: "|6|9"

import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

### Code Block Height

By default, code blocks are limited to a maximum height of 500px. Code that exceeds this height introduces a scrollbar. To avoid a scrollbar you can increase the maximum height with the `code-block-height` option:

``` yaml
---
format:
  revealjs: 
    code-block-height: 650px
---
```

## Executable Code

You can include the output of executable code blocks on slides just the same as with other Quarto documents. This works essentially the same for slides as it does for other formats, however there are a couple of special considerations for slides covered below.

### Figure Size

You will frequently need to customize the size of figures created for slides so that they either fill the entire slide or whatever region of the slide you need them to. Quarto provides some help here: for Python the figure sizes for [Matplotlib](https://matplotlib.org/) and [Plotly Express](https://plotly.com/python/plotly-express/) are set to fill the slide area below the title, and for R the Knitr figure width and height are similarly defaulted.

Nevertheless, you will frequently need to change these defaults for a given figure. The details on how to do this vary by graphics library. Here’s an example of explicitly sizing an [Altair](https://altair-viz.github.io/) plot:

``` python
alt.Chart(cars).mark_point().encode(
    x='Horsepower',
    y='Miles_per_Gallon',
    color='Origin',
).properties(
    width=700,
    height=300
).interactive()
```

### Code Echo

Unlike with ordinary documents, within Quarto presentations executable code blocks do not `echo` their source code by default (this is because often the code produces a figure that wants to occupy as much vertical space as possible). You can override this behavior using the `echo` option. For example:

```` java
```{python}
#| echo: true

import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={"projection": "polar"})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```
````

### Output Location

By default, output from executable code blocks is displayed immediately after the code. You can use the `output-location` option to modify this behavior as follows:

|  |  |
|----|----|
| `fragment` | Display output as a [Fragment](../../../docs/presentations/revealjs/advanced.llms.md#fragments) (delay showing it until it is explicitly stepped through by advancing the slide). |
| `slide` | Display output on the subsequent slide. |
| `column` | Display output in a column adjacent to the code. |
| `column-fragment` | Display output in a column adjacent to the code and delay showing it until it is explicitly stepped through by advancing the slide. |

For example, here we display cell output on its own slide:

```` markdown
```{r}
#| echo: true
#| output-location: slide
library(ggplot2)
ggplot(airquality, aes(Temp, Ozone)) + 
  geom_point() + 
  geom_smooth(method = "loess")
```
````

See the documentation on [Execution Options](../../../docs/computations/execution-options.llms.md) for more details on the various other ways to customize output from code execution.

## Tabsets

You can add tabbed content to slides using the standard Quarto syntax for [tabsets](../../../docs/output-formats/html-basics.llms.md#tabsets). For example:

``` markdown
::: {.panel-tabset}

### Tab A

Content for `Tab A`

### Tab B

Content for `Tab B`

:::
```

Note that one significant disadvantage to tabsets is that only the first tab will be visible when printing to PDF.

## Slide Backgrounds

Slides are contained within a limited portion of the screen by default to allow them to fit any display and scale uniformly. You can apply full page backgrounds outside of the slide area by adding a `background` attribute to your slide headings. Five different types of backgrounds are supported: color, gradient, image, video and iframe.

### Color Background

All CSS color formats are supported, including hex values, keywords, `rgba()` or `hsl()`. For example:

``` markdown
## Slide Title {background-color="aquamarine"}
```

> **TIP:**
>
> Note that if the background color of your media differs from your presentation’s theme (e.g. a dark image when using a light theme) then you should also explicitly set the `background-color` so that text on top of the background appears in the correct color (e.g. light text on a dark background).

### Gradient Background

All CSS gradient formats are supported, including `linear-gradient`, `radial-gradient` and `conic-gradient`.

``` markdown
## Slide Title {background-gradient="linear-gradient(to bottom, #283b95, #17b2c3)"}

## Slide Title {background-gradient="radial-gradient(#283b95, #17b2c3)"}
```

### Image Backgrounds

By default, background images are resized to cover the full page. Available options:

| **Attribute** | **Default** | **Description** |
|:---|:---|:---|
| `background-image` |  | URL of the image to show. GIFs restart when the slide opens. |
| `background-size` | cover | See [background-size](https://developer.mozilla.org/docs/Web/CSS/background-size) on MDN. |
| `background-position` | center | See [background-position](https://developer.mozilla.org/docs/Web/CSS/background-position) on MDN. |
| `background-repeat` | no-repeat | See [background-repeat](https://developer.mozilla.org/docs/Web/CSS/background-repeat) on MDN. |
| `background-opacity` | 1 | Opacity of the background image on a 0-1 scale. 0 is transparent and 1 is fully opaque. |

For example:

``` markdown
## Slide Title {background-color="black" background-image="https://placekitten.com/100/100" background-size="100px" background-repeat="repeat"}

This slide's background image will be sized to 100px and repeated.
```

Since this image has a dark background and our slides use the default (light) theme, we explicitly set the `background-color` to black so that text drawn on top of it is light.

### Video Backgrounds

Automatically plays a full size video behind the slide.

| **Attribute** | **Default** | **Description** |
|:---|:---|:---|
| `background-video` |  | A single video source, or a comma separated list of video sources. |
| `background-video-loop` | false | Flags if the video should play repeatedly. |
| `background-video-muted` | false | Flags if the audio should be muted. |
| `background-size` | cover | Use `cover` for full screen and some cropping or `contain` for letterboxing. |
| `background-opacity` | 1 | Opacity of the background video on a 0-1 scale. 0 is transparent and 1 is fully opaque. |

For example:

``` markdown
## Slide Title {background-video="video.mp4" background-video-loop="true" background-video-muted="true"}

This slides's background video will play in a loop with audio muted.
```

### IFrame Backgrounds

Embeds a web page as a slide background that covers 100% of the reveal.js width and height. The iframe is in the background layer, behind your slides, and as such it’s not possible to interact with it by default. To make your background interactive, you can add the `background-interactive` attribute.

| **Attribute** | **Default** | **Description** |
|:---|:---|:---|
| `background-iframe` |  | URL of the iframe to load |
| `background-interactive` | false | Include this attribute to make it possible to interact with the iframe contents. Enabling this will prevent interaction with the slide content. |

For example:

``` markdown
## Slide Title {background-iframe="https://example.com"}
```

### Slide Backgrounds Without a Title

You can always omit the title text, and specify only the slide background information:

``` markdown
## {background-color="aquamarine"}

(A slide with no title)

## {background-color="black" background-image="https://placekitten.com/100/100" background-size="100px" background-repeat="repeat"}

(Another slide with no title)
```

### Main Title Slide Background

The main title slide is the first slide, which is generated via document YAML options. As a result, the methods described above won’t work for providing a background for the title slide. Rather, you need to do the following:

1.  Provide the title slide background options under `title-slide-attributes`
2.  Prepend the background options with `data-`

For example:

``` yaml
---
title: My Slide Show
title-slide-attributes:
    data-background-image: /path/to/title_image.png
    data-background-size: contain
    data-background-opacity: "0.5"
---
```

## Learning More

See these articles lo learn about more advanced capabilities of Reveal:

- [Presenting Slides](../../../docs/presentations/revealjs/presenting.llms.md) describes slide navigation, printing to PDF, drawing on slides using a chalkboard, and creating multiplex presentations.
- [Advanced Reveal](../../../docs/presentations/revealjs/advanced.llms.md) delves into transitions, animations, advanced layout and positioning, and other options available for customizing presentations.
- [Reveal Themes](../../../docs/presentations/revealjs/themes.llms.md) talks about using and customizing existing themes as well as creating brand new themes.
