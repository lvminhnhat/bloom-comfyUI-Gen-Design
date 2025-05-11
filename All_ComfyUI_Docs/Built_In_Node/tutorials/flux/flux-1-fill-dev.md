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
  
  - [Flux.1 Text-to-Image](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image)
  - [Flux.1 fill dev](http://docs.comfy.org/tutorials/flux/flux-1-fill-dev)
  - [Flux.1 ControlNet](http://docs.comfy.org/tutorials/flux/flux-1-controlnet)
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

ComfyUI Flux.1 fill dev Example

# ComfyUI Flux.1 fill dev Example

This guide demonstrates how to use Flux.1 fill dev to create Inpainting and Outpainting workflows.

## [​](http://docs.comfy.org#introduction-to-flux-1-fill-dev-model) Introduction to Flux.1 fill dev Model

Flux.1 fill dev is one of the core tools in the [FLUX.1 Tools suite](https://blackforestlabs.ai/flux-1-tools/) launched by [Black Forest Labs](https://blackforestlabs.ai/), specifically designed for image inpainting and outpainting.

Key features of Flux.1 fill dev:

- Powerful image inpainting and outpainting capabilities, with results second only to the commercial version FLUX.1 Fill \[pro].
- Excellent prompt understanding and following ability, precisely capturing user intent while maintaining high consistency with the original image.
- Advanced guided distillation training technology, making the model more efficient while maintaining high-quality output.
- Friendly licensing terms, with generated outputs usable for personal, scientific, and commercial purposes, please refer to the [FLUX.1 \[dev\] non-commercial license](https://huggingface.co/black-forest-labs/FLUX.1-dev/blob/main/LICENSE.md) for details.

Open Source Repository: [FLUX.1 \[dev\]](https://huggingface.co/black-forest-labs/FLUX.1-dev)

This guide will demonstrate inpainting and outpainting workflows based on the Flux.1 fill dev model. If you’re not familiar with inpainting and outpainting workflows, you can refer to [ComfyUI Layout Inpainting Example](http://docs.comfy.org/tutorials/basic/inpaint) and [ComfyUI Image Extension Example](http://docs.comfy.org/tutorials/basic/outpaint) for some related explanations.

## [​](http://docs.comfy.org#flux-1-fill-dev-and-related-models-installation) Flux.1 Fill dev and related models installation

Before we begin, let’s complete the installation of the Flux.1 Fill dev model files. The inpainting and outpainting workflows will use exactly the same model files. If you’ve previously used the full version of the [Flux.1 Text-to-Image workflow](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image), then you only need to download the **flux1-fill-dev.safetensors** model file in this section.

However, since downloading the corresponding model requires agreeing to the corresponding usage agreement, please visit the [black-forest-labs/FLUX.1-Fill-dev](https://huggingface.co/black-forest-labs/FLUX.1-Fill-dev) page and make sure you have agreed to the corresponding agreement as shown in the image below.

Complete model list:

- [clip\_l.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/clip_l.safetensors?download=true)
- [t5xxl\_fp16.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp16.safetensors?download=true)
- [ae.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/ae.safetensors?download=true)
- [flux1-fill-dev.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-Fill-dev/resolve/main/flux1-fill-dev.safetensors?download=true)

File storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │    ├── clip_l.safetensors
│   │    └── t5xxl_fp16.safetensors
│   ├── vae/
│   │    └── ae.safetensors
│   └── diffusion_models/
│        └── flux1-fill-dev.safetensors
```

## [​](http://docs.comfy.org#flux-1-fill-dev-inpainting-workflow) Flux.1 Fill dev inpainting workflow

### [​](http://docs.comfy.org#1-inpainting-workflow-and-asset) 1. Inpainting workflow and asset

Please download the image below and drag it into ComfyUI to load the corresponding workflow

Please download the image below, we will use it as the input image

The corresponding image already contains an alpha channel, so you don’t need to draw a mask separately. If you want to draw your own mask, please [click here](https://raw.githubusercontent.com/Comfy-Org/example_workflows/main/flux/inpaint/flux_fill_inpaint_input_original.png) to get the image without a mask, and refer to the MaskEditor usage section in the [ComfyUI Layout Inpainting Example](http://docs.comfy.org/tutorials/basic/inpaint#using-the-mask-editor) to learn how to draw a mask in the `Load Image` node.

### [​](http://docs.comfy.org#2-steps-to-run-the-workflow) 2. Steps to run the workflow

1. Ensure the `Load Diffusion Model` node has `flux1-fill-dev.safetensors` loaded.
2. Ensure the `DualCLIPLoader` node has the following models loaded:
   
   - clip\_name1: `t5xxl_fp16.safetensors`
   - clip\_name2: `clip_l.safetensors`
3. Ensure the `Load VAE` node has `ae.safetensors` loaded.
4. Upload the input image provided in the document to the `Load Image` node; if you’re using the version without a mask, remember to complete the mask drawing using the mask editor
5. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

## [​](http://docs.comfy.org#flux-1-fill-dev-outpainting-workflow) Flux.1 Fill dev Outpainting Workflow

### [​](http://docs.comfy.org#1-outpainting-workflow-and-asset) 1. Outpainting workflow and asset

Please download the image below and drag it into ComfyUI to load the corresponding workflow

Please download the image below, we will use it as the input image

### [​](http://docs.comfy.org#2-steps-to-run-the-workflow-2) 2. Steps to run the workflow

1. Ensure the `Load Diffusion Model` node has `flux1-fill-dev.safetensors` loaded.
2. Ensure the `DualCLIPLoader` node has the following models loaded:
   
   - clip\_name1: `t5xxl_fp16.safetensors`
   - clip\_name2: `clip_l.safetensors`
3. Ensure the `Load VAE` node has `ae.safetensors` loaded.
4. Upload the input image provided in the document to the `Load Image` node
5. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/flux/flux-1-fill-dev.mdx)

[Previous](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image)

[Flux.1 ControlNetThis guide will demonstrate workflow examples using Flux.1 ControlNet.  
\
Next](http://docs.comfy.org/tutorials/flux/flux-1-controlnet)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Introduction to Flux.1 fill dev Model](http://docs.comfy.org#introduction-to-flux-1-fill-dev-model)
- [Flux.1 Fill dev and related models installation](http://docs.comfy.org#flux-1-fill-dev-and-related-models-installation)
- [Flux.1 Fill dev inpainting workflow](http://docs.comfy.org#flux-1-fill-dev-inpainting-workflow)
- [1. Inpainting workflow and asset](http://docs.comfy.org#1-inpainting-workflow-and-asset)
- [2. Steps to run the workflow](http://docs.comfy.org#2-steps-to-run-the-workflow)
- [Flux.1 Fill dev Outpainting Workflow](http://docs.comfy.org#flux-1-fill-dev-outpainting-workflow)
- [1. Outpainting workflow and asset](http://docs.comfy.org#1-outpainting-workflow-and-asset)
- [2. Steps to run the workflow](http://docs.comfy.org#2-steps-to-run-the-workflow-2)