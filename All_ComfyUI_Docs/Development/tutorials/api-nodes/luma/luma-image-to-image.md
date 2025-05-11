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

Luma Image to Image API Node ComfyUI Official Example

# Luma Image to Image API Node ComfyUI Official Example

This guide covers how to use the Luma Image to Image API node in ComfyUI

The [Luma Image to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-image-to-image) node allows you to modify existing images based on text prompts using Luma AI technology, while preserving certain features and structures from the original image.

In this guide, we’ll show you how to set up an image-to-image workflow using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#luma-image-to-image-node-documentation) Luma Image to Image Node Documentation

Check the following documentation for detailed node parameter settings:

[**Luma Image to Image Node Documentation**  
\
Luma Image to Image API Node Documentation](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-image-to-image)

## [​](http://docs.comfy.org#luma-image-to-image-api-node-workflow) Luma Image to Image API Node Workflow

This feature works well for changing objects and shapes. However, it may not be ideal for color changes. We recommend using lower weight values, around 0.0 to 0.1.

### [​](http://docs.comfy.org#1-download-workflow-file) 1. Download Workflow File

Download and drag the following image into ComfyUI to load the workflow (workflow information is included in the image metadata):

Download this image to use as input:

### [​](http://docs.comfy.org#2-complete-the-workflow-steps) 2. Complete the Workflow Steps

Follow these numbered steps:

1. Click **Upload** on the `Load Image` node to upload your input image
2. (Optional) Modify the workflow prompts
3. (Optional) Adjust `image_weight` to change input image influence (lower values stay closer to original)
4. Click `Run` or use shortcut `Ctrl(cmd) + Enter` to generate the image
5. After API returns results, view the generated image in the `Save Image` node. Images are saved to the `ComfyUI/output/` directory

### [​](http://docs.comfy.org#3-results-with-different-image-weight-values) 3. Results with Different `image_weight` Values

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/luma/luma-image-to-image.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-image)

[Luma Text to VideoLearn how to use the Luma Text to Video API node in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Luma Image to Image Node Documentation](http://docs.comfy.org#luma-image-to-image-node-documentation)
- [Luma Image to Image API Node Workflow](http://docs.comfy.org#luma-image-to-image-api-node-workflow)
- [1. Download Workflow File](http://docs.comfy.org#1-download-workflow-file)
- [2. Complete the Workflow Steps](http://docs.comfy.org#2-complete-the-workflow-steps)
- [3. Results with Different image\_weight Values](http://docs.comfy.org#3-results-with-different-image-weight-values)