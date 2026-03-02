# Website Tools

## Headers & Footers

You can provide standard headers and footers for pages on your site. These can apply to the main document body or to the sidebar. Available options include:

| Value | Description |
|----|----|
| `body-header` | Markdown to insert at the beginning of each page’s body (below the title and author block). |
| `body-footer` | Markdown to insert below each page’s body. |
| `margin-header` | Markdown to insert above right margin content (i.e. table of contents). |
| `margin-footer` | Markdown to insert below right margin content. |

For example (included in \_quarto.yml) :

``` yaml
body-header: | 
  This page brought to you by <https://example.com>
margin-header: |
  ![Logo image](/img/logo.png)
```

Note that links to figures should start with a `/` to work on each level of the website.

## Announcement Bar

![Screenshot showing an announcement bar on Quarto website with an 'info-circle' icon, a dismiss button, and a primary colour type. The content reads 'Alert - this is some information that you should pay attention to'.](images/website-announcement.png)

Captured view of the Quarto website, showcasing the dynamic announcement bar feature.

Add an announcement to display a prominent, customizable bar at the top of your website that grabs visitors’ attention. It’s perfect for highlighting important information, such as alerts, promotions, or updates. You can set an icon, make it dismissable, and even include formatted content like bold text. The announcement bar can be positioned to fit seamlessly within your site’s layout (*e.g.*, `below-navbar` or `above-navbar`), ensuring the message is both impactful and integrated.

Here’s an example of how you might configure it:

``` yaml
website:
  announcement: 
    icon: info-circle # <1>
    dismissable: true # <2>
    content: "**Alert** - this is some information that you should pay attention to" # <3>
    type: primary # <4>
    position: below-navbar # <5>
```

