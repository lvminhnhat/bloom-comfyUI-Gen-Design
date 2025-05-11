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
  
  - [Javascript Extensions](http://docs.comfy.org/custom-nodes/js/javascript_overview)
  - [Comfy Hooks](http://docs.comfy.org/custom-nodes/js/javascript_hooks)
  - [Comfy Objects](http://docs.comfy.org/custom-nodes/js/javascript_objects_and_hijacking)
  - [Settings](http://docs.comfy.org/custom-nodes/js/javascript_settings)
  - [Annotated Examples](http://docs.comfy.org/custom-nodes/js/javascript_examples)
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

Javascript Extensions

# Javascript Extensions

## [​](http://docs.comfy.org#extending-the-comfy-client) Extending the Comfy Client

Comfy can be modified through an extensions mechanism. To add an extension you need to:

- Export `WEB_DIRECTORY` from your Python module,
- Place one or more `.js` files into that directory,
- Use `app.registerExtension` to register your extension.

These three steps are below. Once you know how to add an extension, look through the [hooks](http://docs.comfy.org/javascript_hooks) available to get your code called, a description of various [Comfy objects](http://docs.comfy.org/javascript_objects_and_hijacking) you might need, or jump straight to some [example code snippets](http://docs.comfy.org/javascript_examples).

### [​](http://docs.comfy.org#exporting-web-directory) Exporting `WEB_DIRECTORY`

The Comfy web client can be extended by creating a subdirectory in your custom node directory, conventionally called `js`, and exporting `WEB_DIRECTORY` - so your `__init_.py` will include something like:

```python
WEB_DIRECTORY = "./js"
__all__ = ["NODE_CLASS_MAPPINGS", "NODE_DISPLAY_NAME_MAPPINGS", "WEB_DIRECTORY"]
```

### [​](http://docs.comfy.org#including-js-files) Including `.js` files

All Javascript `.js` files will be loaded by the browser as the Comfy webpage loads. You don’t need to specify the file your extension is in.

*Only* `.js` files will be added to the webpage. Other resources (such as `.css` files) can be accessed at `extensions/custom_node_subfolder/the_file.css` and added programmatically.

That path does *not* include the name of the subfolder. The value of `WEB_DIRECTORY` is inserted by the server.

### [​](http://docs.comfy.org#registering-an-extension) Registering an extension

The basic structure of an extension follows is to import the main Comfy `app` object, and call `app.registerExtension`, passing a dictionary that contains a unique `name`, and one or more functions to be called by hooks in the Comfy code.

A complete, trivial, and annoying, extension might look like this:

```javascript
import { app } from "../../scripts/app.js";
app.registerExtension({ 
	name: "a.unique.name.for.a.useless.extension",
	async setup() { 
		alert("Setup complete!")
	},
})
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/js/javascript_overview.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/tensors)

[Comfy Hooks  
\
Next](http://docs.comfy.org/custom-nodes/js/javascript_hooks)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Extending the Comfy Client](http://docs.comfy.org#extending-the-comfy-client)
- [Exporting WEB\_DIRECTORY](http://docs.comfy.org#exporting-web-directory)
- [Including .js files](http://docs.comfy.org#including-js-files)
- [Registering an extension](http://docs.comfy.org#registering-an-extension)