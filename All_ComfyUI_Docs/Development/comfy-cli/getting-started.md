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

Getting Started

# Getting Started

### [​](http://docs.comfy.org#overview) Overview

`comfy-cli` is a [command line tool](https://github.com/Comfy-Org/comfy-cli) that makes it easier to install and manage Comfy.

### [​](http://docs.comfy.org#install-cli) Install CLI

pip

homebrew

```bash
pip install comfy-cli
```

To get shell completion hints:

```bash
comfy --install-completion
```

### [​](http://docs.comfy.org#install-comfyui) Install ComfyUI

Create a virtual environment with any Python version greater than 3.9.

conda

venv

```bash
conda create -n comfy-env python=3.11
conda activate comfy-env
```

Install ComfyUI

```bash
comfy install
```

You still need to install CUDA, or ROCm depending on your GPU.

### [​](http://docs.comfy.org#run-comfyui) Run ComfyUI

```bash
comfy launch
```

### [​](http://docs.comfy.org#manage-custom-nodes) Manage Custom Nodes

```bash
comfy node install <NODE_NAME>
```

We use `cm-cli` for installing custom nodes. See the [docs](https://github.com/ltdrdata/ComfyUI-Manager/blob/main/docs/en/cm-cli.md) for more information.

### [​](http://docs.comfy.org#manage-models) Manage Models

Downloading models with `comfy-cli` is easy. Just run:

```bash
comfy model download <url> models/checkpoints
```

### [​](http://docs.comfy.org#contributing) Contributing

We encourage contributions to comfy-cli! If you have suggestions, ideas, or bug reports, please open an issue on our [GitHub repository](https://github.com/Comfy-Org/comfy-cli/issues). If you want to contribute code, fork the repository and submit a pull request.

Refer to the [Dev Guide](https://github.com/Comfy-Org/comfy-cli/blob/main/DEV_README.md) for further details.

### [​](http://docs.comfy.org#analytics) Analytics

We track usage of the CLI to improve the user experience. You can disable this by running:

```bash
comfy tracking disable
```

To re-enable tracking, run:

```bash
comfy tracking enable
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/comfy-cli/getting-started.mdx)

[Previous](http://docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide)

[Reference  
\
Next](http://docs.comfy.org/comfy-cli/reference)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Overview](http://docs.comfy.org#overview)
- [Install CLI](http://docs.comfy.org#install-cli)
- [Install ComfyUI](http://docs.comfy.org#install-comfyui)
- [Run ComfyUI](http://docs.comfy.org#run-comfyui)
- [Manage Custom Nodes](http://docs.comfy.org#manage-custom-nodes)
- [Manage Models](http://docs.comfy.org#manage-models)
- [Contributing](http://docs.comfy.org#contributing)
- [Analytics](http://docs.comfy.org#analytics)