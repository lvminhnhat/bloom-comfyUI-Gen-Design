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

ComfyUI Image Upscale Workflow

# ComfyUI Image Upscale Workflow

This guide explains the concept of image upscaling in AI drawing and demonstrates how to implement an image upscaling workflow in ComfyUI

## [​](http://docs.comfy.org#what-is-image-upscaling%3F) What is Image Upscaling?

Image Upscaling is the process of converting low-resolution images to high-resolution using algorithms. Unlike traditional interpolation methods, AI upscaling models (like ESRGAN) can intelligently reconstruct details while maintaining image quality.

For instance, the default SD1.5 model often struggles with large-size image generation. To achieve high-resolution results,we typically generate smaller images first and then use upscaling techniques.

This article covers one of many upscaling methods in ComfyUI. In this tutorial, we’ll guide you through:

1. Downloading and installing upscaling models
2. Performing basic image upscaling
3. Combining text-to-image workflows with upscaling

## [​](http://docs.comfy.org#upscaling-workflow) Upscaling Workflow

### [​](http://docs.comfy.org#model-installation) Model Installation

Required ESRGAN models download:

1

Visit OpenModelDB

Visit [OpenModelDB](https://openmodeldb.info/) to search and download upscaling models (e.g., RealESRGAN)

As shown:

1. Filter models by image type using the category selector
2. The model’s magnification factor is indicated in the top-right corner (e.g., 2x in the screenshot)

We’ll use the [4x-ESRGAN](https://openmodeldb.info/models/4x-ESRGAN) model for this tutorial. Click the `Download` button on the model detail page.

2

Save Model Files in Directory

Save the model file (.pth) in `ComfyUI/models/upscale_models` directory

### [​](http://docs.comfy.org#workflow-and-assets) Workflow and Assets

Download and drag the following image into ComfyUI to load the basic upscaling workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

Use this image in smaller size as input:

### [​](http://docs.comfy.org#complete-the-workflow-step-by-step) Complete the Workflow Step by Step

Follow the steps in the diagram below to ensure the workflow runs correctly.

1. Ensure `Load Upscale Model` loads `4x-ESRGAN.pth`
2. Upload the input image to the `Load Image` node
3. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to generate the image

The core components are the `Load Upscale Model` and `Upscale Image (Using Model)` nodes, which receive an image input and upscale it using the selected model.

## [​](http://docs.comfy.org#text-to-image-combined-workflow) Text-to-Image Combined Workflow

After mastering basic upscaling, we can combine it with the [text-to-image](http://docs.comfy.org/tutorials/basic/text-to-image) workflow. For text-to-image basics, refer to the [text-to-image tutorial](http://docs.comfy.org/tutorials/basic/text-to-image).

Download and drag this image into ComfyUI to load the combined workflow:

This workflow connects the text-to-image output image directly to the upscaling nodes for final processing.

## [​](http://docs.comfy.org#additional-tips) Additional Tips

Model characteristics:

- **RealESRGAN**: General-purpose upscaling
- **BSRGAN**: Excels with text and sharp edges
- **SwinIR**: Preserves natural textures, ideal for landscapes

<!--THE END-->

1. **Chained Upscaling**: Combine multiple upscale nodes (e.g., 2x → 4x) for ultra-high magnification
2. **Hybrid Workflow**: Connect upscale nodes after generation for “generate+enhance” pipelines
3. **Comparative Testing**: Different models perform better on specific image types - test multiple options

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/upscale.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/outpaint)

[LoRAThis guide will help you understand and use a single LoRA model  
\
Next](http://docs.comfy.org/tutorials/basic/lora)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [What is Image Upscaling?](http://docs.comfy.org#what-is-image-upscaling%3F)
- [Upscaling Workflow](http://docs.comfy.org#upscaling-workflow)
- [Model Installation](http://docs.comfy.org#model-installation)
- [Workflow and Assets](http://docs.comfy.org#workflow-and-assets)
- [Complete the Workflow Step by Step](http://docs.comfy.org#complete-the-workflow-step-by-step)
- [Text-to-Image Combined Workflow](http://docs.comfy.org#text-to-image-combined-workflow)
- [Additional Tips](http://docs.comfy.org#additional-tips)