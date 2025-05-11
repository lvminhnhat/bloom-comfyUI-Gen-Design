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

pyproject.toml

# pyproject.toml

# [​](http://docs.comfy.org#node-id) Node ID

The node id (“name” field in toml file) uniquely identifies the custom node, and will be used in URLs from the registry. Users can also install the node by referencing the name.

`comfy node install <node-id>`

The node id must be less than 100 characters and can only contain alphanumeric characters, hyphens, underscores, and periods. There should not be consecutive special characters and the id cannot start with a number or special character.

Comparison of node ids is case-insensitive. See the official [python documentation](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#name) for more information.

We recommend using a short name for your node id, and don’t include “ComfyUI” in the name.

# [​](http://docs.comfy.org#version-number) Version Number

The registry uses [semantic versioning](https://semver.org/) which indicates the specific release of a custom node through a three-digit version number X.Y.Z.

X - **MAJOR** change that breaks previous updates

Y - **MINOR** change that adds new features and is backwards compatible

Z - **PATCH** change that fixes a bug

# [​](http://docs.comfy.org#license) License

An optional field that expects a relative path to your license file (usually named `LICENSE` or `LICENSE.txt`).

- `license = { file = "LICENSE" }` ✅
- `license = "LICENSE"` ❌

Alternatively, it can also be referenced by name. Common licenses include [MIT](https://opensource.org/license/mit), [GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), or [Apache](https://www.apache.org/licenses/LICENSE-2.0).

- `license = {text = "MIT License"}` ✅
- `license = "MIT LICENSE"` ❌

Read up more on toml file standards [here](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#license)

# [​](http://docs.comfy.org#publisher-id) Publisher ID

The publisher id uniquely identifies a publisher and is ideally the same as your github username. It is also referred to as the username on the registry and can be found after the `@` symbol on the profile page.

# [​](http://docs.comfy.org#icon) Icon

An optional field that expects a icon URL. It accepts extensions SVG, PNG, JPG or GIF with a maximum resolution of 800px by 400px.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/registry/specifications.mdx)

[Previous](http://docs.comfy.org/registry/cicd)

[Workflow JSONJSON schema for a ComfyUI workflow.  
\
Next](http://docs.comfy.org/specs/workflow_json)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node ID](http://docs.comfy.org#node-id)
- [Version Number](http://docs.comfy.org#version-number)
- [License](http://docs.comfy.org#license)
- [Publisher ID](http://docs.comfy.org#publisher-id)
- [Icon](http://docs.comfy.org#icon)