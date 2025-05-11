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

Lifecycle

# Lifecycle

## [​](http://docs.comfy.org#how-comfy-loads-custom-nodes) How Comfy loads custom nodes

When Comfy starts, it scans the directory `custom_nodes` for Python modules, and attempts to load them. If the module exports `NODE_CLASS_MAPPINGS`, it will be treated as a custom node.

A python module is a directory containing an `__init__.py` file. The module exports whatever is listed in the `__all__` attribute defined in `__init__.py`.

### [​](http://docs.comfy.org#init-py) **init**.py

`__init__.py` is executed when Comfy attempts to import the module. For a module to be recognized as containing custom node definitions, it needs to export `NODE_CLASS_MAPPINGS`. If it does (and if nothing goes wrong in the import), the nodes defined in the module will be available in Comfy. If there is an error in your code, Comfy will continue, but will report the module as having failed to load. So check the Python console!

A very simple `__init__.py` file would look like this:

```python
from .python_file import MyCustomNode
NODE_CLASS_MAPPINGS = { "My Custom Node" : MyCustomNode }
__all__ = ["NODE_CLASS_MAPPINGS"]
```

#### [​](http://docs.comfy.org#node-class-mappings) NODE\_CLASS\_MAPPINGS

`NODE_CLASS_MAPPINGS` must be a `dict` mapping custom node names (unique across the Comfy install) to the corresponding node class.

#### [​](http://docs.comfy.org#node-display-name-mappings) NODE\_DISPLAY\_NAME\_MAPPINGS

`__init__.py` may also export `NODE_DISPLAY_NAME_MAPPINGS`, which maps the same unique name to a display name for the node. If `NODE_DISPLAY_NAME_MAPPINGS` is not provided, Comfy will use the unique name as the display name.

#### [​](http://docs.comfy.org#web-directory) WEB\_DIRECTORY

If you are deploying client side code, you will also need to export the path, relative to the module, in which the JavaScript files are to be found. It is conventional to place these in a subdirectory of your custom node named `js`.

*Only* `.js` files will be served; you can’t deploy `.css` or other types in this way

In previous versions of Comfy, `__init__.py` was required to copy the JavaScript files into the main Comfy web subdirectory. You will still see code that does this. Don’t.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/lifecycle.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/server_overview)

[Publishing to the Manager  
\
Next](http://docs.comfy.org/custom-nodes/backend/manager)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [How Comfy loads custom nodes](http://docs.comfy.org#how-comfy-loads-custom-nodes)
- [init.py](http://docs.comfy.org#init-py)
- [NODE\_CLASS\_MAPPINGS](http://docs.comfy.org#node-class-mappings)
- [NODE\_DISPLAY\_NAME\_MAPPINGS](http://docs.comfy.org#node-display-name-mappings)
- [WEB\_DIRECTORY](http://docs.comfy.org#web-directory)