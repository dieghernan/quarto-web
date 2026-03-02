# Project Options

Options that define the type, render targets, and output of a project. Project options are specified under the `project` key. For example:

``` yaml
project:
  type: default
  output-dir: _output
```

[TABLE]

### Preview

Specify options that control the behavior of `quarto preview` within the `preview` key. For example:

``` yaml
project:
  type: default
  output-dir: _output
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
  type: default
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
