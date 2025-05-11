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
  
  - [Overview](http://docs.comfy.org/tutorials/api-nodes/overview)
  - [FAQs](http://docs.comfy.org/tutorials/api-nodes/faq)
  - [Pricing](http://docs.comfy.org/tutorials/api-nodes/pricing)
  - Black Forest Labs
  - Stability AI
  - Ideogram
  - Luma
    
    - [Luma Text to Image](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-image)
    - [Luma Image to Image](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-image)
    - [Luma Text to Video](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-video)
    - [Luma Image to Video](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-video)
  - OpenAI
  - Recraft

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

Luma Text to Image API Node ComfyUI Official Example

# Luma Text to Image API Node ComfyUI Official Example

This guide explains how to use the Luma Text to Image API node in ComfyUI

The [Luma Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image) node allows you to generate high-quality images from text prompts using Luma AI’s advanced technology, capable of creating photorealistic content and artistic style images.

In this guide, we’ll show you how to set up workflows using this node for text-to-image generation.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#luma-text-to-image-node-documentation) Luma Text to Image Node Documentation

You can refer to the following documentation for detailed parameter settings:

[**Luma Text to Image Node Documentation**  
\
Luma Text to Image API Node Documentation](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image)

[**Luma Reference Node Documentation**  
\
Luma Reference API Node Documentation](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-reference)

## [​](http://docs.comfy.org#luma-text-to-image-api-node-workflow) Luma Text to Image API Node Workflow

When the `Luma Text to Image` node is used without any image inputs, it functions as a text-to-image workflow. In this guide, we’ve created examples using `style_image` and `image_luma_ref` to showcase Luma AI’s excellent image processing capabilities.

### [​](http://docs.comfy.org#1-download-workflow-files) 1. Download Workflow Files

The workflow information is included in the metadata of the image below. Download and drag it into ComfyUI to load the workflow.

Please download these images for input:

### [​](http://docs.comfy.org#2-follow-steps-to-run-the-workflow) 2. Follow Steps to Run the Workflow

Follow the numbered steps in the image to complete the basic workflow:

1. Upload the reference image in the `Load image` node
2. Upload the style reference image in the `Load image (renamed to styleref)` node
3. (Optional) Modify the prompts in the `Luma Text to Image` node
4. (Optional) Adjust the `style_image_weight` to control the style reference image’s influence
5. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to generate the image
6. After the API returns results, view the generated image in the `Save Image` node. Images are saved to the `ComfyUI/output/` directory

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- The [node](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image) allows up to 4 reference images and character references simultaneously.
- To enable multiple image inputs, right-click on the purple “Bypassed” nodes and set their `mode` to `always`

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/luma/luma-text-to-image.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/ideogram/ideogram-v3)

[Luma Image to ImageThis guide covers how to use the Luma Image to Image API node in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Luma Text to Image Node Documentation](http://docs.comfy.org#luma-text-to-image-node-documentation)
- [Luma Text to Image API Node Workflow](http://docs.comfy.org#luma-text-to-image-api-node-workflow)
- [1. Download Workflow Files](http://docs.comfy.org#1-download-workflow-files)
- [2. Follow Steps to Run the Workflow](http://docs.comfy.org#2-follow-steps-to-run-the-workflow)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)