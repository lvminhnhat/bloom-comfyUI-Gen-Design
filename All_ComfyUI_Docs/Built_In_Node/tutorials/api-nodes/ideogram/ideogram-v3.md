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
    
    - [Ideogram 3.0](http://docs.comfy.org/tutorials/api-nodes/ideogram/ideogram-v3)
  - Luma
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

ComfyUI Ideogram 3.0 API Node Official Examples

# ComfyUI Ideogram 3.0 API Node Official Examples

This guide covers how to use the Ideogram 3.0 API node in ComfyUI

Ideogram 3.0 is a powerful text-to-image model by Ideogram, known for its photorealistic quality, accurate text rendering, and consistent style control.

The [Ideogram V3](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3) node currently supports two modes:

- Text-to-Image mode
- Image Editing mode (when both image and mask inputs are provided)

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#ideogram-3-0-node-documentation) Ideogram 3.0 Node Documentation

Check the following documentation for detailed node parameter settings:

- [Ideogram V3](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3)

## [​](http://docs.comfy.org#ideogram-3-0-api-node-text-to-image-mode) Ideogram 3.0 API Node Text-to-Image Mode

When using [Ideogram V3](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3) without image and mask inputs, the node operates in Text-to-Image mode.

### [​](http://docs.comfy.org#1-download-workflow-file) 1. Download Workflow File

Download and drag the following file into ComfyUI to load the workflow:

### [​](http://docs.comfy.org#2-complete-the-workflow-steps) 2. Complete the Workflow Steps

Follow the numbered steps to complete the basic workflow:

1. Enter your image description in the `prompt` field of the `Ideogram V3` node
2. Click `Run` or use shortcut `Ctrl(cmd) + Enter` to generate the image
3. After the API returns results, view the generated image in the `Save Image` node. Images are saved to the `ComfyUI/output/` directory

## [​](http://docs.comfy.org#ideogram-3-0-api-node-image-editing-mode) Ideogram 3.0 API Node Image Editing Mode

\[To be updated]

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/ideogram/ideogram-v3.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-diffusion-3-5-image)

[Luma Text to ImageThis guide explains how to use the Luma Text to Image API node in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Ideogram 3.0 Node Documentation](http://docs.comfy.org#ideogram-3-0-node-documentation)
- [Ideogram 3.0 API Node Text-to-Image Mode](http://docs.comfy.org#ideogram-3-0-api-node-text-to-image-mode)
- [1. Download Workflow File](http://docs.comfy.org#1-download-workflow-file)
- [2. Complete the Workflow Steps](http://docs.comfy.org#2-complete-the-workflow-steps)
- [Ideogram 3.0 API Node Image Editing Mode](http://docs.comfy.org#ideogram-3-0-api-node-image-editing-mode)