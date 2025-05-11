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

Overview

# Overview

Custom nodes allow you to implement new features and share them with the wider community.

A custom node is like any Comfy node: it takes input, does something to it, and produces an output. While some custom nodes perform highly complex tasks, many just do one thing. Here’s an example of a simple node that takes an image and inverts it.

## [​](http://docs.comfy.org#client-server-model) Client-Server Model

Comfy runs in a client-server model. The server, written in Python, handles all the real work: data-processing, models, image diffusion etc. The client, written in Javascript, handles the user interface.

Comfy can also be used in API mode, in which a workflow is sent to the server by a non-Comfy client (such as another UI, or a command line script).

Custom nodes can be placed into one of four categories:

### [​](http://docs.comfy.org#server-side-only) Server side only

The majority of Custom Nodes run purely on the server side, by defining a Python class that specifies the input and output types, and provides a function that can be called to process inputs and produce an output.

### [​](http://docs.comfy.org#client-side-only) Client side only

A few Custom Nodes provide a modification to the client UI, but do not add core functionality. Despite the name, they may not even add new nodes to the system.

### [​](http://docs.comfy.org#independent-client-and-server) Independent Client and Server

Custom nodes may provide additional server features, and additional (related) UI features (such as a new widget to deal with a new data type). In most cases, communication between the client and server can be handled by the Comfy data flow control.

### [​](http://docs.comfy.org#connected-client-and-server) Connected Client and Server

In a small number of cases, the UI features and the server need to interact with each other directly.

Any node that requires Client-Server communication will not be compatible with use through the API.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/overview.mdx)

[Previous](http://docs.comfy.org/comfy-cli/reference)

[Getting Started  
\
Next](http://docs.comfy.org/custom-nodes/walkthrough)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Client-Server Model](http://docs.comfy.org#client-server-model)
- [Server side only](http://docs.comfy.org#server-side-only)
- [Client side only](http://docs.comfy.org#client-side-only)
- [Independent Client and Server](http://docs.comfy.org#independent-client-and-server)
- [Connected Client and Server](http://docs.comfy.org#connected-client-and-server)