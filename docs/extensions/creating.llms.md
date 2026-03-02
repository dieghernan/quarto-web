# Creating Extensions

## Overview

Quarto Extensions are a powerful way to modify or extend the behavior of Quarto, and can be created and distributed by anyone. There are several types of extensions available:

| Extension | Description |
|----|----|
| [Shortcodes](../../docs/extensions/shortcodes.llms.md) | Special markdown directives that generate various types of content. For example, you could create shortcodes to embed tweets or videos in a document. |
| [Filters](../../docs/extensions/filters.llms.md) | A flexible and powerful tool for introducing new global behaviors and/or new markdown rendering behaviors. For example, you could create filters to implement output folding, an image carousel, or just about anything you can imagine! |
| [Journal Articles](../../docs/journals/formats.llms.md) | Enable authoring of professional Journal articles using markdown, and produce both LaTeX (PDF) and HTML versions of the articles. |
| [Custom Formats](../../docs/extensions/formats.llms.md) | Create new output formats by bundling together document options, templates, style sheets, and other content. |
| [Revealjs Plugins](../../docs/extensions/revealjs.llms.md) | Extend the capabilities of HTML presentations created with Revealjs. |
| [Project Types](../../docs/extensions/project-types.llms.md) | Create new project project types that bundle together standard content and options, or make it easy to create a website for a custom HTML format. |
| [Starter Templates](../../docs/extensions/starter-templates.llms.md) | Help users get started with new projects by providing a template and example content. Starter templates aren’t strictly extensions (i.e. they aren’t installed in the `_extensions` directory) but they are often used with custom formats and project types. |
| [Metadata](../../docs/extensions/metadata.llms.md) | Provide YAML configuration that can be merged into existing Quarto projects. |
| [Brand](../../docs/extensions/brand.llms.md) | Distribute a [brand.yml](../../docs/authoring/brand.llms.md) file and its assets. |

## Development

Each type of extension has its own development requirements: in some cases an extension can be created with YAML metadata alone, however in many cases you’ll end up doing some custom scripting using Lua.

These articles provide in-depth documentation on learning and using Lua for extension development:

- [Lua Development](../../docs/extensions/lua.llms.md) helps you get started with Lua (the language used to create extensions)

- [Lua API Documentation](../../docs/extensions/lua-api.llms.md) provides documentation on the Pandoc and Quarto Lua APIs used for creating extensions.

## Distribution

There are two distinct ways to distribute extensions to end users:

- Publish your extension in a public GitHub repository.

- Bundle your extension into a `.zip` or `.tar.gz` archive.

[Distributing Extensions](../../docs/extensions/distributing.llms.md) goes into more depth on how to package and distribute extensions, both on GitHub and using plain gzip archives.

## Examples

The documentation linked to above provides simple motivating examples for each type of extension. Once you understand these, check out the following for more sophisticated examples of each type of extension:

The [Quarto Extensions](https://github.com/quarto-ext/) GitHub organization provides a set of extensions developed by the core Quarto team. Many of these extensions implement frequently requested features, and all of them provide sound examples of how to implement extensions.

The [Quarto Journals](https://github.com/quarto-journals/) GitHub organization contains a set of Journal Article formats developed by the core Quarto team or contributed by third parties.

Finally, most [published extensions](../../docs/extensions/index.llms.md) are hosted on GitHub and therefore have source code available that you can learn from.
