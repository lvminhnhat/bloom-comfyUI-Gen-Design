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

Standards

# Standards

Security and other standards for publishing to the Registry

## [​](http://docs.comfy.org#base-standards) Base Standards

### [​](http://docs.comfy.org#1-community-value) 1. Community Value

Custom nodes must provide valuable functionality to the ComfyUI community

Avoid:

- Excessive self-promotion
- Impersonation or misleading behavior
- Malicious behavior
- Self-promotion is permitted only within your designated settings menu section
- Top and side menus should contain only useful functionality

### [​](http://docs.comfy.org#2-node-compatibility) 2. Node Compatibility

Do not interfere with other custom nodes’ operations (installation, updates, removal)

- For dependencies on other custom nodes:
  
  - Display clear warnings when dependent functionality is used
  - Provide example workflows demonstrating required nodes

### [​](http://docs.comfy.org#3-legal-compliance) 3. Legal Compliance

Must comply with all applicable laws and regulations

### [​](http://docs.comfy.org#5-quality-requirements) 5. Quality Requirements

Nodes must be fully functional, well documented, and actively maintained.

### [​](http://docs.comfy.org#6-fork-guidelines) 6. Fork Guidelines

Forked nodes must:

- Have clearly distinct names from original
- Provide significant differences in functionality or code

Below are standards that must be met to publish custom nodes to the registry.

## [​](http://docs.comfy.org#security-standards) Security Standards

Custom nodes should be secure. We will start working with custom nodes that violate these standards to be rewritten. If there is some major functionality that should be exposed by core, please request it in the [rfcs repo](https://github.com/comfy-org/rfcs).

### [​](http://docs.comfy.org#eval%2Fexec-calls) eval/exec Calls

#### [​](http://docs.comfy.org#policy) Policy

The use of `eval` and `exec` functions is prohibited in custom nodes due to security concerns.

#### [​](http://docs.comfy.org#reasoning) Reasoning

These functions can enable arbitrary code execution, creating potential Remote Code Execution (RCE) vulnerabilities when processing user inputs. Workflows containing nodes that pass user inputs into `eval` or `exec` could be exploited for various cyberattacks, including:

- Keylogging
- Ransomware
- Other malicious code execution

### [​](http://docs.comfy.org#subprocess-for-pip-install) subprocess for pip install

#### [​](http://docs.comfy.org#policy-2) Policy

Runtime package installation through subprocess calls is not permitted.

#### [​](http://docs.comfy.org#reasoning-2) Reasoning

- First item ComfyUI manager will ship with ComfyUI and lets the user install dependencies
- Centralized dependency management improves security and user experience
- Helps prevent potential supply chain attacks
- Eliminates need for multiple ComfyUI reloads

### [​](http://docs.comfy.org#code-obfuscation) Code Obfuscation

#### [​](http://docs.comfy.org#policy-3) Policy

Code obfuscation is prohibited in custom nodes.

#### [​](http://docs.comfy.org#reasoning-3) Reasoning

Obfuscated code:

- Impossible to review and likely to be malicious

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/registry/standards.mdx)

[Previous](http://docs.comfy.org/registry/publishing)

[Custom Node CI/CD  
\
Next](http://docs.comfy.org/registry/cicd)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Base Standards](http://docs.comfy.org#base-standards)
- [1. Community Value](http://docs.comfy.org#1-community-value)
- [2. Node Compatibility](http://docs.comfy.org#2-node-compatibility)
- [3. Legal Compliance](http://docs.comfy.org#3-legal-compliance)
- [5. Quality Requirements](http://docs.comfy.org#5-quality-requirements)
- [6. Fork Guidelines](http://docs.comfy.org#6-fork-guidelines)
- [Security Standards](http://docs.comfy.org#security-standards)
- [eval/exec Calls](http://docs.comfy.org#eval%2Fexec-calls)
- [Policy](http://docs.comfy.org#policy)
- [Reasoning](http://docs.comfy.org#reasoning)
- [subprocess for pip install](http://docs.comfy.org#subprocess-for-pip-install)
- [Policy](http://docs.comfy.org#policy-2)
- [Reasoning](http://docs.comfy.org#reasoning-2)
- [Code Obfuscation](http://docs.comfy.org#code-obfuscation)
- [Policy](http://docs.comfy.org#policy-3)
- [Reasoning](http://docs.comfy.org#reasoning-3)