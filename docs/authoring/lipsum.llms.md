# Adding Placeholder Text to Your Documents

## Overview

When you need to visualize how text will look in your document or your website, the `{{< lipsum >}}` shortcode comes in handy. It inserts “Lorem Ipsum” dummy text, which is standard placeholder text used in the publishing and design industries.

## Example

Here’s an example of `lipsum` generating two paragraphs of text, by adding `{{< lipsum 2 >}}` in a paragraph by itself.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis sagittis posuere ligula sit amet lacinia. Duis dignissim pellentesque magna, rhoncus congue sapien finibus mollis. Ut eu sem laoreet, vehicula ipsum in, convallis erat. Vestibulum magna sem, blandit pulvinar augue sit amet, auctor malesuada sapien. Nullam faucibus leo eget eros hendrerit, non laoreet ipsum lacinia. Curabitur cursus diam elit, non tempus ante volutpat a. Quisque hendrerit blandit purus non fringilla. Integer sit amet elit viverra ante dapibus semper. Vestibulum viverra rutrum enim, at luctus enim posuere eu. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.

Nunc ac dignissim magna. Vestibulum vitae egestas elit. Proin feugiat leo quis ante condimentum, eu ornare mauris feugiat. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Mauris cursus laoreet ex, dignissim bibendum est posuere iaculis. Suspendisse et maximus elit. In fringilla gravida ornare. Aenean id lectus pulvinar, sagittis felis nec, rutrum risus. Nam vel neque eu arcu blandit fringilla et in quam. Aliquam luctus est sit amet vestibulum eleifend. Phasellus elementum sagittis molestie. Proin tempor lorem arcu, at condimentum purus volutpat eu. Fusce et pellentesque ligula. Pellentesque id tellus at erat luctus fringilla. Suspendisse potenti.

## Usage

``` markdown
{{< lipsum 1 >}}
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis sagittis posuere ligula sit amet lacinia. Duis dignissim pellentesque magna, rhoncus congue sapien finibus mollis. Ut eu sem laoreet, vehicula ipsum in, convallis erat. Vestibulum magna sem, blandit pulvinar augue sit amet, auctor malesuada sapien. Nullam faucibus leo eget eros hendrerit, non laoreet ipsum lacinia. Curabitur cursus diam elit, non tempus ante volutpat a. Quisque hendrerit blandit purus non fringilla. Integer sit amet elit viverra ante dapibus semper. Vestibulum viverra rutrum enim, at luctus enim posuere eu. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.

`lipsum` takes an optional parameter, in two possible formats:

- `{{< lipsum nparas >}}`: `nparas` describes the number of paragraphs of placeholder text to include in the document.
- `{{< lipsum start-end >}}`: `start` and `end` are two numbers that describe the range of lorem ipsum paragraphs to include in the document.

`lipsum` produces placeholder text in a predictable manner[^1]. This means that the same parameters will always yield identical text. However, you can choose to set `random=true` to generate a paragraph or a random collection of paragraphs.

- `{{< lipsum 1 random=true >}}`: This will generate a single paragraph of random lorem ipsum text.

## Footnotes

[^1]: Since Quarto 1.7.14. Earlier versions of Quarto generate random text.
