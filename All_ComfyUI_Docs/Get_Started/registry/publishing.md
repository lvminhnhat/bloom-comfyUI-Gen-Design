[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Development

##### ComfyUI Server

- [Server Overview](http://docs.comfy.org/essentials/comfyui-server/comms_overview)
- [Messages](http://docs.comfy.org/essentials/comfyui-server/comms_messages)
- [Execution Model Inversion Guide](http://docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide)

##### CLI

- [Getting Started](http://docs.comfy.org/comfy-cli/getting-started)
- [Reference](http://docs.comfy.org/comfy-cli/reference)

##### Develop Custom Nodes

- [Overview](http://docs.comfy.org/custom-nodes/overview)
- [Getting Started](http://docs.comfy.org/custom-nodes/walkthrough)
- Backend
- UI
- [Workflow templates](http://docs.comfy.org/custom-nodes/workflow_templates)
- [Tips](http://docs.comfy.org/custom-nodes/tips)

##### Registry

- [Overview](http://docs.comfy.org/registry/overview)
- [Publishing Nodes](http://docs.comfy.org/registry/publishing)
- [Standards](http://docs.comfy.org/registry/standards)
- [Custom Node CI/CD](http://docs.comfy.org/registry/cicd)
- [pyproject.toml](http://docs.comfy.org/registry/specifications)
- [](http://docs.comfy.org/)

##### Specifications

- Workflow JSON
- Node Definitions

<!--THE END-->

- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)
  
  ![US](https://purecatamphetamine.github.io/country-flag-icons/1x1/US.svg)
  
  English

[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

![US](https://purecatamphetamine.github.io/country-flag-icons/1x1/US.svg)

English

Search or ask...

- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)

Search...

Navigation

Publishing Nodes

# Publishing Nodes

## [​](http://docs.comfy.org#set-up-a-registry-account) Set up a Registry Account

Follow the steps below to set up a registry account and publish your first node.

### [​](http://docs.comfy.org#watch-a-tutorial) Watch a Tutorial

### [​](http://docs.comfy.org#create-a-publisher) Create a Publisher

A publisher is an identity that can publish custom nodes to the registry. Every custom node needs to include a publisher identifier in the pyproject.toml [file](http://docs.comfy.org).

Go to [Comfy Registry](https://registry.comfy.org), and create a publisher account. Your publisher id is globally unique, and cannot be changed later because it is used in the URL of your custom node.

Your publisher id is found after the `@` symbol on your profile page.

### [​](http://docs.comfy.org#create-an-api-key-for-publishing) Create an API Key for publishing

Go [here](https://registry.comfy.org/nodes) and click on the publisher you want to create an API key for. This will be used to publish a custom node via the CLI.

Name the API key and save it somewhere safe. If you lose it, you’ll have to create a new key.

### [​](http://docs.comfy.org#add-metadata) Add Metadata

Have you installed the comfy-cli? [Do that first](http://docs.comfy.org/comfy-cli/getting-started).

```bash
comfy node init
```

This command will generate the following metadata:

```toml
# pyproject.toml
[project]
name = "" # Unique identifier for your node. Immutable after creation.
description = ""
version = "1.0.0" # Custom Node version. Must be semantically versioned.
license = { file = "LICENSE.txt" }
dependencies  = [] # Filled in from requirements.txt

[project.urls]
Repository = "https://github.com/..."

[tool.comfy]
PublisherId = "" # TODO (fill in Publisher ID from Comfy Registry Website).
DisplayName = "" # Display name for the Custom Node. Can be changed later.
Icon = "https://example.com/icon.png" # SVG, PNG, JPG or GIF (MAX. 800x400px)
```

Add this file to your repository. Check the [specifications](http://docs.comfy.org/registry/specifications) for more information on the pyproject.toml file.

## [​](http://docs.comfy.org#publish-to-the-registry) Publish to the Registry

### [​](http://docs.comfy.org#option-1%3A-comfy-cli) Option 1: Comfy CLI

Run the command below to manually publish your node to the registry.

```bash
comfy node publish
```

You’ll be prompted for the API key.

```bash
API Key for publisher '<publisher id>': ****************************************************

...Version 1.0.0 Published. 
See it here: https://registry.comfy.org/publisherId/your-node
```

Keep in mind that the API key is hidden by default.

When copy-pasting, your API key might have an additional \\x16 at the back when using CTRL+V (for Windows), eg: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\x16.

It is recommended to copy-paste your API key via right-clicking instead.

### [​](http://docs.comfy.org#option-2%3A-github-actions) Option 2: Github Actions

Automatically publish your node through github actions.

1

Set up a Github Secret

Go to Settings -&gt; Secrets and Variables -&gt; Actions -&gt; Under Secrets Tab and Repository secrets -&gt; New Repository Secret.

Create a secret called `REGISTRY_ACCESS_TOKEN` and store your API key as the value.

2

Create a Github Action

Copy the code below and paste it here `/.github/workflows/publish_action.yml`

```bash
name: Publish to Comfy registry
on:
  workflow_dispatch:
  push:
    branches:
      - main
    paths:
      - "pyproject.toml"

jobs:
  publish-node:
    name: Publish Custom Node to registry
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v4
      - name: Publish Custom Node
        uses: Comfy-Org/publish-node-action@main
        with:
          personal_access_token: ${{ secrets.REGISTRY_ACCESS_TOKEN }} ## Add your own personal access token to your Github Repository secrets and reference it here.
```

If your working branch is named something besides `main`, such as `master`, add the name under the branches section.

3

Test the Github Action

Push an update to your `pyproject.toml`’s version number. You should see your updated node on the registry.

The github action will automatically run every time you push an update to your `pyproject.toml` file

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/registry/publishing.mdx)

[Previous](http://docs.comfy.org/registry/overview)

[StandardsSecurity and other standards for publishing to the Registry  
\
Next](http://docs.comfy.org/registry/standards)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Set up a Registry Account](http://docs.comfy.org#set-up-a-registry-account)
- [Watch a Tutorial](http://docs.comfy.org#watch-a-tutorial)
- [Create a Publisher](http://docs.comfy.org#create-a-publisher)
- [Create an API Key for publishing](http://docs.comfy.org#create-an-api-key-for-publishing)
- [Add Metadata](http://docs.comfy.org#add-metadata)
- [Publish to the Registry](http://docs.comfy.org#publish-to-the-registry)
- [Option 1: Comfy CLI](http://docs.comfy.org#option-1%3A-comfy-cli)
- [Option 2: Github Actions](http://docs.comfy.org#option-2%3A-github-actions)