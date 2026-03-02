# Quarto Pub

## Overview

[Quarto Pub](https://quartopub.com) is a free publishing service for static content created with Quarto. Quarto Pub is ideal for blogs, course or project websites, books, presentations, and personal hobby sites.

It’s important to note that all documents and sites published to Quarto Pub are **publicly visible**. You should only publish content you wish to share publicly.

There are two ways to publish content to Quarto Pub (both are covered in more detail below):

1.  Use the `quarto publish` command to publish content rendered on your local machine (this is the recommend approach when you are getting started).

2.  If you are using GitHub, you can use a [GitHub Action](#github-action) to automatically render your project and publish the resulting content whenever your code changes.

Before attempting your first publish, be sure that you have created a free [Quarto Pub](https://quartopub.com) account.

> **NOTE:**
>
> Quarto Pub sites are publicly visible, can be no larger than 100 MB and have a *soft* limit of 10 GB of bandwidth per month. If you want to authenticate users, host larger sites, or use a custom domain, consider using a professional web publishing service like [Netlify](../../docs/publishing/netlify.llms.md) instead.

## Publish Command

The `quarto publish` command is the easiest way to publish locally rendered content. From the directory where your project is located, execute the `quarto publish` command for Quarto Pub:

``` bash
quarto publish quarto-pub
```

If you haven’t published to Quarto Pub before, the publish command will prompt you to authenticate. After confirming that you want to publish, your content will be rendered and deployed, and then a browser opened to view your site.

### \_publish.yml

The `_publish.yml` file is used to specify the publishing destination. This file is automatically created (or updated) whenever you execute the `quarto publish` command, and is located within the project or document directory.

The service, id, and URL of the published content is specified in `_publish.yml`. For example:

``` yaml
- source: project
  quarto-pub:
    - id: "5f3abafe-68f9-4c1d-835b-9d668b892001"
      url: "https://njones.quarto.pub/blog"
```

If you have an existing Quarto Pub site that you want to publish to, you should manually create a `_publish.yml` file that looks like the example above, but with the appropriate `id` and `url` values for your site.

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
quarto publish quarto-pub document.qmd
```

## Managing Sites

If you want to change the “slug” (or URL path) of a published site or remove the site entirely, you can use the site management interface at <https://quartopub.com>, which will display a list of all of your published sites:

![](images/quarto-pub-admin.png)

Click on a site to navigate to an admin page that enables you to change the slug, make the site the default one for your account, or remove the site entirely:

![](images/quarto-pub-admin-site.png)

## User Default Site

In addition to publishing documents and sites to paths within your Quarto Pub sub-domain (e.g. `https://username.quarto.pub/mysite/)` you can also designate one of your sites as the default site that users see when they navigate to your main sub-domain (e.g. `https://username.quarto.pub`). This is an ideal place to publish a blog or personal home page.

To promote one of your sites to the default site, go to your admin page at <https://quartopub.com>, navigate to the site you want to promote, check the **Default Site** option, then **Save** your modified options:

![](images/quarto-pub-default-site.png)

## Multiple Accounts

If you have multiple Quarto Pub accounts it’s important to understand the relationship between the use of accounts in the CLI interface (`quarto publish`) and the use of accounts in your browser (for authenticating and managing sites).

When using `quarto publish`, there are a couple of scenarios where a web browser is launched:

1.  When you need to authorize the Quarto CLI to access your account.
2.  After publishing to open the admin page for your published site.

Before publishing with a Quarto Pub account from the CLI you should always be sure to log in to that account within your default web browser. This ensures that when the CLI launches the browser that it binds to the correct Quarto Pub account.

## Access Tokens

When you publish to Quarto Pub using `quarto publish` an access token is used to grant permission for publishing to your account. If no access token is available for a publish operation then the Quarto CLI will automatically launch a browser to authorize one:

``` markdown
$ quarto publish quarto-pub
? Authorize (Y/n) › 
❯ In order to publish to Quarto Pub you need to
  authorize your account. Please be sure you are
  logged into the correct Quarto Pub account in 
  your default web browser, then press Enter or 
  'Y' to authorize.
```

Authorization will launch your default web browser to confirm that you want to allow publishing from Quarto CLI. An access token will be generated and saved locally by the Quarto CLI. You can list and remove saved accounts using the `quarto publish accounts` command:

``` markdown
$ quarto publish accounts
 ? Manage Publishing Accounts
 ❯ ✔ Quarto Pub: jj@rstudio.com
   ✔ Netlify: jj@rstudio.com
 ❯ Use the arrow keys and spacebar to specify 
   accounts you would like to remove. Press 
   Enter to confirm the list of accounts you
   wish to remain available.
```

You can also view (and revoke) access tokens from the admin interface at <https://quartopub.com>:

![](images/quarto-pub-tokens.png)

Within this interface you’ll see any token you’ve created from the Quarto CLI. You may revoke this token if you no longer wish it to be active. Click the **New Token** button to create additional tokens that can be used for publishing non-interactively (e.g. from a CI service):

![](images/quarto-pub-new-token.png)

Once you have an access token you can use it with `quarto publish` by defining the `QUARTO_PUB_AUTH_TOKEN` environment variable. For example:

``` bash
# token created at https://quartopub.com/profile/
export QUARTO_PUB_AUTH_TOKEN="qpa_k4yWKEmlu5wkvx173Ls"

# publish to quarto-pub site specified within _publish.yml
quarto publish quarto-pub
```

See the article on [Publishing with CI](../../docs/publishing/ci.llms.md) for additional details on non-interactive use of `quarto publish`.

## GitHub Action

Using the `quarto publish quarto-pub` command to publish locally rendered content is the most simple and straightforward way to publish. Another option is to use [GitHub Actions](https://docs.github.com/en/actions) to render and publish your site (you might prefer this if you want execution and/or rendering to be automatically triggered from commits).

There are a few different ways to approach rendering and publishing content. Below, we’ll provide a how-to guide for publishing with GitHub Actions. For more conceptual background on the various approaches, see the discussion on [Rendering for CI](../../docs/publishing/ci.llms.md#rendering-for-ci).

### Publish Record

Prior to attempting to publish with a GitHub Action, you should have completed at least one publish using the [Publish Command](#publish-command) (described immediately above). This publish will create a `_publish.yml` file that records the publishing destination to be used by the GitHub Action. For example:

``` yaml
- source: project
  quarto-pub:
    - id: "5f3abafe-68f9-4c1d-835b-9d668b892001"
      url: "https://njones.quarto.pub/blog"
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
          target: quarto-pub
          QUARTO_PUB_AUTH_TOKEN: ${{ secrets.QUARTO_PUB_AUTH_TOKEN }}
```

### Quarto Pub Credentials

The final step is to configure your GitHub Action with the credentials required for publishing. To do this you need to create a Quarto Pub personal access token and then configure your GitHub action to be able to read it:

1.  If you don’t already have an access token, go to the Quarto Pub [account profile page](https://quartopub.com/profile), and click on **New Token** to create a token. Give this token a memorable name, and copy the token to the clipboard.

2.  Add the Quarto Pub access token to your repository’s action **Secrets** (accessible within repository **Settings**). You will see a **New repository secret** button at the top right:

    ![](images/gh-new-repository-secret.png)

    Click the button and add the personal access token from step 1 as a secret named `QUARTO_PUB_AUTH_TOKEN`:

    ![](images/gh-action-quarto-pub-secret.png)

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

Once you’ve specified your publishing action and Quarto Pub credentials, and pushed your updated repository (including the `_freeze` directory) to GitHub, your action will run with this and subsequent commits, automatically rendering and publishing to Quarto Pub.

### Executing Code

If you prefer, you can also configure a GitHub Action to execute R, Python, or Julia code as part of rendering. While this might reflexively seem like the best approach, consider the following requirements imposed when you execute code within a CI service like GitHub Actions:

- You need to reconstitute all of the dependencies (R, Python, or Julia plus the correct versions of required packages) in the CI environment.

- If your code requires any special permissions (e.g. database or network access) those permissions also need to be present on the CI server.

- Your project may contain documents that can no longer be easily executed (e.g. blog posts from several years ago that use older versions of packages). These documents may need to have `freeze` individually enabled for them to prevent execution on CI.

#### Prerequisites

The best way to ensure that your code can be executed within a GitHub Action is to use a virtual environment like [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment) or [renv](https://rstudio.github.io/renv/articles/renv.llms.md) with your project (below we’ll provide example actions for each). If you aren’t familiar with using these tools check out the article on using [Virtual Environments](../../docs/projects/virtual-environments.llms.md) with Quarto to learn more.

Once you’ve decided to execute code within your GitHub Action you can remove the `freeze: auto` described above from your `_quarto.yml` configuration. Note that if you want to use `freeze` selectively for some documents or directories that is still possible (for a directory, create a `_metadata.yml` file in the directory and specify your freeze configuration there—this is what Quarto does by default for the `posts` folder of blog projects).

#### Example: Jupyter with venv

Here is a complete example of a GitHub Action that installs Python, Jupyter, and package dependencies from `requirements.txt`, then executes code and renders output to Quarto Pub:

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
          target: quarto-pub
          QUARTO_PUB_AUTH_TOKEN: ${{ secrets.QUARTO_PUB_AUTH_TOKEN }}
```

#### Example: Knitr with renv

Here is a complete example of a GitHub Action that installs R and package dependencies from `renv.lock`, then executes code and renders output to Quarto Pub:

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
          target: quarto-pub
          QUARTO_PUB_AUTH_TOKEN: ${{ secrets.QUARTO_PUB_AUTH_TOKEN }}
```

### Additional Options

It’s possible to have a Quarto project in a larger GitHub repository, where the Quarto project does not reside at the top-level directory. In this case, add a `path` input to the invocation of the `publish` action. For example:

``` yaml
- name: Render and Publish
  uses: quarto-dev/quarto-actions/publish@v2
  with:
    target: quarto-pub
    path: subdirectory-to-use
    QUARTO_PUB_AUTH_TOKEN: ${{ secrets.QUARTO_PUB_AUTH_TOKEN }}
```

By default, `quarto publish` will re-render your project before publishing it. However, if you store the rendered output in version control, you don’t need the GitHub action to re-render the project. In that case, add the option `render: false` to the `publish` action:

``` yaml
- name: Render and Publish
  uses: quarto-dev/quarto-actions/publish@v2
  with:
    target: quarto-pub
    render: false
    QUARTO_PUB_AUTH_TOKEN: ${{ secrets.QUARTO_PUB_AUTH_TOKEN }}
```
