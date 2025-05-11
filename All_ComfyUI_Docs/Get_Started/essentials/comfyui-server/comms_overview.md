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

Server Overview

# Server Overview

## [​](http://docs.comfy.org#overview) Overview

The Comfy server runs on top of the [aiohttp framework](https://docs.aiohttp.org/), which in turn uses [asyncio](https://pypi.org/project/asyncio/).

Messages from the server to the client are sent by socket messages through the `send_sync` method of the server, which is an instance of `PromptServer` (defined in `server.py`). They are processed by a socket event listener registered in `api.js`. See [messages](http://docs.comfy.org/comms_messages).

Messages from the client to the server are sent by the `api.fetchApi()` method defined in `api.js`, and are handled by http routes defined by the server. See [routes](http://docs.comfy.org/comms_routes).

The client submits the whole workflow (widget values and all) when you queue a request. The server does not receive any changes you make after you send a request to the queue. If you want to modify server behavior during execution, you’ll need routes.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/comfyui-server/comms_overview.mdx)

[Messages  
\
Next](http://docs.comfy.org/essentials/comfyui-server/comms_messages)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Overview](http://docs.comfy.org#overview)