> **NOTE:**
>
> The Quarto Wizard extension and listing directory website are built and maintained by [Mickaël CANOUIL, *Ph.D.*](https://mickael.canouil.fr).
>
> In this post, he explains what it is and how it can help you manage Quarto extensions directly from Positron or Visual Studio Code.

[![Cartoon](featured.png)](featured.png)

I’m absolutely thrilled to announce **Quarto Wizard 1.0.0**, a groundbreaking extension for Visual Studio Code and Positron that transforms how you interact with the Quarto ecosystem. If you’ve ever found yourself wrestling with command-line extension management or struggling to discover the perfect template for your project, this tool is about to become your new best friend.

Install it today from the [VS Code marketplace](https://marketplace.visualstudio.com/items?itemName=mcanouil.quarto-wizard) or [Open VSX Registry](https://open-vsx.org/extension/mcanouil/quarto-wizard):

- Via VS Code or Positron Extensions view:

  - Search for “Quarto Wizard”.
  - Click “Install”.

  ![Visual Studio Code Extensions Marketplace showing Quarto Wizard search results with install button. ](assets/media/extensions-marketplace-dark.png "Extensions View: Marketplace") ![Visual Studio Code Extensions Marketplace showing Quarto Wizard search results with install button. ](assets/media/extensions-marketplace-light.png "Extensions View: Marketplace")

&nbsp;

- Via the command line:

  ## Visual Studio Code

  ``` bash
  code --install-extension mcanouil.quarto-wizard
  ```

  > **TIP:**
  > Be sure to execute the command *Shell Command: Install ‘code’ command in PATH* from Visual Studio Code’s Command Palette () if you haven’t done so already.

  ## Positron

  ``` bash
  positron --install-extension mcanouil.quarto-wizard
  ```

  > **TIP:**
  > Be sure to execute the command *Shell Command: Install ‘positron’ command in PATH* from Positron’s Command Palette () if you haven’t done so already.

Quarto has revolutionised scientific and technical publishing by enabling reproducible documents that seamlessly blend code, narrative text, and visualisation. However, one persistent friction point has been managing the rich and ever-growing ecosystem of extensions and templates—until now.

##  Quarto Wizard: Your GUI for Quarto extensions

I designed **Quarto Wizard** to address a fundamental challenge I’ve observed in the community: whilst Quarto’s command-line interface is powerful, many users prefer visual interfaces for discovering, installing, and managing extensions.

### Seamless IDE integration

**Quarto Wizard integrates beautifully with both the VS Code and Positron ecosystems**, appearing as a dedicated icon in the Activity Bar alongside your other development tools. This provides instant access to extension management without disrupting your coding flow, whether you’re in Microsoft’s VS Code or Posit’s new Positron IDE.

[![Quarto Wizard Extensions Installed panel in Visual Studio Code showing no extensions installed message with green Install Extensions button. ](assets/media/vscode-activity-bar-dark.png "Quarto Wizard Explorer View (Dark)")](assets/media/vscode-activity-bar-dark.png)

[![Quarto Wizard Extensions Installed panel in Visual Studio Code showing no extensions installed message with green Install Extensions button. ](assets/media/vscode-activity-bar-light.png "Quarto Wizard Explorer View (Light)")](assets/media/vscode-activity-bar-light.png)

The solution is **multi-modal installation**: you can now install extensions through multiple pathways that suit your workflow: from the command line, through the web directory, or via the **Quarto Wizard** GUI in your IDE.

1.  Open the Command Palette ().
2.  Type `Quarto Wizard: Install Extensions` and select it.
3.  Browse the list of available Quarto extensions.
4.  Select the Quarto extension(s) you want to install.
5.  Answer the prompts to confirm the installation.

[![Quarto Wizard extension selection dialog showing list of available extensions with checkboxes including LIVE, HIGHLIGHT TEXT, GITHUB, and other Quarto extensions. ](assets/media/vscode-install-dark.png "Quarto Wizard: Install Extensions (Dark)")](assets/media/vscode-install-dark.png)

[![Quarto Wizard extension selection dialog showing list of available extensions with checkboxes including LIVE, HIGHLIGHT TEXT, GITHUB, and other Quarto extensions. ](assets/media/vscode-install-light.png "Quarto Wizard: Install Extensions (Light)")](assets/media/vscode-install-light.png)

### Intelligent extension management

The **“Recently Installed Extensions”** feature helps track your workflow and easily reproduce project setups across different environments. This is invaluable for researchers collaborating across multiple machines or teaching workshops where consistent setups are essential, regardless of whether team members use VS Code or Positron.

What makes this particularly powerful is that **Quarto Wizard** tracks which extensions were installed through its interface by adding `source` metadata to the `_extensions.yml` file, enabling seamless updates and removals.[^1] This source tracking transforms extension maintenance from manual archaeology into an effortless workflow. The extension maintains detailed metadata about installed extensions, enabling batch operations and dependency tracking. The Explorer View provides a comprehensive overview of all installed extensions with visual indicators for updates and management options.

[![Quarto Wizard Extensions Installed panel showing expanded iconify extension details with update button and version information. ](assets/media/vscode-update-dark.png "Quarto Wizard: Explorer View Update (Dark)")](assets/media/vscode-update-dark.png)

[![Quarto Wizard Extensions Installed panel showing expanded iconify extension details with update button and version information. ](assets/media/vscode-update-light.png "Quarto Wizard: Explorer View Update (Light)")](assets/media/vscode-update-light.png)

### Template workflow simplified

Beyond extension management, I’ve designed **Quarto Wizard** to ease the process of discovering and using document templates. Once you’ve selected a template, **Quarto Wizard** lets you customise and save the document. The file is not created until you confirm, allowing you to adjust the filename and location.

1.  Open the Command Palette ().
2.  Type `Quarto Wizard: Use Template` and select it.
3.  Browse the list of available Quarto templates.
4.  Select the Quarto template(s) you want to use.
5.  Answer the prompts to confirm the selection.

[![Visual Studio Code showing Quarto Wizard with installed extensions list and document editor displaying invoice template with YAML frontmatter. ](assets/media/vscode-template-dark.png "Quarto Wizard: Use Template (Dark)")](assets/media/vscode-template-dark.png)

[![Visual Studio Code showing Quarto Wizard with installed extensions list and document editor displaying invoice template with YAML frontmatter. ](assets/media/vscode-template-light.png "Quarto Wizard: Use Template (Light)")](assets/media/vscode-template-light.png)

## Powered by a comprehensive extension directory

### A curated catalogue of 250+ extensions

At the heart of **Quarto Wizard** lies the [Quarto Extensions directory (m.canouil.dev/quarto-extensions/)](https://m.canouil.dev/quarto-extensions/), a comprehensive listing I maintain that catalogues extensions from across the entire Quarto ecosystem.

[![Quarto Extensions website displaying grid of extension cards including webr, Reveal.js Clean theme, and Hikmah Academic templates. ](assets/media/quarto-extensions-home-dark.png "Mickaël CANOUIL's Quarto Extensions directory")](assets/media/quarto-extensions-home-dark.png)

[![Quarto Extensions website displaying grid of extension cards including webr, Reveal.js Clean theme, and Hikmah Academic templates. ](assets/media/quarto-extensions-home-light.png "Mickaël CANOUIL's Quarto Extensions directory")](assets/media/quarto-extensions-home-light.png)

To date, it includes over 250 extensions contributed by the community, covering a vast array of functionalities from citation management to interactive visualisations. This directory powers **Quarto Wizard**’s discovery features, providing rich metadata about each extension including descriptions, licensing, version tags, and GitHub stars. The directory is continuously updated through GitHub’s API, ensuring you always have access to the latest extensions from the community.

### One-click installation from the web

What’s particularly exciting is that you can install extensions or use templates **directly from the website itself**. Each extension listed at [m.canouil.dev/quarto-extensions/](https://m.canouil.dev/quarto-extensions/) includes multiple installation options: traditional command-line via terminal, or one-click installation through **Quarto Wizard** in VS Code, Positron, or VSCodium. Simply browse the directory, find the extension you need, and choose your preferred installation method. The website generates the appropriate commands or launches your IDE directly. This flexibility means teams with mixed technical backgrounds can all access the same powerful extensions.

[![Quarto Extensions website with Install Options popup showing manual terminal command and Quarto Wizard installation options for Visual Studio Code, Positron, and VSCodium. ](assets/media/quarto-extensions-modal-dark.png "Mickaël CANOUIL's Quarto Extensions install modal")](assets/media/quarto-extensions-modal-dark.png)

[![Quarto Extensions website with Install Options popup showing manual terminal command and Quarto Wizard installation options for Visual Studio Code, Positron, and VSCodium. ](assets/media/quarto-extensions-modal-light.png "Mickaël CANOUIL's Quarto Extensions install modal")](assets/media/quarto-extensions-modal-light.png)

For example, you might want to add the [**Iconify**](https://github.com/mcanouil/quarto-iconify) extension to access over 200,000 open source vector icons in your documents, or the [**Animate**](https://github.com/mcanouil/quarto-animate) extension to bring your presentations to life with CSS animations. Perhaps the [**Spotlight**](https://github.com/mcanouil/quarto-spotlight) extension for Reveal.js catches your eye for creating dramatic Reveal.js presentations that highlight your mouse position. All of these extensions (and hundreds more) are just a click away.

### Template discovery made easy

Additionally, the Quarto Extensions directory excels at **template discovery and deployment** which is enhanced with powerful filtering options: you can sort by recently updated, filter by popularity, browse by categories (*i.e.*, Shortcodes, Filters, Formats, Projects, Reveal.js Plugins), or search for specific functionality. Each extension clearly indicates whether it’s a template with **“Use”** buttons alongside **“Install”** options.

[![Quarto Extensions website in list view showing Template extensions with install and use buttons. ](assets/media/quarto-extensions-template-dark.png "Mickaël CANOUIL's Quarto Extensions list view filtered by formats")](assets/media/quarto-extensions-template-dark.png)

[![Quarto Extensions website in list view showing Template extensions with install and use buttons. ](assets/media/quarto-extensions-template-light.png "Mickaël CANOUIL's Quarto Extensions list view filtered by formats")](assets/media/quarto-extensions-template-light.png)

Whether you’re crafting an academic paper using journal-specific formats, creating professional invoices with my [**Invoice**](https://github.com/mcanouil/quarto-invoice) extension template, or building stunning presentations with themed templates like my [**Reveal.js Coeos**](https://github.com/mcanouil/quarto-revealjs-coeos) extension, browsing available templates becomes as simple as scrolling through a curated gallery.

This directory creates a seamless experience: instead of manually searching GitHub repositories or memorising command-line syntax, you can browse hundreds of extensions with detailed information at your fingertips. This transforms extension discovery from a treasure hunt into a curated shopping experience.

## Addressing real workflow friction

I designed **Quarto Wizard** and the extension directory at [m.canouil.dev/quarto-extensions](https://m.canouil.dev/quarto-extensions/) to directly tackle several persistent Quarto pain points I’ve encountered:

- **Discovery challenges**: Finding relevant extensions in the growing ecosystem becomes intuitive through the visual browser interface powered by the comprehensive extensions directory.

- **Command-line intimidation**: Users who prefer graphical interfaces no longer need to memorise terminal commands.

- **Document setup complexity**: Template-based document initialisation eliminates manual YAML configuration.

- **Extension maintenance**: Updates, removals, and dependency management become point-and-click operations rather than command-line archaeology.

- **Source tracking**: **Quarto Wizard** automatically adds source metadata to installed extensions, enabling future updates and proper version management.

- **Stable installations**: **Quarto Wizard** installs extensions from GitHub releases/tags by default instead of the potentially unstable default branch, ensuring more reliable installations and more replicable environments.

## Perfect for diverse use cases

The extension shines across multiple scenarios:

- **Academic researchers** can quickly install citation management tools, bibliography extensions like [**Multibib**](https://github.com/pandoc-ext/multibib) or [**Section Bibliographies**](https://github.com/pandoc-ext/section-bibliographies), and journal-specific formatting, whether they’re using VS Code or Positron for their analysis work.

- **Data scientists** gain easy access to computational extensions like [**WebR**](https://github.com/coatless/quarto-webr), visualisation tools, and interactive notebook capabilities. This is particularly powerful in Positron, which is designed specifically for data science workflows.

- **Technical writers** can browse and install extensions for enhanced typography with for example the [**Highlight Text**](https://github.com/mcanouil/quarto-highlight-text) extension for multi-format text highlighting, code highlighting, and advanced formatting options of their Reveal.js presentations with [**Reveal.js Editable**](https://github.com/EmilHvitfeldt/quarto-revealjs-editable) extension in their preferred IDE.

- **Workshop instructors** can ensure all participants have consistent extension setups through guided installation processes, regardless of whether attendees prefer VS Code or Positron.

## Future-ready architecture

I’ve built **Quarto Wizard** on robust foundations that ensure long-term reliability. The extension integrates with GitHub’s API through the [Quarto Extensions directory](https://m.canouil.dev/quarto-extensions/) for real-time metadata, includes attestation verification for security, and maintains full compatibility with both VS Code and Positron environments.

The modular architecture allows for future enhancements whilst maintaining backwards compatibility. As the Quarto ecosystem continues expanding and as Positron evolves alongside VS Code, **Quarto Wizard** will support new extension types and project management workflows in both environments.

## Getting started today

Begin your **Quarto Wizard** journey by installing the extension from the VS Code marketplace, the Open VSX Registry, or directly through your IDE’s Extensions view. Once installed, the **Quarto Wizard** icon appears in your Activity Bar, providing immediate access to extension management and project tools.

You have multiple paths to explore Quarto extensions:

1.  **Through Quarto Wizard**: Click the **Quarto Wizard** icon in your IDE’s Activity Bar and browse the integrated catalogue.
2.  **Via the web directory**: Visit [m.canouil.dev/quarto-extensions](https://m.canouil.dev/quarto-extensions/) where you can browse all extensions and install them directly from the website. Each extension offers installation buttons for **Quarto Wizard**, VS Code, Positron, VSCodium, or traditional terminal commands.
3.  **Traditional command-line**: Use the familiar `quarto add` commands if you prefer.

Try installing your first extension: perhaps [**Iconify**](https://github.com/mcanouil/quarto-iconify) extension for comprehensive icon support or [**GitHub**](https://github.com/mcanouil/quarto-github) for seamless GitHub linking. Whether you click “Install” on the website, use **Quarto Wizard**’s interface, or type commands in the terminal, the choice is yours. The difference in experience compared to traditional command-line installation is immediately apparent, especially when browsing the visual catalogue with its filtering options, popularity indicators, and rich metadata.

I believe **Quarto Wizard** represents a significant step forward in making Quarto’s powerful publishing capabilities accessible to users regardless of their comfort level with command-line tools or their choice of IDE. By providing intuitive visual interfaces for complex operations, **Quarto Wizard** democratises access to the rich Quarto ecosystem whilst maintaining the flexibility and power that makes Quarto exceptional.

The future of reproducible publishing is here, and it’s more accessible than ever in whichever modern development environment you prefer.

## Footnotes

[^1]: Quarto CLI does not natively track installation sources as of version 1.8.24 ([quarto-dev/quarto-cli#11468](https://github.com/quarto-dev/quarto-cli/issues/11468)).
