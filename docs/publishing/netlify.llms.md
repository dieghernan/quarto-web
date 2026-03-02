# Netlify

## Overview

[Netlify](https://www.netlify.com/) is a professional web publishing platform with support for many advanced features including custom domains, authentication, branch previews, and instant rollbacks. Netlify also has a free plan that is ideal for personal projects, hobby sites, or experiments.

There are several ways to publish Quarto content to Netlify:

1.  Use the `quarto publish` command to publish content rendered on your local machine.

2.  If you are using GitHub, GitLab, Bitbucket, or Azure DevOps, you can point Netlify at your site’s source code and have it deployed whenever your code changes.

3.  If you are using GitHub, you can use a [GitHub Action](#github-action) to automatically render your project and publish the resulting content whenever your code changes.

4.  If you are using another Continuous Integration (CI) service, you can script the `quarto publish` command to render and publish content to Netlify.

We’ll cover each of these methods below, starting with the most straightforward and then proceeding to more sophisticated scenarios.

## Publish Command

The `quarto publish` command is the easiest way to publish locally rendered content. From the directory where your project is located, execute the `quarto publish` command for Netlify:

``` bash
quarto publish netlify
```

If you haven’t published to Netlify before, the publish command will prompt you to authenticate. After confirming that you want to publish, your content will be rendered and deployed, and then a browser opened to view your site.

### \_publish.yml

The `_publish.yml` file is used to specify the publishing destination. This file is automatically created (or updated) whenever you execute the `quarto publish` command, and is located within the project or document directory.

The service, id, and URL of the published content is specified in `_publish.yml`. For example:

``` yaml
- source: project
  netlify:
    - id: "5f3abafe-68f9-4c1d-835b-9d668b892001"
      url: "https://tubular-unicorn-97bb3c.netlify.app"
```

If you have an existing Netlify site that you want to publish to, you should manually create a `_publish.yml` file that looks like the example above, but with the appropriate `id` and `url` values for your site.

Account information is not stored in `_publish.yml`, so it is suitable for checking in to version control and being shared by multiple publishers.

### Options

You can customize the behavior of `quarto publish` by providing the following command line options:

| Option         | Behavior                                  |
|----------------|-------------------------------------------|
| `--no-prompt`  | Do not prompt to confirm publish actions. |
| `--no-browser` | Do not open a browser after publish.      |
| `--no-render`  | Do not re-render prior to publish         |

To publish a document rather than a website or book, provide the path to the document:

``` bash
quarto publish netlify document.qmd
```

### Domain Name

The domain name for your published site will by default use a random identifier (e.g. `mystifying-jepsen-fa4396.netlify.app`). You can pick a more descriptive sub-domain (still using `netlify.app` as the main domain) or if you own another domain, assign that one to the site. These options are available (respectively) from the **Site settings** and **Domain settings** panels:

![](images/netlify-control-panel.png)

Within **Site settings**, click the **Change site name** button to specify a different sub-domain:

![](images/netlify-site-settings.png)

If you own another domain that you want to use for your site, follow the directions in **Domain settings**.

## Publish from Git Provider

Netlify has the ability to automatically deploy sites when changes are committed to Git repositories hosted on GitHub, GitLab, Bitbucket, and Azure DevOps. The most straightforward approach to this is to check your rendered site (i.e. the `_site` or `_book` directory) into version control and have Netlify deploy that. We’ll cover that scenario first and then explore using a Netlify Build Plugin to render the site on Netlify servers.

### Importing a Project

Start by going to the main Netlify page for your team, choosing **Add new site,** and then **Import an existing project**:

![](images/netlify-import-project.png)

You’ll be prompted to authenticate with your version control provider, select a repository, and then finally specify the configuration for publishing the site.

### Publishing Configuration

The build settings for our project will have no **Build command** and will specify `_site` or `_book` (as appropriate) for the **Publish directory**:

![](images/netlify-build-settings.png)

If you have your `_site` or `_book` directory checked into version control then everything is now configured and your site will be deployed to Netlify automatically whenever you commit to your repository.

### Rendering on Netlify

If you prefer not to check your rendered site into version control, you can also use the Quarto [Netlify Build Plugin](https://github.com/quarto-dev/netlify-plugin-quarto) to render on a Netlify build server (note that Netlify servers can only render markdown and cannot execute R, Python, or Julia code).

#### Freezing Computations

To make sure that R, Python, and Julia code is only executed locally, configure your project to use Quarto’s [freeze](../projects/code-execution.llms.md#freeze) feature by adding this to your `_quarto.yml`:

``` yaml
execute:
  freeze: auto
```

Now, fully re-render your site:

``` bash
quarto render
```

If you have executable code in your project you’ll notice that a `_freeze` directory has been created at the top level of your project. This directory stores the results of computations and should be checked in to version control. Whenever you change a `.qmd` file with executable code, it will automatically be re-run during your next render and the updated computations will be stored in `_freeze`.

#### Ignoring Output

It’s important to note that you don’t need to check your `_site` or `_book` directory into version control (if you have done this in the past you know it makes for very messy diffs!). Before proceeding you should add the output directory of your project to `.gitignore`. For example:

``` bash
/.quarto/
/_site/
```

If you’ve already checked these files into source control you may need to remove them explicitly:

``` bash
git rm -r _site
```

#### Plugin Configuration

To use the Quarto Netlify Build Plugin, add the following two files to your project:

``` toml
[[plugins]]
package = "@quarto/netlify-plugin-quarto"
```

``` json
{
  "dependencies": {
    "@quarto/netlify-plugin-quarto": "^0.0.5"
  }
}
```

Now, commit and push your modified project (including `_freeze`, `netlify.toml`, and `package.json`). Assuming that you configured the project correctly in the previous step (i.e. **Publish directory** set to the `_site` or `_book` directory) then Netlify will begin rendering and publishing your site each time you push a new commit.

## GitHub Action

Using the `quarto publish netlify` command to publish locally rendered content is the most simple and straightforward way to publish. Another option is to use [GitHub Actions](https://docs.github.com/en/actions) to render and publish your site (you might prefer this if you want execution and/or rendering to be automatically triggered from commits).

There are a few different ways to approach rendering and publishing content. Below, we’ll provide a how-to guide for publishing with GitHub Actions. For more conceptual background on the various approaches, see the discussion on [Rendering for CI](../../docs/publishing/ci.llms.md#rendering-for-ci).

### Publish Record

Prior to attempting to publish with a GitHub Action, you should have completed at least one publish using the [Publish Command](#publish-command) (described immediately above). This publish will create a `_publish.yml` file that records the publishing destination to be used by the GitHub Action. For example:

``` yaml
- source: project
  netlify:
    - id: "5f3abafe-68f9-4c1d-835b-9d668b892001"
      url: "https://tubular-unicorn-97bb3c.netlify.app"
```

You can also manually create a `_publish.yml` file that looks like the example above, but with the appropriate `id` and `url` values for your site.

Do not proceed to the next step(s) until you have a `_publish.yml` that indicates your publishing destination.

### Freezing Computations

To make sure that R, Python, and Julia code is only executed locally, configure your project to use Quarto’s [freeze](../projects/code-execution.llms.md#freeze) feature by adding this to your `_quarto.yml`:

``` yaml
execute:
  freeze: auto
```

Now, fully re-render your site:

``` bash
quarto render
```

If you have executable code in your project you’ll notice that a `_freeze` directory has been created at the top level of your project. This directory stores the results of computations and should be checked in to version control. Whenever you change a `.qmd` file with executable code, it will automatically be re-run during your next render and the updated computations will be stored in `_freeze`.

Note that an alternative approach is to execute the code as part of the GitHub Action. For now we’ll keep things simpler by executing code locally and storing the computations by using freeze. Then, further below, we’ll cover [Executing Code](#executing-code) within a GitHub Action.

### Publish Action

Add a `publish.yml` GitHub Action to your project by creating this YAML file and saving it to `.github/workflows/publish.yml`:

``` yaml
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v4 

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render and Publish 
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: netlify
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

### Netlify Credentials

The final step is to configure your GitHub Action with the credentials required for publishing to Netlify. To do this you need to create a Netlify personal access token and then configure your GitHub action to be able to read it:

1.  If you don’t already have an access token, go to the Netlify [applications page](https://app.netlify.com/user/applications), and click on **New Access Token** to create a new personal access token. Give this token a memorable name, and copy the token to the clipboard.

2.  Add the Netlify personal access token to your repository’s action **Secrets** (accessible within repository **Settings**). You will see a **New repository secret** button at the top right:

    ![](images/gh-new-repository-secret.png)

    Click the button and add the personal access token from step 1 as a secret named `NETLIFY_AUTH_TOKEN`:

    ![](images/netlify-gh-action-secret.png)

### Ignoring Output

It’s important to note that you don’t need to check your `_site` or `_book` directory into version control (if you have done this in the past you know it makes for very messy diffs!). Before proceeding you should add the output directory of your project to `.gitignore`. For example:

``` bash
/.quarto/
/_site/
```

If you’ve already checked these files into source control you may need to remove them explicitly:

``` bash
git rm -r _site
```

### Commit to Publish

Once you’ve specified your publishing action and Netlify credentials, and pushed your updated repository (including the `_freeze` directory) to GitHub, your action will run with this and subsequent commits, automatically rendering and publishing to Netlify.

### Executing Code

If you prefer, you can also configure a GitHub Action to execute R, Python, or Julia code as part of rendering. While this might reflexively seem like the best approach, consider the following requirements imposed when you execute code within a CI service like GitHub Actions:

- You need to reconstitute all of the dependencies (R, Python, or Julia plus the correct versions of required packages) in the CI environment.

- If your code requires any special permissions (e.g. database or network access) those permissions also need to be present on the CI server.

- Your project may contain documents that can no longer be easily executed (e.g. blog posts from several years ago that use older versions of packages). These documents may need to have `freeze` individually enabled for them to prevent execution on CI.

#### Prerequisites

The best way to ensure that your code can be executed within a GitHub Action is to use a virtual environment like [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment) or [renv](https://rstudio.github.io/renv/articles/renv.llms.md) with your project (below we’ll provide example actions for each). If you aren’t familiar with using these tools check out the article on using [Virtual Environments](../../docs/projects/virtual-environments.llms.md) with Quarto to learn more.

Once you’ve decided to execute code within your GitHub Action you can remove the `freeze: auto` described above from your `_quarto.yml` configuration. Note that if you want to use `freeze` selectively for some documents or directories that is still possible (for a directory, create a `_metadata.yml` file in the directory and specify your freeze configuration there—this is what Quarto does by default for the `posts` folder of blog projects).

#### Example: Jupyter with venv

Here is a complete example of a GitHub Action that installs Python, Jupyter, and package dependencies from `requirements.txt`, then executes code and renders output to Netlify:

``` yaml
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v4 

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
        
      - name: Install Python and Dependencies
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
          cache: 'pip'
      - run: pip install jupyter
      - run: pip install -r requirements.txt
      
      - name: Render and Publish 
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: netlify
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

#### Example: Knitr with renv

Here is a complete example of a GitHub Action that installs R and package dependencies from `renv.lock`, then executes code and renders output to Netlify:

``` yaml
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v4 

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
        
      - name: Install R
        uses: r-lib/actions/setup-r@v2
        with:
          r-version: '4.2.0'
      
      - name: Install R Dependencies 
        uses: r-lib/actions/setup-renv@v2
        with:
          cache-version: 1
      
      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: netlify
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

### Additional Options

It’s possible to have a Quarto project in a larger GitHub repository, where the Quarto project does not reside at the top-level directory. In this case, add a `path` input to the invocation of the `publish` action. For example:

``` yaml
- name: Render and Publish
  uses: quarto-dev/quarto-actions/publish@v2
  with:
    target: netlify
    path: subdirectory-to-use
    NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

By default, `quarto publish` will re-render your project before publishing it. However, if you store the rendered output in version control, you don’t need the GitHub action to re-render the project. In that case, add the option `render: false` to the `publish` action:

``` yaml
- name: Render and Publish
  uses: quarto-dev/quarto-actions/publish@v2
  with:
    target: netlify
    render: false
    NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

## Continuous Integration

You can publish Quarto content to Netlify using any CI service by scripting the `quarto publish` command.

For example, here is a shell script that publishes to Netlify based on the information in a `_publish.yml` file in the root of the project:

``` bash
# credentials from https://app.netlify.com/user/applications
export NETLIFY_AUTH_TOKEN="45fd6ae56c"

# publish to the netlify site id provided within _publish.yml
quarto publish netlify
```

Here are the contents of `_publish.yml`:

``` yaml
- source: project
  netlify:
    - id: "5f3abafe-68f9-4c1d-835b-9d668b892001"
      url: "https://tubular-unicorn-97bb3c.netlify.app"
```

Here is another variation that provides the publish target on the command line:

``` bash
quarto publish netlify --id 5f3abafe-68f9-4c1d-835b-9d668b892001
```

See the article on [Publishing with CI](../../docs/publishing/ci.llms.md) for additional details on the various approaches to rendering and publishing with Continuous Integration.
