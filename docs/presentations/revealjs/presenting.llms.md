# Presenting Slides

## Overview

This article covers the mechanics of presenting slides with Reveal. Basic navigation is done using the following keyboard shortcuts:

| Action                     | Keys            |
|----------------------------|-----------------|
| Next slide                 | → SPACE N       |
| Previous slide             | ← P             |
| Navigate without fragments | Alt → Alt ←     |
| Jump to first/last slide   | Shift → Shift ← |

> **TIP:**
>
> You will often want to enter fullscreen mode when presenting. You can do this by pressing the FF key.

In addition to basic keyboard navigation, Reveal supports several more advanced capabilities, including:

- Navigation menu and overview mode
- Speaker view (w/ speaker notes,timer, and preview of upcoming slides)
- Printing to PDF and publishing as self contained HTML
- Drawing on top of slides & chalkboard/whiteboard mode
- Multiplex, which allows your audience to follow the slides of the presentation you are controlling on their own phone, tablet or laptop.

These capabilities are described below.

## Navigation Menu

Quarto includes a built in version of the [reveal.js-menu](https://github.com/denehyg/reveal.js-menu) plugin. You can access the navigation menu using the button ![](images/navigation-menu-icon.png) located in the bottom left corner of the presentation. Clicking the button opens a slide navigation menu that enables you to easily jump to any slide:

![Screen shot of basic reveal.js slide with no overlays.](images/navigation-menu-button.png)

![Screenshot of reveal.js slide with menu plugin open on the left. The menu bar has the Slides tab open, which shows a selectable list of all of the slides in the presentation.](images/navigation-menu-open.png)

> **TIP:**
>
> You can also open the navigation menu by pressing the MM key.

The navigation menu also includes a **Tools** pane that provides access to the various other navigation tools including Fullscreen, Speaker View, Overview Mode, and Print to PDF.

Use the following options to customize the appearance and behavior of the menu:

| Option | Description |
|----|----|
| `side` | Side of the presentation where the menu will be shown. `left` or `right` (defaults to `left`). |
| `width` | Width of the menu (`normal`, `wide`, `third`, `half`, `full`, or any valid css length value). Defaults to `normal` |
| `numbers` | Add slide numbers to menu items. |

For example:

``` yaml
format:
  revealjs:
    menu:
      side: right
      width: wide
```

You can hide the navigation menu by specifying the `menu: false` option:

``` yaml
format:
  revealjs:
    menu: false
```

Note that you can still open the menu using the MM key even if the button is hidden.

## Jump To Slide

You can skip ahead to a specific slide using reveal.js’ jump-to-slide shortcut. Here’s how it works:

- Press GG to activate
- Type a slide number or an id
- Press Enter to confirm

You can either enter - a numeric value to navigate to the desired slide number - a string, which will try to locate a slide with a matching id and navigate to it.

This feature can be opt-out by setting `jump-to-slide: false` option:

``` yaml
format:
  revealjs:
    jump-to-slide: false
```

## Overview Mode

Overview mode provides an alternate view that shows you a thumbnail for each slide:

![Screenshot of slides shown in overview mode, showing a series of thumbnails for the slides in the presentation.](images/overview-mode.png)

> **TIP:**
>
> You can enable Overview Mode by pressing the OO key.

## Scroll View

Reveal presentations can be presented in [Scroll View](https://revealjs.com/scroll-view/) with vertically scrolled navigation instead of Slides. This is a new view mode introduced in Revealjs 5. It is always available in presentations as an alternative view mode (like [Print view](#print-to-pdf)), and it will be used as the default view on small screens (e.g. viewing a presentation on a mobile).

Our demo presentation can be seen [in scroll view mode](https://quarto.org/docs/presentations/revealjs/demo/?view=scroll) and below

### Entering Scroll View

To enter Scroll View , do one the following:

- Toggle into Scroll View using the RR key

- Toggle into Scroll View using the [Navigation Menu](#navigation-menu)

- Toggle into Scroll View by adding `?view=scroll` to the url, e.g. `https://quarto.org/docs/presentations/revealjs/demo/?view=scroll`

You can easily toggle out of Scroll View by the same action.

### Default View Mode

Scroll View can be set as the default mode for the presentation using the `scroll-view` option:

``` yaml
format:
  revealjs:
    scroll-view: true
```

### Scroll View Options

Scroll View can be configured using the following options under `scroll-view`:

[TABLE]

For example, the following specifies that we want a compact layout, proximity snap mode, to always show the progress scrollbar, and to never automatically activate for small screens:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    scroll-view:
      layout: compact
      snap: proximity
      progress: true
      activation-width: 0
---
```

## Slide Zoom

Hold down the AltAlt key and click on any element to zoom towards it. Try zooming in on one of these images:

AltAlt or CtrlCtrl click again to zoom back out.

## Speaker View

The speaker view shows the current slide along with the upcoming slide, a timer, and any speaker notes associated with the current slide:

![Screenshot of reveal.js presentation in Speaker View. On the right, the active slide is shown. The left column contains three sections which show (from top to bottom): the upcoming slide, time (both elapsed and clock time), and a section where speaker notes go.](images/speaker-view.png)

> **TIP:**
>
> You can enable Speaker View by pressing the SS key.

You can add speaker notes to a slide using a div with class `.notes`. For example:

``` markdown
## Slide with speaker notes

Slide content

::: {.notes}
Speaker notes go here.
:::
```

## Slide Numbers

You can add slide numbers to your presentation using the `slide-number` option. You can also control in which contexts slide numbers appear using the `show-slide-number` option. For example, here we configure slides numbers for printed output only:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    slide-number: true
    show-slide-number: print
---
```

In addition to a simple `true` or `false` value, the `slide-number` option can also specify a format. Available formats include:

| Value | Description                           |
|-------|---------------------------------------|
| `c/t` | Slide number / total slides (default) |
| `c`   | Slide number only                     |
| `h/v` | Horizontal / Vertical slide number    |
| `h.v` | Horizontal . Vertical slide number    |

See [Vertical Slides](../../../docs/presentations/revealjs/advanced.llms.md#vertical-slides) for additional information on vertical slides.

The `show-slide-number` option supports the following values:

| Value     | Description                                  |
|-----------|----------------------------------------------|
| `all`     | Show slide numbers in all contexts (default) |
| `print`   | Only show slide numbers when printing to PDF |
| `speaker` | Only show slide numbers in the speaker view  |

## Print to PDF

Reveal presentations can be exported to PDF via a special print stylesheet.

> **NOTE:**
>
> Note: This feature has been confirmed to work in [Google Chrome](https://google.com/chrome), [Chromium](https://www.chromium.org/Home) as well as in [Firefox](https://www.mozilla.org/en-US/firefox/).

To Print to PDF, do the following:

1.  Toggle into Print View using the EE key (or using the [Navigation Menu](#navigation-menu))
2.  Open the in-browser print dialog Ctrl+PCtrl+P.
3.  Change the **Destination** setting to **Save as PDF**.
4.  Change the **Layout** to **Landscape**.
5.  Change the **Margins** to **None**.
6.  Enable the **Background graphics** option.
7.  Click **Save** 🎉

If you entered print mode in the same window, you can toggle out of Print View using the same EE key, or navigate back to last slide seen using usual back button in your browser.

Here’s what the Chrome print dialog would look like with these settings enabled:

![Screenshot of Chrome print dialog with the first slide/page of 27 shown on the left, and print options on the right. The Destination print option has Save as PDF selected.](images/print-to-pdf.png)

### Print Options

There are a number of options that affected printed output that you may want to configure prior to printing:

| Option | Description |
|----|----|
| `show-notes` | Include speaker notes (`true`, `false`, or `separate-page)` |
| `slide-number` | Include slide numbers (`true` or `false`) |
| `pdf-max-pages-per-slide` | Slides that are too tall to fit within a single page will expand onto multiple pages. You can limit how many pages a slide may expand to using the `pdf-max-pages-per-slide` option. |
| `pdf-separate-fragments` | Slides with multiple fragments are printed on a single page by default. To create a page for each fragment set this option to `true`. |

For example, the following specifies that we want to print speaker notes on their own page and include slide numbers:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    show-notes: separate-page
    slide-number: true
---
```

## Preview Links

Reveal makes it easy to incorporate navigation to external websites into the flow of presentations using the `preview-links` option.

When you click on a hyperlink with `preview-links: true`, the link will be navigated to in an iframe that overlays the slide. For example, here we’ve clicked on a [Matplotlib](https://matplotlib.org/) link and the website opens on top of the slide (you’d click the close button at top right to hide it):

![Screenshot of matplotlib landing page.](images/matplotlib.png)

Available values for `preview-link` include:

| Value | Description |
|----|----|
| `auto` | Preview links when presenting in full-screen mode (otherwise navigate to them normally) |
| `true` | Always preview links |
| `false` | Never preview links (the default) |

For example, here we set `preview-links` to `auto`:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    preview-links: auto
---
```

You can also set this option on a per-link basis. These two links respectively enable and disable preview:

``` markdown
[Preview](https://example.com){preview-link="true"}

[NoPreview](https://example.com){preview-link="false"}
```

Previewing website in HTML format will use an `<iframe>`, which not all websites will allow (e.g. they could set in their response header [`X-Frame-Options` to `deny`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options), or [`frame-ancestor` restriction in their `Content-Security-Policy`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)). If a website disallow `iframe` usage, the preview will not be working in the Quarto document output.

## Slide Tone

Slide tone plays a subtle sound when you change slides. It was [requested by a blind user](https://github.com/yihui/xaringan/issues/214) and enables presenters to hear an auditory signal of their progress through the slides. Enable slide tone with:

``` yaml
format:
  revealjs:
    slide-tone: true
```

The tones increase in pitch for each slide from a low C to a high C note. The tone pitch stays the same for incremental slides.

The implementation of slide tone was adapted from the [slide tone plugin](https://github.com/gadenbuie/xaringanExtra/blob/master/docs/slide-tone/libs/slide-tone/slide-tone.js) in xaringanExtra.

## Auto-Slide

Presentations can be configured to step through slides automatically, without any user input. To enable this you will need to specify an interval for slide changes using the `auto-slide` option (the interval is provided in milliseconds). The `loop` option can additionally be specified to continue presenting in a loop once all the slides have been shown.

For example, here we specify that we want to advance every 5 seconds and continue in a loop:

``` yaml
---
title: "Presentation"
format: 
  revealjs: 
    auto-slide: 5000
    loop: true
---
```

A play/pause control element will automatically appear for auto-sliding decks. Sliding is automatically paused if the user starts interacting with the deck. It’s also possible to pause or resume sliding by pressing AA on the keyboard.

You can disable the auto-slide controls and prevent sliding from being paused by specifying `auto-slide-stoppable: false`.

### Slide Timing

It’s also possible to override the slide duration for individual slides and fragments by using the `autoslide` attribute (this attribute also works on [Fragments](../../../docs/presentations/revealjs/advanced.llms.md#fragments)). For example, here we set the auto-slide value to 2 seconds:

``` markdown
## Slide Title {autoslide=2000}
```

## Publishing

There are two main ways to publish Reveal presentations:

1.  As a PDF file—see [Print to PDF](#print-to-pdf) above for details on how to do this.

2.  As an HTML file. For HTML, it’s often most convenient to distribute the presentation as a single self contained file. To do this, specify the `embed-resources` option:

    ``` yaml
    ---
    title: "Presentation"
    format:
      revealjs:
        embed-resources: true
    ---
    ```

    All of the dependent images, CSS styles, and other assets will be contained within the HTML file created by Quarto.

    > **NOTE:**
    > Note that specifying `embed-resources` can slow down rendering by a couple of seconds, so you may want to enable `embed-resources` only when you are ready to publish. Also note that Reveal plugin [Chalkboard](#chalkboard) is not compatible with `embed-resources` — when [Chalkboard](#chalkboard) plugin is enabled, specifying `embed-resources: true` will result an error.

See the documentation on [Publishing HTML](../../../docs/publishing/index.llms.md) for details on additional ways to publish Reveal presentations including GitHub Pages and Posit Connect.

## Navigation Options

There are several navigational cues provided as part of Reveal presentations and corresponding options that control them:

| Option | Description |
|----|----|
| `controls` | Show arrow controls for navigating through slides (defaults to `auto`, which will show controls when vertical slides are present or when the deck is embedded in an iframe). |
| `progress` | Show a progress bar at the bottom (defaults to `true`). |
| `history` | Push slide changes to the browser history. Defaults to `true`, which means that the browser Forward/Back buttons can be used for slide navigation. |
| `hash-type` | Type of URL hash to use for slides. Defaults to `title` which is derived from the slide title. You can also specify `number`. |

For example, the following configuration hides the progress bar and specifies that we want to use browser history:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    progress: false
    history: true
---
```

## Chalkboard

Quarto includes a built-in version of the [reveal.js-chalkboard](https://github.com/rajgoel/reveal.js-plugins/tree/master/chalkboard) plugin. Specify the `chalkboard: true` option to enable the plugin, which enables you to draw on a notes canvas on top of your slides and/or open up an empty chalkboard within your presentation:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    chalkboard: true
---
```

> **WARNING:**
>
> Note that Reveal plugin [Chalkboard](#chalkboard) is not compatible with `embed-resources` output — when [Chalkboard](#chalkboard) plugin is enabled, specifying `embed-resources: true` will result an error.

Here are what the notes canvas and chalkboard look like when activated:

![Slide with notes canvas activated has a panel on the left to select colors, and a menu bar at the bottom with a paintbrush. One of the words in the slide header has been underlined with the brush in blue.](images/drawing-canvas.png)

![Screenshot of chalkboard canvas with color selector on the left, and paintbrush tool at the bottom. The background is dark, and the equation 'y = mx + b' has been drawn in white with a chalky texture.](images/chalkboard.png)

To toggle the notes canvas on and off use the ![](images/canvas-icon.png) button or the CC key.

To toggle the chalkboard on and off use the ![](images/chalkboard-icon.png) button or the BB key.

Here are all of the keyboard shortcuts associated with the notes canvas and chalkboard:

| Action                  | Key                |
|-------------------------|--------------------|
| Toggle notes canvas     | CC                 |
| Toggle chalkboard       | BB                 |
| Reset all drawings      | BACKSPACEBACKSPACE |
| Clear drawings on slide | DELDEL             |
| Cycle colors forward    | XX                 |
| Cycle colors backward   | YY                 |
| Download drawings       | DD                 |

The following mouse and touch gestures can be used for interacting with drawings:

- Click on the buttons at the bottom left to toggle the notes canvas or chalkboard

- Click on the color picker at the left to change the color (the color picker is only visible if the notes canvas or chalkboard is active)

- Click on the up/down arrows on the right to switch among multiple chalkboard (the up/down arrows are only available for the chalkboard)

- Click the left mouse button and drag to write on notes canvas or chalkboard

- Click the right mouse button and drag to wipe away previous drawings

- Touch and move to write on notes canvas or chalkboard

- Touch and hold for half a second, then move to wipe away previous drawings

### Restoring Drawings

The DD key downloads any active drawings into a JSON file. You can then restore these drawings when showing your presentation using the `src` option. For example:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    chalkboard:
      src: drawings.json
---
```

### Chalkboard Options

The following options are available to customize the behavior and appearance of the chalkboard:

[TABLE]

For example, the following configuration specifies that we want to use the `whiteboard` theme with a (thicker) boardmarker width, and that we want to hide the chalkboard buttons at the bottom of each slide:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    chalkboard:
      theme: whiteboard
      boardmarker-width: 5
      buttons: false
---
```

If you disable the chalkboard buttons globally you can selectively re-enable them for individual slides with the `chalkboard-buttons` attribute. For example:

``` markdown
## Slide Title {chalkboard-buttons="true"}
```

You can also use `chalkboard-buttons="false"` to turn off the buttons for individual slides.

## Multiplex

Quarto includes a built-in version of the [Reveal Multiplex](https://github.com/reveal/multiplex) plugin. The multiplex plugin allows your audience to follow the slides of the presentation you are controlling on their own phone, tablet or laptop. When you change slides in your master presentations everyone will follow and see the same content on their own device.

Creating a Reveal presentation that supports multiplex is straightforward. Just specify the `multiplex: true` option as follows:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    multiplex: true
---
```

Rendering the presentation will result in two HTML files being created by Quarto:

| File | Description |
|----|----|
| `presentation.html` | This is the file you should publish online and that your audience should view. |
| `presentation-speaker.html` | This is the file that you should present from . This file can remain on your computer and does not need to be published elsewhere. |

The two versions of the presentation will be synchronized such that when the speaker version switches slides the viewers also all switch to the same slide.

### Multiplex Server

Behind the scenes there is a multiplex server that is synchronizing slide events between the viewer and speaker versions of the presentation. Note that the this server does not actually see any of the slide content, it is only used to synchronize events.

By default, a server created and hosted by the Revealjs team is used for this: <https://multiplex.up.railway.app/>. This server is used by default when you specify `multiplex: true`.

#### Running your own server

If you want to run your own version of this server its source code is here: <https://github.com/reveal/multiplex/blob/master/index.js>.

You can then configure multiplex to use an alternate server as follows:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    multiplex: 
      url: 'https://myserver.example.com/
---
```

Note that Quarto calls the multiplex server behind the scenes to provision a id and secret for your presentation. If you want to provision your own id and secret you can do so at <https://multiplex.up.railway.app/> (or using your custom hosted server URL) and provide them explicitly in YAML:

``` yaml
---
title: "Presentation"
format:
  revealjs:
    multiplex: 
      id: '1ea875674b17ca76'
      secret: '13652805320794272084'
---
```

Note that the `secret` value will be included in only the speaker version of the presentation.

## Learning More

See these articles lo learn more about using Reveal:

- [Reveal Basics](../../../docs/presentations/revealjs/index.llms.md) covers the basic mechanics of creating presentations.
- [Advanced Reveal](../../../docs/presentations/revealjs/advanced.llms.md) delves into transitions, animations, advanced layout and positioning, and other options available for customizing presentations.
- [Reveal Themes](../../../docs/presentations/revealjs/themes.llms.md) talks about using and customizing existing themes as well as creating brand new themes.
