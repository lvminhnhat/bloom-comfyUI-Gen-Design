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

ComfyUI Outpainting Workflow Example

# ComfyUI Outpainting Workflow Example

This guide will introduce you to the outpainting workflow in ComfyUI and walk you through an outpainting example

This guide will introduce you to the concept of outpainting in AI image generation and how to create an outpainting workflow in ComfyUI. We will cover:

- Using outpainting workflow to extend an image
- Understanding and using outpainting-related nodes in ComfyUI
- Mastering the basic outpainting process

## [​](http://docs.comfy.org#about-outpainting) About Outpainting

In AI image generation, we often encounter situations where an existing image has good composition but the canvas area is too small, requiring us to extend the canvas to get a larger scene. This is where outpainting comes in.

Basically, it requires similar content to [Inpainting](http://docs.comfy.org/tutorials/basic/inpaint), but we use different nodes to **build the mask**.

Outpainting applications include:

- **Scene Extension:** Expand the scene range of the original image to show a more complete environment
- **Composition Adjustment:** Optimize the overall composition by extending the canvas
- **Content Addition:** Add more related scene elements to the original image

## [​](http://docs.comfy.org#comfyui-outpainting-workflow-example-explanation) ComfyUI Outpainting Workflow Example Explanation

### [​](http://docs.comfy.org#preparation) Preparation

#### [​](http://docs.comfy.org#1-model-installation) 1. Model Installation

Download the following model file and save it to `ComfyUI/models/checkpoints` directory:

- [512-inpainting-ema.safetensors](https://huggingface.co/stabilityai/stable-diffusion-2-inpainting/blob/main/512-inpainting-ema.safetensors)

#### [​](http://docs.comfy.org#2-input-image) 2. Input Image

Prepare an image you want to extend. In this example, we will use the following image:

#### [​](http://docs.comfy.org#3-outpainting-workflow) 3. Outpainting Workflow

Download the image below and **drag it into ComfyUI** to load the workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

### [​](http://docs.comfy.org#outpainting-workflow-usage-explanation) Outpainting Workflow Usage Explanation

The key steps of the outpainting workflow are as follows:

1. Load the locally installed model file in the `Load Checkpoint` node
2. Click the `Upload` button in the `Load Image` node to upload your image
3. Click the `Queue` button or use the shortcut `Ctrl + Enter` to execute the image generation

In this workflow, we mainly use the `Pad Image for outpainting` node to control the direction and range of image extension. This is actually an [Inpaint](http://docs.comfy.org/tutorials/basic/inpaint.mdx) workflow, but we use different nodes to build the mask.

### [​](http://docs.comfy.org#pad-image-for-outpainting-node) Pad Image for outpainting Node

This node accepts an input image and outputs an extended image with a corresponding mask, where the mask is built based on the node parameters.

#### [​](http://docs.comfy.org#input-parameters) Input Parameters

Parameter NameFunction`image`Input image`left`Left padding amount`top`Top padding amount`right`Right padding amount`bottom`Bottom padding amount`feathering`Controls the smoothness of the transition between the original image and the added padding, higher values create smoother transitions

#### [​](http://docs.comfy.org#output-parameters) Output Parameters

Parameter NameFunction`image`Output `image` represents the padded image`mask`Output `mask` indicates the original image area and the added padding area

#### [​](http://docs.comfy.org#node-output-content) Node Output Content

After processing by the `Pad Image for outpainting` node, the output image and mask preview are as follows:

You can see the corresponding output results:

- The `Image` output is the extended image
- The `Mask` output is the mask marking the extension areas

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/outpaint.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/inpaint)

[UpscaleThis guide explains the concept of image upscaling in AI drawing and demonstrates how to implement an image upscaling workflow in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/basic/upscale)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [About Outpainting](http://docs.comfy.org#about-outpainting)
- [ComfyUI Outpainting Workflow Example Explanation](http://docs.comfy.org#comfyui-outpainting-workflow-example-explanation)
- [Preparation](http://docs.comfy.org#preparation)
- [1. Model Installation](http://docs.comfy.org#1-model-installation)
- [2. Input Image](http://docs.comfy.org#2-input-image)
- [3. Outpainting Workflow](http://docs.comfy.org#3-outpainting-workflow)
- [Outpainting Workflow Usage Explanation](http://docs.comfy.org#outpainting-workflow-usage-explanation)
- [Pad Image for outpainting Node](http://docs.comfy.org#pad-image-for-outpainting-node)
- [Input Parameters](http://docs.comfy.org#input-parameters)
- [Output Parameters](http://docs.comfy.org#output-parameters)
- [Node Output Content](http://docs.comfy.org#node-output-content)