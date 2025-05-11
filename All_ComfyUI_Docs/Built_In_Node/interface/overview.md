[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Get Started

##### Get Started

- [Introduction](http://docs.comfy.org/get_started/introduction)
- Installation
- [First Image Generation](http://docs.comfy.org/get_started/first_generation)

##### Interface

- [Interface Overview](http://docs.comfy.org/interface/overview)
- [Account Management](http://docs.comfy.org/interface/user)
- [Credits Management](http://docs.comfy.org/interface/credits)
- [Workflow](http://docs.comfy.org/essentials/core-concepts/workflow)
- [Nodes](http://docs.comfy.org/essentials/core-concepts/nodes)
- [Properties](http://docs.comfy.org/essentials/core-concepts/properties)
- [Links](http://docs.comfy.org/essentials/core-concepts/links)
- [Mask Editor](http://docs.comfy.org/interface/maskeditor)
- [Models](http://docs.comfy.org/essentials/core-concepts/models)
- [Dependencies](http://docs.comfy.org/essentials/core-concepts/dependencies)
- [Shortcuts](http://docs.comfy.org/interface/shortcuts)

##### Tutorials

- Basic Examples
- ControlNet
- Flux
- Image
- 3D
- Video
- Audio
- API Nodes

##### Community

- [Contributing](http://docs.comfy.org/community/contributing)

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

ComfyUI Interface Overview

# ComfyUI Interface Overview

In this article, we will briefly introduce the basic user interface of ComfyUI, familiarizing you with the various parts of the ComfyUI interface.

The visual interface is currently the way most users utilize ComfyUI to call the [ComfyUI Server](http://docs.comfy.org/essentials/comfyui-server/comms_overview) to generate corresponding media resources. It provides a visual interface for users to operate and organize workflows, debug workflows, and create amazing works.

Typically, when you start the ComfyUI server, you will see an interface like this:

If you are an earlier user, you may have seen the previous menu interface like this:

Currently, the [ComfyUI frontend](https://github.com/Comfy-Org/ComfyUI_frontend) is a separate project, released and maintained as an independent pip package. If you want to contribute, you can fork this [repository](https://github.com/Comfy-Org/ComfyUI_frontend) and submit a pull request.

## [​](http://docs.comfy.org#localization-support) Localization Support

Currently, ComfyUI supports: English, Chinese, Russian, French, Japanese, and Korean. If you need to switch the interface language to your preferred language, you can click the **Settings gear icon** and then select your desired language under `Comfy` —&gt; `Locale`.

## [​](http://docs.comfy.org#new-menu-interface) New Menu Interface

### [​](http://docs.comfy.org#workspace-areas) Workspace Areas

Below are the main interface areas of ComfyUI and a brief introduction to each part.

Currently, apart from the main workflow interface, the ComfyUI interface is mainly divided into the following parts:

1. Menu Bar: Provides workflow, editing, help menus, workflow execution, ComfyUI Manager entry, etc.
2. Sidebar Panel Switch Buttons: Used to switch between workflow history queue, node library, model library, local user workflow browsing, etc.
3. Theme Switch Button: Quickly switch between ComfyUI’s default dark theme and light theme
4. Settings: Click to open the settings button
5. Canvas Menu: Provides zoom in, zoom out, and auto-fit operations for the ComfyUI canvas

### [​](http://docs.comfy.org#menu-bar-functions) Menu Bar Functions

The image above shows the corresponding functions of the top menu bar, including common features, which we will explain in detail in the specific function usage section.

### [​](http://docs.comfy.org#sidebar-panel-buttons) Sidebar Panel Buttons

In the current ComfyUI, we provide four side panels with the following functions:

1. Workflow History Queue (Queue): All queue information for ComfyUI executing media content generation
2. Node Library: All nodes in ComfyUI, including `Comfy Core` and your installed custom nodes, can be found here
3. Model Library: Models in your local `ComfyUI/models` directory can be found here
4. Local User Workflows (Workflows): Your locally saved workflows can be found here

## [​](http://docs.comfy.org#old-menu-version) Old Menu Version

Currently, ComfyUI enables the new interface by default. If you prefer to use the old interface, you can click the **Settings gear icon** and then set `Use new menu` to `disabled` under `Comfy` —&gt; `Menu` to switch to the old menu version.

The old menu interface only supports English.

The function annotations for the old menu interface are explained below:

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/interface/overview.mdx)

[Previous](http://docs.comfy.org/get_started/first_generation)

[Account ManagementIn this document, we will introduce the account management features of ComfyUI, including account login, registration, and logout operations.  
\
Next](http://docs.comfy.org/interface/user)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Localization Support](http://docs.comfy.org#localization-support)
- [New Menu Interface](http://docs.comfy.org#new-menu-interface)
- [Workspace Areas](http://docs.comfy.org#workspace-areas)
- [Menu Bar Functions](http://docs.comfy.org#menu-bar-functions)
- [Sidebar Panel Buttons](http://docs.comfy.org#sidebar-panel-buttons)
- [Old Menu Version](http://docs.comfy.org#old-menu-version)