# Website Options

All available options for `website` projects are documented below. See [Creating a Website](../../../docs/websites/) for an in-depth guide to creating websites with Quarto.

## Project

Options that define the type, render targets, and output of a project. Project options are specified under the `project` key. For example:

``` yaml
project:
  type: website
  output-dir: _site
```

[TABLE]

### Preview

Specify options that control the behavior of `quarto preview` within the `preview` key. For example:

``` yaml
project:
  type: website
  output-dir: _site
  preview:
    port: 4200
    browser: false
```

Available `preview` options include:

|  |  |
|:---|:---|
| `port` | Port to listen on (defaults to random value between 3000 and 8000) |
| `host` | Hostname to bind to (defaults to 127.0.0.1) |
| `serve` | Options for external preview server (see [Serve](#serve)) |
| `browser` | Open a web browser to view the preview (defaults to true) |
| `watch-inputs` | Re-render input files when they change (defaults to true) |
| `navigate` | Navigate the browser automatically when outputs are updated (defaults to true) |
| `timeout` | Time (in seconds) after which to exit if there are no active clients |

### Serve

If you are creating a project extension for another publishing system that includes its own preview server (for example, [Hugo](../../../docs/output-formats/hugo.llms.md) or [Docusaurus](../../../docs/output-formats/docusaurus.llms.md)) then use the `preview: serve` options to customize the behavior of the preview server.

``` yaml
project:
  type: website
    preview:
      serve:
        cmd: "hugo serve --port {port} --bind {host} --navigateToChanged"
        env:
          HUGO_RELATIVEURLS: "true"
        ready: "Web Server is available at"
```

|  |  |
|:---|:---|
| `cmd` | Serve project preview using the specified command. Interpolate the `--port` into the command using `{port}`. |
| `args` | Additional command line arguments for preview command. |
| `env` | Environment variables to set for preview command. |
| `ready` | Regular expression for detecting when the server is ready. |

See the [Hugo](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/extensions/quarto/hugo/_extension.yml) and [Docusaurus](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/extensions/quarto/docusaurus/_extension.yml) extension source code for example usages of `preview: serve`.

## Website

Options that affect website output. Website options are specified under the `website` key. For example:

``` yaml
website:
  title: "My Website"
  image: opengraph.png
  page-navigation: true
```

[TABLE]

## Navbar

Options that define the top navigation bar for a website For example:

``` yaml
website:
  navbar:
    search: true
```

|  |  |
|:---|:---|
| `title` | The navbar title. Uses the project title if none is specified. |
| `logo` | Specification of image that will be displayed to the left of the title. |
| `logo-alt` | Alternate text for the logo image. |
| `logo-href` | Target href from navbar logo / title. By default, the logo and title link to the root page of the site (/index.html). |
| `background` | The navbar’s background color (named or hex color). |
| `foreground` | The navbar’s foreground color (named or hex color). |
| `search` | Include a search box in the navbar. |
| `pinned` | Always show the navbar (keeping it pinned). |
| `collapse` | Collapse the navbar into a menu when the display becomes narrow. |
| `collapse-below` | The responsive breakpoint below which the navbar will collapse into a menu (`sm`, `md`, `lg` (default), `xl`, `xxl`). |
| `left` | List of items for the left side of the navbar (see [Nav Items](#nav-items)) |
| `right` | List of items for the right side of the navbar (see [Nav Items](#nav-items)) |
| `toggle-position` | The position of the collapsed navbar toggle when in responsive mode |
| `tools-collapse` | Collapse tools into the navbar menu when the display becomes narrow. |

## Nav Items

Nav items appear in the `left` or `right` key of `navbar` definitions, or `contents` key of `sidebar` definitions. For example:

``` yaml
website:
  navbar:
    right:
      - icon: github
        href: https://github.com/
        aria-label: GitHub
```

|  |  |
|:---|:---|
| `aria-label` | Accessible label for the item. |
| `href` | Link to file contained with the project or external URL |
| `icon` | Name of bootstrap icon (e.g. `github`, `twitter`, `share`) See <https://icons.getbootstrap.com/> for a list of available icons |
| `menu` | Submenu of [navigation items](#nav-items) |
| `text` | Text to display for item (defaults to the document title if not provided) |
| `rel` | Value for rel attribute. Multiple space-separated values are permitted. See <https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel> for a details. |
| `target` | Value for target attribute. See <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-target> for details. |

Note that the `icon` option is available for items in the Navbar, however items in the Sidebar do not support the `icon` option.

## Sidebar

Options that define the side navigation area for a website. For example:

``` yaml
website:
  sidebar:
    search: true
```

|  |  |
|:---|:---|
| `id` | The identifier for this sidebar. |
| `title` | The sidebar title. Uses the project title if none is specified. |
| `logo` | Specification of image that will be displayed in the sidebar. |
| `logo-alt` | Alternate text for the logo image. |
| `logo-href` | Target href from navbar logo / title. By default, the logo and title link to the root page of the site (/index.html). |
| `search` | Include a search control in the sidebar. |
| `tools` | List of sidebar tools (see [Sidebar Tools](#sidebar-tools)) |
| `contents` | List of [navigation items](#nav-items) to appear in the sidebar. Can also include `section` entries which in turn contain sub-lists of navigation items. |
| `style` | The style of sidebar (`docked` or `floating`). |
| `background` | The sidebar’s background color (named or hex color). |
| `foreground` | The sidebar’s foreground color (named or hex color). |
| `border` | Whether to show a border on the sidebar (defaults to true for ‘docked’ sidebars) |
| `alignment` | Alignment of the items within the sidebar (`left`, `right`, or `center`) |
| `collapse-level` | The depth at which the sidebar contents should be collapsed by default. |
| `pinned` | When collapsed, pin the collapsed sidebar to the top of the page. |
| `header` | Markdown to place above sidebar content (text or file path) |
| `footer` | Markdown to place below sidebar content (text or file path) |

### Sidebar Tools

Action buttons that appear on the sidebar. For example:

``` yaml
website:
  sidebar:
    tools:
      - icon: github
        href: https://github.com/
```

|  |  |
|:---|:---|
| `icon` | Name of bootstrap icon (e.g. `github`, `twitter`, `share`) See <https://icons.getbootstrap.com/> for a list of available icons |
| `href` | Link to file contained with the project or external URL |
| `menu` | Submenu of [navigation items](#nav-items) |

## Announcement

An announcement that appears at the top of the site. For example:

``` yaml
---
website:
  announcement: 
    content: "**New** - this is an announcement" 
    position: below-navbar 
---
```

|  |  |
|:---|:---|
| `content` | The content of the announcement |
| `dismissable` | Whether this announcement may be dismissed by the user. |
| `icon` | Name of bootstrap icon (e.g. `github`, `twitter`, `share`) for the announcement. See <https://icons.getbootstrap.com/> for a list of available icons |
| `position` | The position of the announcement. One of `above-navbar` (default) or `below-navbar`. |
| `type` | The type of announcement. One of `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light` or `dark`. Affects the appearance of the announcement. |

## Footer

Website page footer definition. For example:

``` yaml
website:
  page-footer:
    center: 
      - text: "About"
        href: about.qmd
      - text: "License"
        href: license.md
      - text: "Trademark"
        href: trademark.qmd
```

|              |                                                    |
|:-------------|:---------------------------------------------------|
| `left`       | Footer left content                                |
| `right`      | Footer right content                               |
| `center`     | Footer center content                              |
| `border`     | Footer border (`true`, `false`, or a border color) |
| `background` | Footer background color                            |
| `foreground` | Footer foreground color                            |

## Search

Search options are specified under the `search` key of `website`. For example:

``` yaml
website:
  search:
    location: navbar
    type: overlay
```

|  |  |
|:---|:---|
| `location` | Location for search widget (`navbar` or `sidebar`) |
| `type` | Type of search UI (`overlay` or `textbox`) |
| `limit` | Number of matches to display (defaults to 20) |
| `collapse-after` | Matches after which to collapse additional results |
| `copy-button` | Provide button for copying search link |
| `merge-navbar-crumbs` | When false, do not merge navbar crumbs into the crumbs in `search.json`. |
| `keyboard-shortcut` | One or more keys that will act as a shortcut to launch search (single characters) |
| `show-item-context` | Whether to include search result parents when displaying items in search results (when possible). |
| `algolia` | Use an Algolia index for site search (see [Algolia Options](#algolia-options)) |

### Algolia Options

You can use an [Algolia](../../../docs/websites/website-search.llms.md#using-algolia) index as the back end of website search. Specify Algolia options using the `algolia` sub-key of `search`, for example:

``` yaml
website:
  search:
    algolia:
      index-name: <my-index-name>
      application-id: <my-application-id>
      search-only-api-key: <my-search-only-api-key>
```

|  |  |
|:---|:---|
| `index-name` | The name of the index to use when performing a search |
| `application-id` | The unique ID used by Algolia to identify your application |
| `search-only-api-key` | The Search-Only API key to use to connect to Algolia |
| `analytics-events` | Enable tracking of Algolia analytics events |
| `show-logo` | Enable the display of the Algolia logo in the search results footer. |
| `index-fields` | Fields to target for searches (see below for details) |
| `params` | Additional parameters to pass when executing a search |

The `index-fields` option provides sub-fields within the Algolia index to target for searches:

|           |                                                  |
|:----------|:-------------------------------------------------|
| `href`    | Field that contains the URL of index entries     |
| `title`   | Field that contains the title of index entries   |
| `text`    | Field that contains the text of index entries    |
| `section` | Field that contains the section of index entries |

## Social

Social metadata is provided as a subkey of `website` options. You can specify `true` to generate social metadata using a set of default option, or specify one or more Twitter or Open Graph specific options as enumerated below. For example:

``` yaml
website:
  open-graph: true
  twitter-card: 
    site: "@sitehandle"
```

### Twitter Card

Set Twitter options under the `twitter-card` key:

``` yaml
website:
  twitter-card: 
    site: "@sitehandle"
```

[TABLE]

### Open Graph

Set Open Graph options under the `open-graph` key:

``` yaml
website:
  open-graph: 
    title: "Title for Open Graph"
```

|  |  |
|:---|:---|
| `title` | The title of the page. Note that by default Quarto will automatically use the title metadata from the page. Specify this field if you’d like to override the title for this provider. |
| `description` | A short description of the content. Note that by default Quarto will automatically use the description metadata from the page. Specify this field if you’d like to override the description for this provider. |
| `image` | The path to a preview image for the content. By default, Quarto will use the `image` value from the format metadata. If you provide an image, you may also optionally provide an `image-width` and `image-height`. |
| `image-alt` | The alt text for the preview image. By default, Quarto will use the `image-alt` value from the format metadata. If you provide an image, you may also optionally provide an `image-width` and `image-height`. |
| `image-width` | Image width (pixels) |
| `image-height` | Image height (pixels) |
| `locale` | Locale of open graph metadata |
| `site-name` | Name that should be displayed for the overall site. If not explicitly provided in the `open-graph` metadata, Quarto will use the website or book `title` by default. |

## Comments

You can add commenting to your website using either [Hypothesis](https://web.hypothes.is/), [Utterances](https://utteranc.es/), or [Giscus](https://giscus.app/).

### Hypothesis

Enable and configure Hypothesis commenting via `comments` key. For example:

``` yaml
website:
  comments: 
    hypothesis:
      theme: clean
      openSidebar: false
```

|  |  |
|:---|:---|
| `client-url` | Override the default hypothesis client url with a custom client url. |
| `openSidebar` | Controls whether the sidebar opens automatically on startup. |
| `showHighlights` | Controls whether the in-document highlights are shown by default (`always`, `whenSidebarOpen` or `never`) |
| `theme` | Controls the overall look of the sidebar (`classic` or `clean`) |
| `enableExperimentalNewNoteButton` | Controls whether the experimental New Note button should be shown in the notes tab in the sidebar. |
| `usernameUrl` | Specify a URL to direct a user to, in a new tab. when they click on the annotation author link in the header of an annotation. |
| `services` | Array of service definitions |
| `branding` | Custom branding/colors to apply to UI |
| `externalContainerSelector` | A CSS selector specifying the containing element into which the sidebar iframe will be placed. |
| `focus` | User focused filter set for the available annotations on a page |
| `requestConfigFromFrame` | Specify a host iframe to request configuration from |
| `assetRoot` | The root URL from which assets are loaded. |
| `sidebarAppUrl` | The URL for the sidebar application which displays annotations. |

For additional documentation on the Hypothesis options enumerated above, see the [Hypothesis Publisher Config](https://h.readthedocs.io/projects/client/en/latest/publishers/config.llms.md) documentation.

### Utterances

Enable and configure Utterances commenting via the `comments` key. For example:

``` yaml
website:
  comments: 
    utterances:
      repo: quarto-dev/quarto-web
```

|  |  |
|:---|:---|
| `repo` | The Github repo that will be used to store comments. |
| `label` | The label that will be assigned to issues created by Utterances. |
| `theme` | The Github theme that should be used for Utterances (`github-light`, `github-dark`, `github-dark-orange`, `icy-dark`, `dark-blue`, `photon-dark`, `body-light`, or `gruvbox-dark`) |
| `issue-term` | How posts should be mapped to Github issues (`pathname`, `url`, `title` or `og:title`) |

### Giscus

Enable and configure usage of the [Giscus app](https://giscus.app) via the `comments` key. For example:

``` yaml
website:
  comments:
    giscus:
      repo: quarto-dev/quarto-web
```

[TABLE]

## Listings

[Listings](../../../docs/websites/website-listings.llms.md) enable you to automatically generate the contents of a page (or region of a page) from a list of Quarto documents or other custom data. You can enable listings on a page using the `listing` option in the document front matter. For example, setting `listing: default` will generate a listing of all documents in the directory (with the exception of the current document):

``` yaml
---
title: "Listing Example"
listing: default
---
```

To customize the listing, specify additional options under the `listing` key:

``` yaml
---
title: "Listing Example"
listing: 
  contents: posts
  type: grid
  grid-columns: 2
---
```

[TABLE]

### Feed

Enable an RSS feed for your listing by including the `feed` option:

``` yaml
---
title: "Listing Example"
listing:
  contents: posts
  feed:
    items: 10
---
```

[TABLE]

## About

Layout a simple about page for an individual or organization. Specify about page options under the `about` key in the document front matter:

``` yaml
---
title: About
about:
  template: jolla
  image: profile.jpg
  links:
    - icon: twitter
      text: twitter
      href: https://twitter.com
---
```

For more, see the [About Pages](../../../docs/websites/website-about.llms.md) documentation.

[TABLE]
