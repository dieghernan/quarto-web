# Environment Variables

## Variables Quarto inspects

These are variables that you can set to control how Quarto renders documents. For example, you can set them explicitly before running `quarto render`:

``` bash
export QUARTO_R=/opt/R/4.2.3/bin
quarto render
```

You can read about other ways to set environment variables in Quarto Projects in [Environment Variables](../../docs/projects/environment.llms.md).

[TABLE]

## Variables Quarto sets

These variables are set by Quarto you can query them. For example, you can query them in an executable code cell:

## R

``` r
Sys.getenv("QUARTO_DOCUMENT_PATH")
```

## Python

``` python
import os
print(os.environ["QUARTO_DOCUMENT_PATH"])
```

## Julia

``` julia
ENV["QUARTO_DOCUMENT_PATH"]
```

[TABLE]

For more information on the JSON object referenced by `QUARTO_EXECUTE_INFO`, see [Quarto engine execution information](../../docs/advanced/quarto-execute-info.llms.md).