1.  `icon` - The Bootstrap icon to display in the announcement bar. You can choose from any of the [Bootstrap icons](https://icons.getbootstrap.com/).
2.  `dismissable` - Whether the announcement bar can be dismissed by the user. It can be `true` or `false`.
3.  `content` - The content of the announcement bar. You can use markdown to format the content.
4.  `type` - The type of the announcement bar. It can be one of `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`.
5.  `position` - The position of the announcement bar. It can be one of `below-navbar` or `above-navbar`.

## Social Metadata

You can enhance your website and the content that you publish to it by including additional types of metadata, including:

- Favicon
- Twitter Cards
- Open Graph

One important thing to note about using website tools is that while these tools are added to websites within the `website` key, in a book you should include the same options in the `book` key. For example, in a website you would include a favicon and twitter card as follows:

``` yaml
website:
  favicon: logo.png
  twitter-card: true
  site-url: https://example.com
```

In a book you’d use the `book` key instead:

``` yaml
book:
  favicon: logo.png
  twitter-card: true
  site-url: https://example.com
```

As you read the documentation below, keep in mind to substitute `book` for `website` if you are authoring a book.

### Favicon

The favicon for your site provides an icon for browser tabs and other sites that link to yours. Use the `favicon` option to provide the path to a favicon image. For example:

``` yaml
website:
  favicon: logo.png
```

### Twitter Cards

[Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards) provide an enhanced appearance when someone links to your site on Twitter. When a link to your site is included in a Tweet, Twitter automatically crawls your site and fetches any Twitter Card metadata. To enable the automatic generation of Twitter Card metadata for your site, you can add the following to your `_quarto.yml` configuration file:

``` yaml
website:
  twitter-card: true
```

In this case, Quarto will automatically generate a title, description, and preview image for the content. For more information about how Quarto finds preview images, see [Preview Images](#preview-images).

You may also provide additional metadata to be used when generating the Twitter Card, including:

[TABLE]

Here is a more comprehensive example of specifying Twitter Card metadata in a `quarto.yml` file:

``` yaml
website:
  twitter-card:
    creator: "@dragonstyle"
    site: "@rstudio"
```

Quarto will automatically merge global metadata found in the `website: twitter-card` key with any metadata provided in the document itself in the `twitter-card` key. This is useful when you need to specify a mix of global options (for example, `site`) with per document options such as `title` or `image`.

### Open Graph

The [Open Graph protocol](http://ogp.me/) is a specification that enables richer sharing of links to articles on the web. It will improve the previews of your content when a link to it is pasted into applications like Slack, Discord, Facebook, Linkedin, and more. To enable the automatic generation of Open Graph metadata for your content, include the following in your `_quarto.yml` configuration file:

``` yaml
website:
  open-graph: true
```

In this case, Quarto will automatically generate a title, description, and preview image for the content. For more information about how Quarto finds preview images, see [Preview Images](#preview-images).

You may also provide additional metadata to be used when generating the Open Graph metadata, including:

[TABLE]

Here is a more comprehensive example of specifying Open Graph metadata in a `quarto.yml` file:

``` yaml
website:
  open-graph:
    locale: es_ES
    site-name: Quarto
```

Quarto will automatically merge global metadata found in the `website: open-graph` key with any metadata provided in the document itself in the `open-graph` key. This is useful when you need to specify a mix of global options (for example, `site`) with per document options such as `title` or `image`.

### Preview Images

You can specify a preview image for your article in several different ways:

1.  **Full URL**: You can explicitly provide a full url to the preview image using the `image` field in the appropriate metadata. For example:

    ``` yaml
    title: "My Document"
    image: "https://quarto.org/docs/websites/images/tools.png"
    ```

2.  **Relative Path**: You may provide a document relative path to an image (such as `images/preview-code.png`) or a project relative path to an image (such as `/images/preview-code.png`). If you provide a relative path such as this, you must also provide a `site-url` in your site’s metadata. For example in your `_quarto.yml` configuration file:

    ``` yaml
    website:
      site-url: "https://www.quarto.org"
    ```

    and in your document front matter:

    ``` yaml
    title: "My Document"
    image: "/docs/websites/images/tools.png"
    ```

3.  **Image Class**: Any image that is being rendered in the page may also be used as a preview image by giving it the class name `preview-image`. Quarto will select the first image it finds with this class. For example, the following image will be used as the preview image when included on a page:

    ``` markdown
    ![](images/tools.png){.preview-image}
    ```

    If you label an image with this class, you must also provide a `site-url` in your site’s metadata.

4.  **Image Filename**: If none of the above ways of specifying a preview image have been used, Quarto will attempt to find a preview image by looking for an image included in the rendered document with one of the following names: `preview.png`, `feature.png`, `cover.png`, or `thumbnail.png`.

If you’d like to provide a default that is used when pages specify a preview image in none of the above ways, specify it at the site level:

``` yaml
website:
  image: "https://quarto.org/quarto-dark-bg.jpeg"
```

If you would like to prevent preview image discovery on a page, set `image` to `false`:

``` yaml
---
image: false
---
```

## Google Analytics

You can add [Google Analytics](https://analytics.google.com/) to your website by adding a `google-analytics` key to your `_quarto.yml` file. In its simplest form, you can just pass your Google Analytics tracking Id (e.g. `UA-xxxxxxx`) or Google Tag measurement Id (e.g. `G-xxxxxxx`) like:

``` yaml
website:
  google-analytics: "UA-XXXXXXXX"
```

Quarto will use the key itself to determine whether to embed Google Analytics (analytics.js) or Google Tags (gtag) as appropriate.

In addition to this basic configuration, you can exercise more fine grained control of your site analytics using the following keys.

[TABLE]

### Storage

Google Analytics uses cookies to distinguish unique users and sessions. If you choose to use cookies to store this user data, you should consider whether you need to enable [Cookie Consent](#cookie-consent) in order to permit the viewer to control any tracking that you enable.

If you choose `none` for storage, this will have the following effects:

- For Google Analytics v3 (analytics.js)  
  No tracking cookies will be used. Individual page hits will be properly tracked, enabling you to see which pages are viewed and how often they are viewed. Unique user and session tracking will not report data correctly since the tracking cookies they rely upon are not set.

- For Google Tags (gtag)  
  User consent for ad and analytics tracking cookies will be withheld. In this mode, Google Analytics will still collect user data without the user identification, but that data is currently not displayed in the Google Analytics reports.

## Cookie Consent

Quarto includes the ability to request cookie consent before enabling scripts that set cookies, using [Cookie Consent](https://www.cookieconsent.com).

The user’s cookie preferences will automatically control [Google Analytics](#google-analytics) (if enabled) and can be used to control custom scripts you add as well (see [Custom Scripts and Cookie Consent](#custom-scripts-and-cookie-consent)). You can enable the default request for cookie consent using the following:

``` yaml
website:
  cookie-consent: true
```

You can further customize the appearance and behavior of the consent using the following:

[TABLE]

A custom example might look more like:

``` yaml
website:
  cookie-consent:
    type: express
    style: headline
    palette: dark
  google-analytics:
    tracking-id: "G-XXXXXXX"
    anonymize-ip: true
```

### Cookie Preferences

In addition to requesting consent when a new user visits your website, Cookie Consent will also add a cookie preferences link to the footer of the website. You can control the text of this link using `prefs-text`. If you would rather position this link yourself, just add a link with the id `#open_preferences_center` to the website and Cookie Consent will not add the preferences link to the footer. For example:

``` markdown
Change [cookie preferences]{#open_preferences_center}
```

### Custom Scripts and Cookie Consent

Cookie Consent works by preventing the execution of scripts unless the user has expressed their consent. To control your custom scripts using Cookie Consent:

1.  Insert script tags as `type='text/plain'` (when the user consents, the type will be switched to `text/javascript` and the script will be executed).

&nbsp;

2.  Add a `cookie-consent` attribute to your script tag, setting it one of the following 4 levels:

    | Level | Description |
    |----|----|
    | `strictly-necessary` | Strictly scripts are loaded automatically and cannot be disabled by the user. |
    | `functionality` | Scripts that are required for basic functionality of the website, for example, remembering a user language preference. |
    | `tracking` | Scripts that are used to track users, for example [Google Analytics](#google-analytics). |
    | `targeting` | Scripts that are used for the purpose of advertising to ad targeting, for example Google AdSense remarketing. |

An example script that is used for user tracking would look like:

``` javascript
<script type="text/plain" cookie-consent="tracking">

// My tracking JS code here

</script>
```

## Site Resources

Besides input and configuration files, your site likely also includes a variety of resources (e.g. images) that you will want to publish along with your site. Quarto will automatically detect any files that you reference within your site and copy them to the output directory (e.g. `_site`).

Quarto also recognizes the following files and copies them to your output directory:

- `404.html`, one option for providing a [404 Page](../../docs/websites/website-navigation.llms.md#pages-404)
- `robots.txt`, a file specified by the [Robots Exclusion Protocol](https://datatracker.ietf.org/doc/html/rfc9309) that tells search engine crawlers which pages or files on your website they can or cannot access
- `_redirects`, a file used by some publishing providers to provide page redirects, e.g. [Netlify](https://docs.netlify.com/routing/redirects/#syntax-for-the-redirects-file)
- `CNAME`, a file used by some publishing providers to specify a custom domain, e.g. [GitHub Pages](../../docs/publishing/github-pages.llms.md#custom-domain)
- `.nojekyll`, a file used by GitHub pages to bypass building with Jekyll, e.g. when [publishing from `docs/`](../../docs/publishing/github-pages.llms.md#render-to-docs)

If this auto-detection fails for any reason, or if you want to publish a file not explicitly linked to from within your site, you can add a `resources` entry to your configuration. For example, here we specify that we want to include all Excel spreadsheets within the project directory as part of the website:

``` yaml
project:
  type: website
  resources: 
    - "*.xlsx"
```

Note that the `*.xlsx` value is quoted: this is because YAML requires that strings that begin with non-alphanumeric characters be quoted.

You can also add a `resources` metadata value to individual files. For example:

``` yaml
title: "My Page"
resources:
  - "sheet.xlsx"
```

Images are the most commonly used type of resource file. If you have global images (e.g. a logo) that you want to reference from various pages within your site, you can use a site-absolute path to refer to the images, and it will be automatically converted to a relative path during publishing. For example:

``` markdown
![](/images/logo.png)
```

## Dark Mode

Quarto websites can support both a light and dark mode. For example, you may use the `flatly` and `darkly` themes (which are designed to be used in tandem as dark and light appearances) as:

``` yaml
theme:
  light: flatly
  dark: darkly
```

For more about selecting the dark and light themes for your website, see [Dark Mode](../../docs/output-formats/html-themes.llms.md#dark-mode).

| Light | Dark |
|----|----|
| ![A Quarto sidebar showing a light theme. The 'Dark mode' toggle is off.](images/site-light.png) | ![A Quarto sidebar showing a dark theme. The 'Dark mode' toggle is on.](images/site-dark.png) |

When enabled, a toggle that allows your reader to control the appearance of the website will appear. The toggle will automatically be added to the website navigation as follows:

1.  If a navbar has been specified, the toggle will appear in the top right corner of the nav bar.
2.  If there is no navbar present, but a sidebar has been specified, the toggle will appear in the same location that the sidebar tools appears (adjacent to the title or logo in the sidebar).
3.  If there is no navbar or sidebar present, the toggle will appear in the top right corner of the page.
