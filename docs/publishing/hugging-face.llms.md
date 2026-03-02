# Hugging Face Spaces

## Overview

Hugging Face is a comprehensive platform that offers a wide array of machine learning models, particularly in natural language processing (NLP) and computer vision. It is designed to facilitate the training, deployment, and use of open-access machine learning models, making it easier for developers and researchers to access state-of-the-art models.

Hugging Face also provides application and static site hosting as part of its [Spaces project](https://huggingface.co/docs/hub/spaces-overview). You can use [Hugging Face Spaces](https://huggingface.co/spaces) to render and host Quarto websites as a way to document and present your work.

Quarto’s integration in Hugging Face Spaces happens through a [Docker](https://www.docker.com/) image created by the Quarto team that Hugging Face has made easily available for authors as a template.

To create and publish a Hugging Face Space using Quarto, you’ll start by creating a new space using Quarto’s Docker Template. Then you’ll edit or replace the example content with your own. Learn more about this process in [Getting Started](#getting-started) below.

Whenever changes are committed to your Hugging Face Space, a new build is initiated which renders and serves your Quarto website. You can make and commit changes directly in the Hugging Face UI. However, previewing your changes via a build on Hugging Face is time-consuming, so for faster iteration we recommend working locally and using the `quarto publish huggingface` command. This workflow is described below in [Publish Command](#publish-command).

## Getting Started

### Create a New Space

To get started you’ll create a new Hugging Face Space using the Quarto template.

Visit [the Hugging Face Create a New Space webpage](https://huggingface.co/new-space?template=posit%2Fquarto-template).

If you’re not logged in to Hugging Face, log in first:

![Screenshot of UI for logging in to Hugging Face.](./images/hugging-face-login-ui.png)

The UI for logging in to Hugging Face

Start by choosing a name and license for your space:

![Screenshot of Hugging Face UI for space creation consisting of three text boxes labelled: Owner, Space name and License.](./images/hugging-face-choose-name-ui.png)

The UI for choosing name and license for your space

If you followed the link above, you will see “Docker” selected for the Space SDK, and “Quarto” chosen as the Docker template. If not, select them as shown below:

![Screenshot of Hugging Face UI for selecting the space SDK and template. The Docker SDK and Quarto template are highlighted.](./images/hugging-face-create-ui.png)

The UI for Hugging Face Spaces creation webpage

Finally, choose the hardware that will be used to run your space, whether the space will be public or private, and click on “Create Space”:

![Screenshot of Hugging Face UI showing: a dropdown labelled 'Space Hardware', two radio buttons labelled Public (selected) and Private, and a button labelled 'Create Space'.](./images/hugging-face-hardware-ui.png)

The UI for choosing hardware configuration and space visibility

Hugging Face will then “Build” your space:

> **WARNING:**
>
> It can take a couple of minutes for the Space to deploy to Hugging Face after the Docker build process completes. To see your changes you will need to do two things:
>
> 1.  Wait for your space’s status to go from ‘Building’ to ‘Running’(this is visible in the status bar above the Space)
>
> 2.  Force-reload the web page by holding Shift and hitting the reload button in your browser.

![Screenshot of the Build log in a Hugging Face Space. Log starts with and ends with](images/hugging-face-build.png)

Build process for a new space based on the Quarto template

You’ll know the space is finished building when you see the `Running` in the top bar.

![](images/hugging-face-running-button.png)

Hugging Face `Running` badge

Once built, your Space will display the rendered example website (you may need to refresh the page in your browser for this to appear):

![Screenshot of a Hugging Face Space, displaying a website with the title ''.](images/hugging-face-complete.png)

A Quarto template website running in a Hugging Face Space

### Quarto’s Hugging Face Template

You can click on the `Files` tab in the top right to look at the files which make up the template. Quarto’s Hugging Face template consists of files used to create an environment to build and render the Quarto website (`Dockerfile`and `requirements.txt`), and the website source itself in `src/`:

- `Dockerfile`: This contains the system setup to build and serve the Quarto site on Hugging Face. You probably won’t need to change this file unless you need to add additional system dependencies or modify the Quarto version.

- `requirements.txt`: This is where you should include any Python dependencies which you need for your website. These are installed when the Dockerfile builds.

- The `src` directory contains the source files for the Quarto website. You can include Jupyter notebooks or markdown (`.qmd` or `.md`) files.

- `src/_quarto.yml` defines the navigation for your website. If you want to add new pages or reorganize the existing ones, you’ll need to change this file.

You can edit these files directly in the Hugging Face UI but we reccommend cloning your space, and making and previewing changes locally, then using the publish command as described in the next section.

## Publish Command

The `quarto publish huggingface` command facilitates a workflow where you [make and preview edits](#edit-and-preview) locally before [publishing](#publish) to your Hugging Face space. Before using the command you’ll need to complete some [Setup](#setup).

### Setup

To get set up to use `quarto publish huggingface` you should have already:

1.  [Created a space using Quarto’s Docker Template](#create-a-new-space) as described above.

Then complete the following steps, explained at length below:

2.  (Optional) [Create an authorization token if you lack one](#create-an-authorization-token)

3.  [Clone the repository locally](#clone-the-repository-locally)

#### Create an authorization token

In order to publish the results to Hugging Face, `quarto publish` needs access to your credentials. If you haven’t created such an authorization token yet, visit [Hugging Face’s documentation on user access tokens](https://huggingface.co/docs/hub/security-tokens#how-to-manage-user-access-tokens) and follow the instructions to create a token with the `write` role. You’ll need this token the first time you run the publish command.

#### Clone the repository locally

The URL for your space, as well as the URL to clone the repository, is `https://huggingface.co/spaces/<your-hugging-face-username>/<name-of-space>`. Use your favorite `git` interface to clone the Hugging Face Space you’ve just created with the URL above. You can also find instructions in your space under **⋮** \> **Clone repository**.

### Edit and Preview

Once your repository is set up, use whichever text editor you prefer to make changes to your repository. Quarto’s Hugging Face template includes a Quarto website in the `src/` directory of the repository. For information on how to create websites with Quarto, see [our documentation](../../docs/websites/index.llms.md)

To preview your changes, from the root of your repository, run:

``` bash
quarto preview src
```

### Publish

When you are happy with the results in the repository, run:

``` bash
quarto publish huggingface
```

Quarto will stage, commit, and push all required changes to Hugging Face, as well as fetching remote content and merging it with your repository’s contents first. If the repository you’re working on hasn’t been configured to take in an explicit user name and authorization token, Quarto will prompt you for such information on the command line.

On completion Quarto will open your space in your default browser.

## Publishing an Existing Repository

The command `quarto publish huggingface` requires that the `origin` [git remote](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories) point to a `https://huggingface.co/spaces` URL. If you used the instructions above, this will happen automatically.

If you are working from an existing repository already configured with a Quarto template pointing to the right URL, you can use `quarto publish huggingface` directly without needing to create or clone a new space.
