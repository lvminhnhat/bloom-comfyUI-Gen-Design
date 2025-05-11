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

Workflow templates

# Workflow templates

If you have example workflow files associated with your custom nodes then ComfyUI can show these to the user in the template browser (`Workflow`/`Browse Templates` menu). Workflow templates are a great way to support people getting started with your nodes.

All you have to do as a node developer is to create an `example_workflows` folder and place the `json` files there. Optionally you can place `jpg` files with the same name to be shown as the template thumbnail.

Under the hood ComfyUI statically serves these files along with an endpoint (`/api/workflow_templates`) that returns the collection of workflow templates.

## [​](http://docs.comfy.org#example) Example

Under `ComfyUI-MyCustomNodeModule/example_workflows/` directory:

- `My_example_workflow_1.json`
- `My_example_workflow_1.jpg`
- `My_example_workflow_2.json`

In this example ComfyUI’s template browser shows a category called `ComfyUI-MyCustomNodeModule` with two items, one of which has a thumbnail.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/workflow_templates.mdx)

[Previous](http://docs.comfy.org/custom-nodes/js/javascript_examples)

[Tips  
\
Next](http://docs.comfy.org/custom-nodes/tips)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Example](http://docs.comfy.org#example)