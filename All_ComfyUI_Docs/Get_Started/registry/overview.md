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

## [​](http://docs.comfy.org#introduction) Introduction

The Registry is a public collection of custom nodes. Developers can publish, version, deprecate, and track metrics related to their custom nodes. ComfyUI users can discover, install, and rate custom nodes from the registry.

## [​](http://docs.comfy.org#why-use-the-registry%3F) Why use the Registry?

The Comfy Registry helps the community by standardizing the development of custom nodes:

  **Node Versioning:** Developers frequently publish new versions of their custom nodes which often break workflows that rely on them. With registry nodes being [semantically versioned](https://semver.org/), users can now choose to safely upgrade, deprecate, or lock their node versions in place, knowing in advance how their actions will impact their workflows. The workflow JSON will store the version of the node used, so you can always reliably reproduce your workflows.

  **Node Security:** The registry will serve as a backend for the [ComfyUI-manager](https://github.com/ltdrdata/ComfyUI-Manager). All nodes will be scanned for malicious behaviour such as custom pip wheels, arbitrary system calls, etc. Nodes that pass these checks will have a verification flag () beside their name on the UI-manager. For a list of security standards, see the [standards](http://docs.comfy.org/registry/standards).

  **Search:** Search across all nodes on the Registry to find existing nodes for your workflow.x

## [​](http://docs.comfy.org#publishing-nodes) Publishing Nodes

Get started publishing your first node by following the [tutorial](http://docs.comfy.org/registry/publishing).

## [​](http://docs.comfy.org#frequently-asked-questions) Frequently Asked Questions

Do registry nodes have unique identifiers?

Yes, a custom node on the Registry has a globally unique name and this allows Comfy Workflow JSON files to uniquely identify any custom node without collisions.

Are there any restrictions on what I can publish?

Check the [standards](http://docs.comfy.org/registry/standards) for more information.

How do you ensure node stability?

Once a custom node version is published, it cannot be changed. This ensures that users can rely on the stability of the custom node over time.

How are nodes versioned?

Custom nodes are versioned using [semantic versioning](https://semver.org/). This allows users to understand the impact of upgrading to a new version.

How do I deprecate a node version?

You can deprecate a version in the Comfy Registry website by clicking **More Actions &gt; Deprecate**. Users who installed this version will be shown the deprecation message and be encouraged to upgrade to a newer version.

Deprecating versions is useful when an issue is discovered after publishing.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/registry/overview.mdx)

[Previous](http://docs.comfy.org/custom-nodes/tips)

[Publishing Nodes  
\
Next](http://docs.comfy.org/registry/publishing)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Introduction](http://docs.comfy.org#introduction)
- [Why use the Registry?](http://docs.comfy.org#why-use-the-registry%3F)
- [Publishing Nodes](http://docs.comfy.org#publishing-nodes)
- [Frequently Asked Questions](http://docs.comfy.org#frequently-asked-questions)