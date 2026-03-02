# Videos

## Overview

You can embed videos in documents using the `{{< video >}}` shortcode. For example, here we embed a YouTube video:

``` markdown
{{< video https://www.youtube.com/embed/wo9vZccmqwc >}}
```

Videos can refer to video files (e.g. `.mp4`) or can be links to videos published on YouTube, Vimeo, or Brightcove.

Here are some additional examples that demonstrate using various video sources and options:

``` default
{{< video local-video.mp4 >}}

{{< video https://www.youtube.com/embed/wo9vZccmqwc >}}

{{< video https://vimeo.com/548291297 >}}

{{< video https://youtu.be/wo9vZccmqwc width="400" height="300" >}}

{{< video https://www.youtube.com/embed/wo9vZccmqwc
    title="What is the CERN?"
    start="116"
    aspect-ratio="21x9" 
>}}
```

In HTML formats the video will be embedded within the document. For other formats, a simple link to the video will be rendered.

Next, we’ll cover the various options available for video embedding. For additional details on using videos within Revealjs presentations (including how to create slides with full-screen video backgrounds), see the [Revealjs](#revealjs) section below.

## Video URL

The video URL can specify either a path to a video file (e.g. a `.mp4`) alongside the document, a remote URL to a video file, or a URL to a video service (YouTube, Vimeo, or Brightcove).

These are valid URLs for video files:

``` default
{{< video local-video.mp4 >}}
{{< video https://videos.example.com/video.mp4 >}}
```

For video services, a variety of URL forms are supported. For example, the following video service URLs are all valid:

``` default
{{< video https://youtu.be/wo9vZccmqwc >}}
{{< video https://www.youtube.com/watch?v=wo9vZccmqwc >}}
{{< video https://www.youtube.com/embed/wo9vZccmqwc >}}
{{< video https://vimeo.com/548291297 >}}
{{< video https://players.brightcove.net/1460825906/default_default/index.html?videoId=5988531335001 >}}
```

Note that YouTube videos support both the URL that is available in the address bar when watching a video as well as the standard URLs used for linking and embedding. Brightcove videos are embedded using the standard [iframe embed code](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.llms.md).

## Options

### Aspect Ratio

Videos are automatically rendered responsively using the full width of the document’s main text column. The `aspect-ratio` specifies how the height should vary with changes in width. For example:

``` default
{{< video https://youtu.be/wo9vZccmqwc aspect-ratio="4x3" >}}
```

Available [aspect ratios](https://getbootstrap.com/docs/5.0/helpers/ratio/#aspect-ratios) include `1x1`, `4x3`, `16x9` (the default), and `21x9`.

#### Width and Height

You can disable responsive sizing by providing explicit `width` and `height` attributes. For example:

``` default
{{< video https://youtu.be/wo9vZccmqwc width="250" height="175" >}}
```

This will produce a video that renders at the specified dimensions and is not responsive. Note that when no `height` or `width` are specified, videos will size responsively given the space available to them.

### Start Time

For YouTube videos, you can specify a `start` option to indicate how many seconds into the video you want to start playing:

``` default
{{< video https://youtu.be/wo9vZccmqwc start="10" >}}
```

### Frame Title

The `title` option adds a `title` attribute to the video `<iframe>`:

``` default
{{< video https://www.youtube.com/embed/wo9vZccmqwc 
    title='What is the CERN?' 
>}}
```

## Revealjs

You can include videos within [Revealjs](../../docs/presentations/revealjs/index.llms.md) presentations in one of two ways:

- A video that appears within the contents of a slide.

- A video that occupies the entire background of a slide.

### Slide Content

Here’s a video on a slide without a title:

``` default
---

{{< video https://youtu.be/wo9vZccmqwc width="100%" height="100%" >}}
```

Note that we set the `width` and `height` explicitly to 100% so that the video fills the slide.

Here’s a video on a slide with a title.

``` default
## Video Slide 

{{< video https://youtu.be/wo9vZccmqwc width="100%" height="85%" >}}
```

Note that we set the `height` to 85% to leave room for the title.

### Backgrounds

For videos on slides without titles, you might prefer to have the video fill the entire background of the slide. You can do this using the `background-video` attribute. For example:

``` markdown
## {background-video="intro-cern.mp4"}

## {background-video="https://videos.example.com/intro-cern.mp4"}

## {background-video="https://youtu.be/wo9vZccmqwc?autoplay=1"}

## {background-video="https://vimeo.com/548291297"}
```

Note that when using `background-video` for video files (as distinct from services like YouTube) you can specify a number of other attributes, including:

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

## Cross-References

To add a cross-reference to a video, use the [cross-reference div syntax](../../docs/authoring/cross-references-divs.llms.md) and treat it like a figure. For example,

``` markdown
::: {#fig-cern}

{{< video https://www.youtube.com/embed/wo9vZccmqwc >}}

The video "CERN: The Journey of Discovery"

:::

In @fig-cern...
```

Which renders as:

![Screenshot that shows a YouTube video followed by the caption, 'Figure 1: The video CERN: The Journey of Discovery'. Below the caption is the text 'In Figure 1 ...'.](images/crossrefs-video.png)

If you would rather give videos a label and counter distinct from figures, consider defining [Custom Cross-Reference Types](../../docs/authoring/cross-references-custom.llms.md).
