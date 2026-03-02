# Publishing Basics

## Overview

There are a wide variety of ways to publish documents, presentations, and websites created using Quarto. Since content rendered with Quarto uses standard formats (HTML, PDFs, MS Word, etc.) it can be published anywhere. Additionally, there is a `quarto publish` command available for easy publishing to various popular services (GitHub, Netlify, Posit Connect, etc.) as well as various tools to make it easy to publish from a Continuous Integration (CI) system.

## Getting Started

To get started, review the documentation for using one of the following publishing services:

| Destination | Description |
|----|----|
| [Quarto Pub](../../docs/publishing/quarto-pub.llms.md) | Publishing service for Quarto documents, websites, and books. Use Quarto Pub when you want a free, easy to use service for publicly available content. |
| [GitHub Pages](../../docs/publishing/github-pages.llms.md) | Publish content based on source code managed within a GitHub repository. Use GitHub Pages when the source code for your document or site is hosted on GitHub. |
| [Posit Connect](../../docs/publishing/rstudio-connect.llms.md) | Publishing platform for secure sharing of data products within an organization. Use Posit Connect when you want to publish content within an organization rather than on the public internet. |
| [Netlify](../../docs/publishing/netlify.llms.md) | Professional web publishing platform. Use Netlify when you want support for custom domains, authentication, previewing branches, and other more advanced capabilities. |
| [Confluence](../../docs/publishing/confluence.llms.md) | Publishing platform for supporting team collaboration. Use Confluence to share documents in team Spaces. |
| [Hugging Face Spaces](../../docs/publishing/hugging-face.llms.md) | Publishing platform specializing in learning models and datasets. Use Hugging Face Spaces when you want to share Quarto documents together with associated machine learning models and/or datasets. |
| [Other Services](../../docs/publishing/other.llms.md) | Content rendered with Quarto uses standard formats (HTML, PDFs, MS Word, etc.) that can be published anywhere. Use this if none of the methods above meets your requirements. |

If you don’t know which to choose, try [Quarto Pub](../../docs/publishing/quarto-pub.llms.md) which is a free service for publicly available content. If you are publishing to a destination not listed above, choose [Other Services](../../docs/publishing/other.llms.md).

These articles cover both straightforward direct publishing as well as Continuous Integration (CI) publishing with GitHub Actions. If you want to publish using CI and aren’t using GitHub Actions, the article on [Publishing with CI](../../docs/publishing/ci.llms.md) provides additional details and documentation.
