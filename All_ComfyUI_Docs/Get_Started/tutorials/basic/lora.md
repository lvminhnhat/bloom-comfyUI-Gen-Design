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

ComfyUI LoRA Example

# ComfyUI LoRA Example

This guide will help you understand and use a single LoRA model

**LoRA (Low-Rank Adaptation)** is an efficient technique for fine-tuning large generative models like Stable Diffusion. It introduces trainable low-rank matrices to the pre-trained model, adjusting only a portion of parameters rather than retraining the entire model, thus achieving optimization for specific tasks at a lower computational cost. Compared to base models like SD1.5, LoRA models are smaller and easier to train.

The image above compares generation with the same parameters using [dreamshaper\_8](https://civitai.com/models/4384?modelVersionId=128713) directly versus using the [blindbox\_V1Mix](https://civitai.com/models/25995/blindbox) LoRA model. As you can see, by using a LoRA model, we can generate images in different styles without adjusting the base model.

We will demonstrate how to use a LoRA model. All LoRA variants: Lycoris, loha, lokr, locon, etc… are used in the same way.

In this example, we will learn how to load and use a LoRA model in [ComfyUI](https://github.com/comfyanonymous/ComfyUI), covering the following topics:

1. Installing a LoRA model
2. Generating images using a LoRA model
3. A simple introduction to the `Load LoRA` node

## [​](http://docs.comfy.org#required-model-installation) Required Model Installation

Download the [dreamshaper\_8.safetensors](https://civitai.com/api/download/models/128713?type=Model&format=SafeTensor&size=pruned&fp=fp16) file and put it in your `ComfyUI/models/checkpoints` folder.

Download the [blindbox\_V1Mix.safetensors](https://civitai.com/api/download/models/32988?type=Model&format=SafeTensor&size=full&fp=fp16) file and put it in your `ComfyUI/models/loras` folder.

## [​](http://docs.comfy.org#lora-workflow-file) LoRA Workflow File

Download the image below and **drag it into ComfyUI** to load the workflow.

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

## [​](http://docs.comfy.org#complete-the-workflow-step-by-step) Complete the Workflow Step by Step

Follow the steps in the diagram below to ensure the workflow runs correctly.

1. Ensure `Load Checkpoint` loads `dreamshaper_8.safetensors`
2. Ensure `Load LoRA` loads `blindbox_V1Mix.safetensors`
3. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to generate the image

## [​](http://docs.comfy.org#load-lora-node-introduction) Load LoRA Node Introduction

Models in the `ComfyUI\models\loras` folder will be detected by ComfyUI and can be loaded using this node.

### [​](http://docs.comfy.org#input-types) Input Types

Parameter NameFunction`model`Connect to the base model`clip`Connect to the CLIP model`lora_name`Select the LoRA model to load and use`strength_model`Affects how strongly the LoRA influences the model weights; higher values make the LoRA style stronger`strength_clip`Affects how strongly the LoRA influences the CLIP text embeddings

### [​](http://docs.comfy.org#output-types) Output Types

Parameter NameFunction`model`Outputs the model with LoRA adjustments applied`clip`Outputs the CLIP model with LoRA adjustments applied

This node supports chain connections, allowing multiple `Load LoRA` nodes to be linked in series to apply multiple LoRA models. For more details, please refer to [ComfyUI Multiple LoRAs Example](http://docs.comfy.org/tutorials/basic/multiple-loras)

## [​](http://docs.comfy.org#try-it-yourself) Try It Yourself

1. Try modifying the prompt or adjusting different parameters of the `Load LoRA` node, such as `strength_model`, to observe changes in the generated images and become familiar with the `Load LoRA` node.
2. Visit [CivitAI](https://civitai.com/models) to download other kinds of LoRA models and try using them.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/lora.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/upscale)

[Multiple LoRAsThis guide demonstrates how to apply multiple LoRA models simultaneously in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/basic/multiple-loras)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Required Model Installation](http://docs.comfy.org#required-model-installation)
- [LoRA Workflow File](http://docs.comfy.org#lora-workflow-file)
- [Complete the Workflow Step by Step](http://docs.comfy.org#complete-the-workflow-step-by-step)
- [Load LoRA Node Introduction](http://docs.comfy.org#load-lora-node-introduction)
- [Input Types](http://docs.comfy.org#input-types)
- [Output Types](http://docs.comfy.org#output-types)
- [Try It Yourself](http://docs.comfy.org#try-it-yourself)