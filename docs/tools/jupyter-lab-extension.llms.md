# JupyterLab Extension

## Overview

The Quarto JuptyerLab extension enables JupyterLab Notebooks which use Quarto markdown to properly display the contents of the markdown cells. For example, when the Quarto JupyterLab extension is installed, your Notebook will show rendered previews of elements like Callouts, Divs, Mermaid charts, as well as other Quarto elements (including the document front matter as a title block).

![](images/jupyter-lab-extension.png)

## Installing the Extension

Installation depends on which version of JupyterLab you have:

## JupyterLab 4

You can install the Quarto JupyterLab extension one of two ways:

1.  **In the JupyterLab UI**: Search for ‘Quarto’ in the Extension Manager and install the `jupyterlab-quarto` extension. You’ll be prompted to refresh the page when complete.

    ![Screenshot of the Jupyter Lab Extension Manager with 'quarto' typed in the search box, and one Search Result with the name 'jupyterlab-quarto'.](../../docs/tools/images/jupyterlab-extension.png)

2.  **Using `pip`**:

    [TABLE]

## JupyterLab 3

You can install the Quarto JupyterLab extension one of two ways:

1.  Using `pip`, you can install the `jupyterlab-quarto` by executing:

    [TABLE]

    This is the preferred way to install the JupyterLab Quarto extension as this takes advantage of traditional python packaging and doesn’t require a rebuild of JupyterLab to complete the installation.

2.  In the JupyterLab UI, you can install the Quarto extension directly using the Extension Manager by searching for ‘Quarto’ and installing the `@quarto/jupyterlab-quarto` extension. To complete the installation you need to rebuild JupyterLab (you should see a prompt to complete this once you’ve installed the Quarto extension).

## Using the Extension

The Quarto extension, once installed, will automatically render the contents of markdown cells within your notebook. Cells without Quarto specific markdown will render normally, while cells containing Quarto specific markdown will show a preview of the content in a more usable form.

> **NOTE:**
>
> The Quarto contents shown in your Notebooks will not match the rendered output precisely. For example, callouts shown in the Notebook don’t change their display based upon callout options you specify in your markdown.

## Disabling the Extension

1.  If you installed the Quarto JupyterLab extension using `pip`, you can use the following commands to disable and enable the extension.

    To disable extension, use the following command:

    [TABLE]

    To enable the extension, use the following command:

    [TABLE]

2.  If you installed the Quarto JupyterLab extension using the JupyterLab Notebook Extension Manager, you can use the UI directly to disable and enable the extension.

## Uninstalling the Extension

1.  If you installed the extension using `pip`, you can uninstall the Quarto extension using `pip`, like so:

    [TABLE]

2.  If you installed the extension using the JupyterLab Notebook Extension Manager, use the Extension Manager to uninstall the extension. To complete the uninstallation you need to rebuild JupyterLab (you should see a prompt to complete this once you’ve uninstalled the Quarto extension).

## Reporting Issues

Please report issues with the Quarto JuptyerLab extension [here](https://github.com/quarto-dev/quarto/issues/new).
