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
  
  - [Properties](http://docs.comfy.org/custom-nodes/backend/server_overview)
  - [Lifecycle](http://docs.comfy.org/custom-nodes/backend/lifecycle)
  - [Publishing to the Manager](http://docs.comfy.org/custom-nodes/backend/manager)
  - [Datatypes](http://docs.comfy.org/custom-nodes/backend/datatypes)
  - [Images, Latents, and Masks](http://docs.comfy.org/custom-nodes/backend/images_and_masks)
  - [Hidden and Flexible inputs](http://docs.comfy.org/custom-nodes/backend/more_on_inputs)
  - [Lazy Evaluation](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation)
  - [Node Expansion](http://docs.comfy.org/custom-nodes/backend/expansion)
  - [Data lists](http://docs.comfy.org/custom-nodes/backend/lists)
  - [Annotated Examples](http://docs.comfy.org/custom-nodes/backend/snippets)
  - [Working with torch.Tensor](http://docs.comfy.org/custom-nodes/backend/tensors)
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

Publishing to the Manager

# Publishing to the Manager

### [​](http://docs.comfy.org#using-comfyui-manager) Using ComfyUI Manager

To make your custom node available through **ComfyUI Manager** you need to save it as a git repository (generally at `github.com`) and then submit a Pull Request on the **ComfyUI Manager** git, in which you have edited `custom-node-list.json` to add your node. [More details](https://github.com/ltdrdata/ComfyUI-Manager?tab=readme-ov-file#how-to-register-your-custom-node-into-comfyui-manager).

When a user installs the node, **ComfyUI Manager** will:

1

Git Clone

git clone the repository,

2

Install Python Dependencies

install the pip dependencies listed in the custom node repository under `requirements.txt` (if present),

```plaintext
pip install -r requirements.txt
```

As is always the case with `pip`, it is possible that your node requirements will be in conflict with other custom nodes. Don’t make your `requirements.txt` any more restrictive than they need to be.

3

Run Install Script

execute `install.py`, if it is present in the custom node repository.

`install.py` is executed from the root path of the custom node

### [​](http://docs.comfy.org#comfyui-manager-files) ComfyUI Manager files

As indicated above, there are a number of files and scripts that **ComfyUI Manager** will use to manage the lifecycle of a custom node. These are all optional.

- `requirements.txt` - Python dependencies as mentioned above
- `install.py`, `uninstall.py` - executed when the custom node is installed or uninstalled
  
  Users can just delete the directory, so you can’t rely on `uninstall.py` being run
- `disable.py`, `enable.py` - executed when a custom node is disabled or re-enabled
  
  `enable.py` is only run when a disabled node is re-enabled - it should just reverse anything done in `disable.py`
  
  Disabled custom node subdirectory have `.disabled` appended to their names, and Comfy ignores these modules
- `node_list.json` - only required if the custom nodes pattern of NODE\_CLASS\_MAPPINGS is not conventional.

See the [ComfyUI Manager guide](https://github.com/ltdrdata/ComfyUI-Manager?tab=readme-ov-file#custom-node-support-guide) for official details.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/manager.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/lifecycle)

[Datatypes  
\
Next](http://docs.comfy.org/custom-nodes/backend/datatypes)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Using ComfyUI Manager](http://docs.comfy.org#using-comfyui-manager)
- [ComfyUI Manager files](http://docs.comfy.org#comfyui-manager-files)