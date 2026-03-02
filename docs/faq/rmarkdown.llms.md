# FAQ for R Markdown Users

Answers to R Markdown users’ most frequently asked questions about Quarto.

## On this page

- [What can I use Quarto for?](#what-can-i-use-quarto-for)
- [Quarto sounds similar to R Markdown. What is the difference and why create a new project?](#quarto-sounds-similar-to-r-markdown.-what-is-the-difference-and-why-create-a-new-project)
- [Is R Markdown going away? Will my R Markdown documents continue to work?](#is-r-markdown-going-away-will-my-r-markdown-documents-continue-to-work)
- [Should I switch from R Markdown to Quarto?](#should-i-switch-from-r-markdown-to-quarto)
- [I use X (bookdown, blogdown, etc.). What is the Quarto equivalent?](#i-use-x-bookdown-blogdown-etc..-what-is-the-quarto-equivalent)
- [Can you create custom formats for Quarto like you can for R Markdown?](#can-you-create-custom-formats-for-quarto-like-you-can-for-r-markdown)
- [When would be a good time to start new projects in Quarto rather than R Markdown?](#when-would-be-a-good-time-to-start-new-projects-in-quarto-rather-than-r-markdown)
- [Does the RStudio IDE support Quarto?](#does-the-rstudio-ide-support-quarto)
- [Does Posit Connect support Quarto?](#does-posit-connect-support-quarto)
- [Can I use `!expr` or `!r` syntax in YAML options and headers like I do in R Markdown?](#can-i-use-expr-or-r-syntax-in-yaml-options-and-headers-like-i-do-in-r-markdown)

- [Edit this page](https://github.com/quarto-dev/quarto-web/edit/main/docs/faq/rmarkdown.qmd)
- [Report an issue](https://github.com/quarto-dev/quarto-cli/issues/new/choose)

### What can I use Quarto for?

Quarto® is an open-source scientific and technical publishing system built on Pandoc. You can weave together narrative text and code to produce elegantly formatted output as documents, web pages, blog posts, books and more. 

### Quarto sounds similar to R Markdown. What is the difference and why create a new project?

At its core, Quarto works the same way as R Markdown: 

![How Quarto works: qmd to knitr to md to pandoc to multiple formats including pdf, HTML and Microsoft Word](../../docs/get-started/hello/images/rstudio-qmd-how-it-works.png)

The goal of Quarto is to make the process of creating and collaborating on scientific and technical documents dramatically better. Quarto combines the functionality of R Markdown, bookdown, distill, xaringian, etc into a single consistent system with “batteries included” that reflects everything we’ve learned from R Markdown over the past 10 years.

The number of languages and runtimes used for scientific discourse is very broad (and the Jupyter ecosystem in particular is extraordinarily popular). Quarto is at its core multi-language and multi-engine (supporting Knitr, Jupyter, and Observable today and potentially other engines tomorrow).

On the other hand, R Markdown is fundamentally tied to R which severely limits the number of practitioners it can benefit. Quarto is Posit’s attempt to bring R Markdown to everyone! Unlike R Markdown, Quarto doesn’t have a dependency or requirement for R. Quarto was developed to be multilingual, beginning with R, Python, Javascript, and Julia, with the idea that it will work even for languages that don’t yet exist.

While it is a “new” system, it should also be noted that it is highly compatible with existing content: you can render most R Markdown documents and Jupyter notebooks unmodified with Quarto. The concept is to make a major, long term investment in reproducible research, while keeping it compatible with existing formats and adaptable to the various environments users work in.

### Is R Markdown going away? Will my R Markdown documents continue to work?

R Markdown is not going away! R Markdown is used extensively and continues to work well. It will continue to be actively supported. We’re not leaving R Markdown, we’re expanding our scope. Over the years there have been many feature requests, and rather than implementing them all in R Markdown, for certain features we may refer you to Quarto. Everything that is currently in R Markdown will continue to work and be supported. There are no plans for deprecation.

Read more about this in Yihui Xie’s blog post [With Quarto Coming, is R Markdown Going Away? No.](https://yihui.org/en/2022/04/quarto-r-markdown/)

### Should I switch from R Markdown to Quarto?

If you like using R Markdown, there’s no need to switch! R Markdown will continue to be supported and work as it always has been. You’re welcome to try Quarto if you like, but there’s no need to switch. Some new features may only exist in Quarto, so if you want to use those, then that’s where you would give those a try.  

We should emphasize that switching is not imperative. While we don’t plan on major feature initiatives in R Markdown and related packages, we are going to continue to maintain them (smaller improvements and bug fixes) for a long time to come. Furthermore, since Rmd files can in most cases be rendered without modification by Quarto, you can continue using R Markdown and the switching cost will still be minimal whenever you decide to do it. 

### I use X (bookdown, blogdown, etc.). What is the Quarto equivalent?

Here are the Quarto equivalents for various packages and features of the R Markdown ecosystem (in some cases Quarto equivalents are not yet available but will be later this year):

[TABLE]

### Can you create custom formats for Quarto like you can for R Markdown?

Quarto offers an [Extension](../../docs/extensions/index.llms.md) mechanism to add features to a format using [Shortcodes](../../docs/extensions/#using-shortcodes) or [Filters](../../docs/extensions/#using-filters) but also create [custom formats](../../docs/extensions/formats.llms.md). A major difference with custom output format in R Markdown is that Quarto Extension does not use R but Lua, for example if you need to add some logic behind custom metadata fields. See [Developing with Lua](../../docs/extensions/lua.llms.md) to get started if you need use it your extension. Some of the features from R Markdown custom formats like customizing knitting behavior can also now be done in YAML with [execution options](../../docs/computations/execution-options.llms.md#knitr-options).

As example of custom formats for Quarto, [Journal Articles](../../docs/journals/index.llms.md) for Quarto are port of some custom output format inside the **rticles** R package. Extensions lives in [Quarto Journals](https://github.com/quarto-journals/) Github organization, and you can find information on how to [customize templates](../../docs/journals/templates.llms.md) and [manage Authors](../../docs/journals/authors.llms.md) for you format.

If you are an advanced developer of R Markdown custom format, the Extension mechanism may still have limitation (like pre and post processor). The Extension feature in Quarto will be improved over time - do not hesitate to share with us your use case or wished in our [Discussion Board](https://github.com/quarto-dev/quarto-cli/discussions).

### When would be a good time to start new projects in Quarto rather than R Markdown?

Quarto v1.0 was [announced at rstudio::conf(2022)](https://www.rstudio.com/blog/announcing-quarto-a-new-scientific-and-technical-publishing-system/). This is the first stable release which is already an excellent foundation for starting new projects with Quarto or migrating existing R Markdown projects ([if you are so inclined](../../docs/faq/rmarkdown.llms.md#is-r-markdown-going-away-will-my-r-markdown-documents-continue-to-work)). If you start using Quarto, please do stay updated with [latest release and changes](../../docs/download/index.llms.md) as development is very active.

### Does the RStudio IDE support Quarto?

Yes! You need to use RStudio v2022.07 or a later version, which includes support for [editing and preview of Quarto documents](../../docs/tools/rstudio.llms.md).

You can download the latest release of RStudio from <https://posit.co/download/rstudio-desktop/>.

### Does Posit Connect support Quarto?

Yes! You can publish Quarto content to Posit Connect v2021.08.0 or later. Quarto has to be enabled as documented in the Posit Connect [admin guide](https://docs.rstudio.com/connect/admin/appendix/configuration/#Quarto). Connect’s user [documentation](https://docs.rstudio.com/connect/user/quarto/) refers to [Quarto.org docs](../../docs/publishing/rstudio-connect.llms.md#rstudio-ide) on how to publish from the RStudio IDE. To publish Python-based Quarto content, you can use the [rsconnect-python CLI](https://docs.rstudio.com/rsconnect-python/) from various locations, including VSCode, JupyterLab or the terminal.

### Can I use `!expr` or `!r` syntax in YAML options and headers like I do in R Markdown?

It depends on where you use them:

- Inside knitr cells for options using YAML syntax: Yes, `!expr` can be used as [documented](../../docs/computations/r.llms.md#chunk-options). However, `!r` cannot be used because it will fail Quarto’s YAML validation.
- Inside YAML blocks for Quarto document or project configurations: No, neither `!expr` nor `!r` is supported.

Quarto differs from R Markdown because it doesn’t rely entirely on R for YAML processing. `!expr` is handled by the **yaml** R package, while `!r` is handled by **knitr** via `xfun::yaml_load()`. These are specific to R’s YAML parsing and are not supported in Quarto’s YAML metadata blocks. However, when using `engine: knitr` (the default for documents with R cells), YAML options inside knitr cells are parsed by **knitr**, allowing the use of `!expr`.

Lastly, note that Quarto’s YAML validation supports `!expr` but not `!r`. If you’re a `!r` user, switch to `!expr` for compatibility.
