# Positron

## Overview

Positron bundles both the Quarto CLI and the VS Code Quarto extension so it comes ready to work with Quarto out-of-the-box.

The [Quarto VS Code Extension](https://open-vsx.org/extension/quarto/quarto) provides the support for Quarto in Positron, including:

- Integrated render and preview for Quarto documents.
- Syntax highlighting for markdown and embedded languages
- Completion and diagnostics for YAML options
- Completion for embedded languages (e.g. Python, R, Julia, etc.)
- Commands and key-bindings for running cells and selected lines.
- Live preview for LaTeX math as well as Mermaid and Graphviz diagrams

The Quarto extension integrates directly with Positron’s native R and Python features. For example, here the Quarto extension runs a Python cell in the active Python Console and shows a preview of an included image.

![Screen shot of Positron editor with three vertical sections. The leftmost includes the file explorer, and quarto assist pane. The second pane is the source code for a quarto file with python code, and the active Python Console. The third shows the Environment and Plots for the active console populated with the output of the code cells.](../../../docs/tools/images/positron-python.png)

![Screen shot of Positron editor with three vertical sections. The leftmost includes the file explorer, and quarto assist pane. The second pane is the source code for a quarto file with python code, and the active Python Console. The third shows the Environment and Plots for the active console populated with the output of the code cells.](../../../docs/tools/images/positron-python-dark.png)

The Quarto extension also works well with other extensions bundled with Positron, like Jupyter extension, and those you might install separately, like the Julia extension.

## Positron Editors

Depending on your preference and the task at hand, you can author documents for rendering by Quarto using three different editors within Positron:

1.  The source code editor for editing `.qmd` documents as text.

2.  The [Visual Editor](../../../docs/tools/positron/visual-editor.llms.md) for WYSIWYG editing of `.qmd` documents.

3.  The [Notebook Editor](../../../docs/tools/positron/notebook.llms.md) for editing `.ipynb` notebooks.

We’ll cover the source code editor below, however you might also want to consult the documentation for the [Visual Editor](../../../docs/tools/positron/visual-editor.llms.md) or [Notebook Editor](../../../docs/tools/positron/notebook.llms.md) after you’ve become familiar with the basics.

## Render and Preview

The Quarto VS Code extension includes commands and keyboard shortcuts for rendering Quarto documents (both standalone and within websites or books). After rendering, `quarto preview` is used behind the scenes to provide a preview in the Viewer Pane within Positron alongside your document:

![Two windows arranged side by side. The window on the left is a qmd file opened in Positron. The contents of this document are the same as the first part of the Getting Started: Welcome section of this website. The contents of this document are rendered by Quarto in the window on the right.](../../../docs/tools/images/positron-render-dark.png)

![Two windows arranged side by side. The window on the left is a qmd file opened in Positron. The contents of this document are the same as the first part of the Getting Started: Welcome section of this website. The contents of this document are rendered by Quarto in the window on the right.](../../../docs/tools/images/positron-render.png)

To render and preview, execute the **Quarto: Preview** command. You can alternatively use the Ctrl+Shift+K keyboard shortcut, or the **Preview** button (![Preview icon](../../../docs/tools/images/vscode-preview-icon.svg)![Preview icon](../../../docs/tools/images/vscode-preview-icon-white.svg)) at the top right of the editor:

![The top of the Positron editor. The right side of the editor tab area includes a Preview button.](../../../docs/tools/images/positron-preview-button.png)

![The top of the Positron editor. The right side of the editor tab area includes a Preview button.](../../../docs/tools/images/positron-preview-button-dark.png)

> **NOTE:**
>
> Note that on the Mac you should use `Cmd` rather than `Ctrl` as the prefix for all Quarto keyboard shortcuts.

### Other Formats

The **Quarto: Preview** command renders the default format of the currently active document. If you want to preview a different format, use the **Quarto: Preview Format** command:

![The top of the Positron editor. The editor title menu is expanded and the Preview Format command is available on the menu.](../../../docs/tools/images/positron-preview-format-menu.png)

![The top of the Positron editor. The editor title menu is expanded and the Preview Format command is available on the menu.](../../../docs/tools/images/positron-preview-format-menu-dark.png)

When you execute **Preview Format**, you’ll see a quick pick list of formats to choose from (any formats declared in the document as well as some standard formats like PDF and MS Word):

![The top of the Positron editor. The command pallette shows a quick pick list of available formats to preview.](../../../docs/tools/images/positron-preview-format.png)

![The top of the Positron editor. The command pallette shows a quick pick list of available formats to preview.](../../../docs/tools/images/positron-preview-format-dark.png)

After previewing a different format, the **Quarto: Preview** command and Ctrl+Shift+K keyboard shortcut will be automatically rebound to the newly selected format for the duration of the current preview. To switch back to previewing the original format, use **Quarto: Preview Format** command again.

> **NOTE:**
>
> Embedded preview is currently supported for HTML and PDF based formats (including `revealjs` and `beamer` slideshows). However, for Word and other formats you need to use an appropriate external program to preview the output.

### Render Command

The **Quarto: Preview** command is what you will most commonly use while authoring documents. If you have a single format (e.g. HTML or PDF) then previewing also renders your document so it’s ready for distribution once you are happy with the output. However, if you have multiple formats will need to explicitly render them (as preview only renders a single format at a time). You can do this with the **Quarto: Render Document** command:

![The top of the Positron editor. The command palette shows a quick pick list of available formats to render.](../../../docs/tools/images/positron-render-command.png)

![The top of the Positron editor. The command palette shows a quick pick list of available formats to render.](../../../docs/tools/images/positron-render-command-dark.png)

If you have multiple declared formats you can render all of them. You can also selectively render any of the declared formats or other standard formats like PDF and MS Word.

## Render on Save

By default Quarto does not automatically render `.qmd` or `.ipynb` files when you save them. This is because rendering might be very time consuming (e.g. it could include long running computations) and it’s good to have the option to save periodically without doing a full render.

However, you can configure the Quarto extension to automatically render whenever you save. You can do this either within Positron settings or within the YAML options for your project or document. To configure the Positron setting, search for `quarto.render` in settings and you’ll find the **Render on Save** option:

![The Positron Quarto render settings. The Render on Save option is checked.](../../../docs/tools/images/vscode-render-on-save.png)

![The Positron Quarto render settings. The Render on Save option is checked.](../../../docs/tools/images/vscode-render-on-save-dark.png)

You might also want to control this behavior on a per-document or per-project basis. If you include the `editor: render-on-save` option in your document or project YAML it will supersede whatever your Positron setting is. For example:

``` yaml
editor:
  render-on-save: true
```

You can also enable this setting using the checkbox in the Editor toolbar:

![The Editor toolbar showing the Render on Save option checked.](../../../docs/tools/images/positron-render-on-save.png)

![The Editor toolbar showing the Render on Save option checked.](../../../docs/tools/images/positron-render-on-save-dark.png)

## External Preview

If you prefer to use an external browser for preview (or have no preview triggered at all by rendering) you can use the **Preview Type** option to specify an alternate behavior:

![Positron settings interface with 'quarto preview type' entered into the search bar. User settings reveals Quarto \> Render: Preview Type, with a dropdown to select location for document preview after render. The default, internal, is selected, which previews using a side-by-side panel in Positron. The other two options in the dropdown are external and none.](../../../docs/tools/images/vscode-preview-settings.png)

![Positron settings interface with 'quarto preview type' entered into the search bar. User settings reveals Quarto \> Render: Preview Type, with a dropdown to select location for document preview after render. The default, internal, is selected, which previews using a side-by-side panel in Positron. The other two options in the dropdown are external and none.](../../../docs/tools/images/vscode-preview-settings-dark.png)

## Code Cells

There are a variety of tools that make it easier to edit and execute code cells. Editing tools include syntax highlighting, code folding, code completion, and signature tips:

![A Quarto document in Positron with a python code cell. There is a code completion helper active in the python cell.](../../../docs/tools/images/positron-code-cell.png)

![A Quarto document in Positron with a python code cell. There is a code completion helper active in the python cell.](../../../docs/tools/images/positron-code-cell-dark.png)

For Python, R, and Julia cells, commands are available to execute the current cell, previous cells, or the currently selected line(s).

![Positron with two panes open, source code on the right, and the interactive output of that code shown in a second pane on the left.](../../../docs/tools/images/positron-execute-cell.png)

![Positron with two panes open, source code on the right, and the interactive output of that code shown in a second pane on the left.](../../../docs/tools/images/positron-execute-cell-dark.png)

Here are all of the commands and keyboard shortcuts available for executing cells:

| Quarto Command       | Keyboard Shortcut |
|----------------------|-------------------|
| Run Current Cell     | ⇧⌘ Enter          |
| Run Selected Line(s) | ⌘ Enter           |
| Run Next Cell        | ⌥⌘ N              |
| Run Previous Cell    | ⌥⌘ P              |
| Run All Cells        | ⌥⌘ R              |
| Run Cells Above      | ⇧⌥⌘ P             |
| Run Cells Below      | ⇧⌥⌘ N             |

You can quickly insert a new code cell using the Ctrl+Shift+I keyboard shortcut.

Positron includes enhanced features for R and Python code cells (e.g. completion, code execution). To get enhanced features for Julia, install the [Julia Extension](https://marketplace.visualstudio.com/items?itemName=julialang.language-julia).

### Execution Directory

The execution directory for code cells in Positron depends on the language of the code cell:

1.  **R and Python** cells will be executed in the appropriate Console in Positron. The default execution directory for the Console is folder that was opened as the workspace.

2.  **Julia** cells require the Julia Extension which runs code within the working directory of the Julia session running in the **Julia REPL** terminal. You can change this directory manually using `cd()`.

## Contextual Assistance

Positron provides code assistance for Python and R code cells in Quarto documents. This includes:

- Code completion for functions and arguments
- Help tooltips as you write, or hover over, functions
- Opening help in a dedicated Help pane when you hit F1F1 while the cursor is in a function.

For example, below the help for the `np.arange` function is shown in the Help pane.

![Screen shot of Positron editor with two vertical sections. The left section includes the source code for a quarto file with python code, and the active Python Console. The right shows the Help pane with the help for \`np.arange\` displayed.](../../../docs/tools/images/positron-help-pane.png)

![Screen shot of Positron editor with two vertical sections. The left section includes the source code for a quarto file with python code, and the active Python Console. The right shows the Help pane with the help for \`np.arange\` displayed.](../../../docs/tools/images/positron-help-pane-dark.png)

For additional contextual assistance, execute the **Quarto: Show Assist Panel** command to show a panel in the sidebar that shows contextual assistance depending on the current cursor location:

1.  A realtime preview of equations is shown when editing LaTeX math
2.  Thumbnail previews are shown when your cursor is located on a markdown image.

For example, below an image preview is shown automatically when the cursor is located in the image path in the markdown:

![Screen shot of Positron editor with three vertical sections. The leftmost includes the file explorer, and quarto assist pane. The second pane is the source code for a quarto file with python code, and the active Python Console. The third shows the Environment and Plots for the active console populated with the output of the code cells.](../../../docs/tools/images/positron-python.png)

![Screen shot of Positron editor with three vertical sections. The leftmost includes the file explorer, and quarto assist pane. The second pane is the source code for a quarto file with python code, and the active Python Console. The third shows the Environment and Plots for the active console populated with the output of the code cells.](../../../docs/tools/images/positron-python-dark.png)

## Live Preview

While editing LaTeX math or Mermaid and Graphviz diagrams, click the **Preview** button above the code (or use the Ctrl+Shift+L keyboard shortcut) to open a live preview which will update automatically as you edit.

Here we see a preview of the currently edited LaTeX equation displayed in the Quarto assist panel:

![Quarto document open in Positron with a LaTeX equation shown in the 'Quarto Equation' section of the panel to the left of the document.](../../../docs/tools/images/positron-equation.png)

![Quarto document open in Positron with a LaTeX equation shown in the 'Quarto Equation' section of the panel to the left of the document.](../../../docs/tools/images/positron-equation-dark.png)

Here we see a Graphviz diagram preview automatically updated as we edit:

![A Quarto document being edited in Positron, with a live preview of the currently edited diagram shown in a pane to the right](../../../docs/tools/images/positron-graphviz.gif)

![A Quarto document being edited in Positron, with a live preview of the currently edited diagram shown in a pane to the right](../../../docs/tools/images/positron-graphviz-dark.gif)

## YAML Intelligence

YAML code completion is available for project files, YAML front matter, and executable cell options:

![Quarto document with YAML being edited. Next to the cursor code completion helper is open showing YAML options beginning with the letters preceding the cursor ('co').](../../../docs/tools/images/positron-yaml-completion.png)

![Quarto document with YAML being edited. Next to the cursor code completion helper is open showing YAML options beginning with the letters preceding the cursor ('co').](../../../docs/tools/images/positron-yaml-completion-dark.png)

If you have incorrect YAML it will also be highlighted when documents are saved:

![Quarto document YAML metadata with an incorrect option underlined in red.](../../../docs/tools/images/positron-yaml-diagnostics.png)

![Quarto document YAML metadata with an incorrect option underlined in red.](../../../docs/tools/images/positron-yaml-diagnostics-dark.png)

## Code Snippets

Code snippets are templates that make it easier to enter repeating code patterns (e.g. code blocks, callouts, divs, etc.). Execute the **Insert Snippet** command within a Quarto document to insert a markdown snippet:

![Quarto document with dropdown 'Select a snippet' dropdown, the first item (bold - insert bold text) is selected.](../../../docs/tools/images/positron-snippets.png)

![Quarto document with dropdown 'Select a snippet' dropdown, the first item (bold - insert bold text) is selected.](../../../docs/tools/images/positron-snippets-dark.png)

### IntelliSense

Positron uses IntelliSense to suggest snippets or possible values for a specific function while typing. This is turned off by default for snippets, but not for values. To enable snippet suggestions in IntelliSense while typing or when selecting a text snippet and pressing `ctrl+space`, the setting `editor.snippetSuggestions` needs to be set to a value other than `none` (for example to `inline`).

- Press `F1` and search for `Preferences: Open Settings (UI)` or `File` \> `Preferences` \> `Settings`
- Search for following term `@lang:quarto editor.snippetSuggestions`. `Editor: Snippet Suggestions` should show up.
- Change value to a not-`none` value.

## Document Navigation

If you have a large document use the outline view for quick navigation between sections:

![Quarto document with outline view shown in left-hand panel. The outline shows the section headers of the quarto documents.](../../../docs/tools/images/positron-outline.png)

![Quarto document with outline view shown in left-hand panel. The outline shows the section headers of the quarto documents.](../../../docs/tools/images/positron-outline-dark.png)

You can also use the **Go to Symbol in Editor** command or keyboard shortcut Ctrl+Shift+O for type-ahead navigation of the current document’s outline.

Use the **Go to File** command Ctrl+P to navigate to other files and the **Go to Symbol in Workspace** command Ctrl+T for type-ahead navigation to all headings in the workspace:

![Quarto document in Positron with command palette open showing the files in the project with the entered term, 'margin'.](../../../docs/tools/images/positron-workspace-symbols.png)

![Quarto document in Positron with command palette open showing the files in the project with the entered term, 'margin'.](../../../docs/tools/images/positron-workspace-symbols-dark.png)

## Learning More

Besides the traditional source editor described above, you can also use one of the following other editors depending on your preferences and task at hand:

1.  The [Visual Editor](../../../docs/tools/positron/visual-editor.llms.md) for WYSIWYG editing of `.qmd` documents.

2.  The [Notebook Editor](../../../docs/tools/positron/notebook.llms.md) for editing `.ipynb` notebooks.
