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
  
  - [Text to Image](http://docs.comfy.org/tutorials/basic/text-to-image)
  - [Image to Image](http://docs.comfy.org/tutorials/basic/image-to-image)
  - [Inpaint](http://docs.comfy.org/tutorials/basic/inpaint)
  - [Outpaint](http://docs.comfy.org/tutorials/basic/outpaint)
  - [Upscale](http://docs.comfy.org/tutorials/basic/upscale)
  - [LoRA](http://docs.comfy.org/tutorials/basic/lora)
  - [Multiple LoRAs](http://docs.comfy.org/tutorials/basic/multiple-loras)
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

ComfyUI Multiple LoRAs Example

# ComfyUI Multiple LoRAs Example

This guide demonstrates how to apply multiple LoRA models simultaneously in ComfyUI

In our [ComfyUI LoRA Example](http://docs.comfy.org/tutorials/basic/lora), we introduced how to load and use a single LoRA model, mentioning the node’s chain connection capability.

This tutorial demonstrates chaining multiple `Load LoRA` nodes to apply two LoRA models simultaneously: [blindbox\_V1Mix](https://civitai.com/models/25995?modelVersionId=32988) and [MoXinV1](https://civitai.com/models/12597?modelVersionId=14856).

The comparison below shows individual effects of these LoRAs using identical parameters:

By chaining multiple LoRA models, we achieve a blended style in the final output:

## [​](http://docs.comfy.org#model-installation) Model Installation

Download the [dreamshaper\_8.safetensors](https://civitai.com/api/download/models/128713?type=Model&format=SafeTensor&size=pruned&fp=fp16) file and put it in your `ComfyUI/models/checkpoints` folder.

Download the [blindbox\_V1Mix.safetensors](https://civitai.com/api/download/models/32988?type=Model&format=SafeTensor&size=full&fp=fp16) file and put it in your `ComfyUI/models/loras` folder.

Download the [MoXinV1.safetensors](https://civitai.com/api/download/models/14856?type=Model&format=SafeTensor&size=full&fp=fp16) file and put it in your `ComfyUI/models/loras` folder.

## [​](http://docs.comfy.org#multi-lora-workflow) Multi-LoRA Workflow

Download the image below and **drag it into ComfyUI** to load the workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

## [​](http://docs.comfy.org#complete-the-workflow-step-by-step) Complete the Workflow Step by Step

Follow the steps in the diagram below to ensure the workflow runs correctly.

1. Ensure `Load Checkpoint` loads **dreamshaper\_8.safetensors**
2. Ensure first `Load LoRA` loads **blindbox\_V1Mix.safetensors**
3. Ensure second `Load LoRA` loads **MoXinV1.safetensors**
4. Click `Queue` or press `Ctrl/Cmd + Enter` to generate

## [​](http://docs.comfy.org#try-it-yourself) Try It Yourself

1. Adjust `strength_model` values in both `Load LoRA` nodes to control each LoRA’s influence
2. Explore [CivitAI](https://civitai.com/models) for additional LoRAs and create custom combinations

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/multiple-loras.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/lora)

[ControlNetThis guide will introduce you to the basic concepts of ControlNet and demonstrate how to generate corresponding images in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/controlnet/controlnet)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Model Installation](http://docs.comfy.org#model-installation)
- [Multi-LoRA Workflow](http://docs.comfy.org#multi-lora-workflow)
- [Complete the Workflow Step by Step](http://docs.comfy.org#complete-the-workflow-step-by-step)
- [Try It Yourself](http://docs.comfy.org#try-it-yourself)