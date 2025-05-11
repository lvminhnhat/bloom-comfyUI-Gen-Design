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
    
    - [Flux 1.1 Pro Ultra Image](http://docs.comfy.org/tutorials/api-nodes/black-forest-labs/flux-1-1-pro-ultra-image)
  - Stability AI
  - Ideogram
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

Flux 1.1 Pro Ultra Image API Node ComfyUI Official Workflow Examples

# Flux 1.1 Pro Ultra Image API Node ComfyUI Official Workflow Examples

This guide covers how to use the Flux 1.1 Pro Ultra Image API node in ComfyUI

FLUX 1.1 Pro Ultra is a high-performance AI image generation tool by BlackForestLabs, featuring ultra-high resolution and efficient generation capabilities. It supports up to 4MP resolution (4x the standard version) while keeping single image generation time under 10 seconds - 2.5x faster than similar high-resolution models.

The tool offers two core modes:

- **Ultra Mode**: Designed for high-resolution needs, perfect for advertising and e-commerce where detail magnification is important. It accurately reflects prompts while maintaining generation speed.
- **Raw Mode**: Focuses on natural realism, optimizing skin tones, lighting, and landscape details. Reduces the “AI look” and is ideal for photography and realistic style creation.

We now support the Flux 1.1 Pro Ultra Image node in ComfyUI. This guide will cover:

- Flux 1.1 Pro Text-to-Image
- Flux 1.1 Pro Image-to-Image (Remix)

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#flux-1-1-pro-ultra-image-node-documentation) Flux 1.1 Pro Ultra Image Node Documentation

Check the following documentation for detailed node parameter settings:

- [Flux 1.1 Pro Ultra Image](http://docs.comfy.org/built-in-nodes/api-node/image/bfl/flux-pro-ultra-image)

## [​](http://docs.comfy.org#flux-1-1-%5Bpro%5D-text-to-image-tutorial) Flux 1.1 \[pro] Text-to-Image Tutorial

### [​](http://docs.comfy.org#1-download-workflow-file) 1. Download Workflow File

Download and drag the following file into ComfyUI to load the workflow:

### [​](http://docs.comfy.org#2-complete-the-workflow-steps) 2. Complete the Workflow Steps

Follow the numbered steps to complete the basic workflow:

1. (Optional) Modify the prompt in the `Flux 1.1 [pro] Ultra Image` node
2. (Optional) Set `raw` parameter to `false` for more realistic output
3. Click `Run` or use shortcut `Ctrl(cmd) + Enter` to generate the image
4. After the API returns results, view the generated image in the `Save Image` node. Images are saved to the `ComfyUI/output/` directory

## [​](http://docs.comfy.org#flux-1-1%5Bpro%5D-image-to-image-tutorial) Flux 1.1\[pro] Image-to-Image Tutorial

When adding an `image_prompt` to the node input, the output will blend features from the input image (Remix). The `image_prompt_strength` value affects the blend ratio: higher values make the output more similar to the input image.

### [​](http://docs.comfy.org#1-download-workflow-file-2) 1. Download Workflow File

Download and drag the following file into ComfyUI, or right-click the purple node in the Text-to-Image workflow and set `mode` to `always` to enable `image_prompt` input:

We’ll use this image as input:

### [​](http://docs.comfy.org#2-complete-the-workflow-steps-2) 2. Complete the Workflow Steps

Follow these numbered steps:

1. Click **Upload** on the `Load Image` node to upload your input image
2. (Optional) Adjust `image_prompt_strength` in `Flux 1.1 [pro] Ultra Image` to change the blend ratio
3. Click `Run` or use shortcut `Ctrl(cmd) + Enter` to generate the image
4. After the API returns results, view the generated image in the `Save Image` node. Images are saved to the `ComfyUI/output/` directory

Here’s a comparison of outputs with different `image_prompt_strength` values:

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/black-forest-labs/flux-1-1-pro-ultra-image.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/pricing)

[Stable Image UltraThis article will introduce how to use the Stability AI Stable Image Ultra API node's text-to-image and image-to-image capabilities in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-image-ultra)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Flux 1.1 Pro Ultra Image Node Documentation](http://docs.comfy.org#flux-1-1-pro-ultra-image-node-documentation)
- [Flux 1.1 \[pro\] Text-to-Image Tutorial](http://docs.comfy.org#flux-1-1-%5Bpro%5D-text-to-image-tutorial)
- [1. Download Workflow File](http://docs.comfy.org#1-download-workflow-file)
- [2. Complete the Workflow Steps](http://docs.comfy.org#2-complete-the-workflow-steps)
- [Flux 1.1\[pro\] Image-to-Image Tutorial](http://docs.comfy.org#flux-1-1%5Bpro%5D-image-to-image-tutorial)
- [1. Download Workflow File](http://docs.comfy.org#1-download-workflow-file-2)
- [2. Complete the Workflow Steps](http://docs.comfy.org#2-complete-the-workflow-steps-2)