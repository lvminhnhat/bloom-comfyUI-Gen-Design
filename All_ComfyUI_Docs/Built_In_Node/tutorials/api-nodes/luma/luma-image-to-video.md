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

Luma Image to Video API Node ComfyUI Official Example

# Luma Image to Video API Node ComfyUI Official Example

Learn how to use the Luma Image to Video API node in ComfyUI

The [Luma Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video) node allows you to convert static images into smooth, dynamic videos using Luma AI’s advanced technology, bringing life and motion to your images.

In this guide, we’ll show you how to set up a workflow for image-to-video conversion using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#luma-image-to-video-node-documentation) Luma Image to Video Node Documentation

Check out the following documentation to learn more about the node’s parameters:

[**Luma Image to Video Node Docs**  
\
Luma Image to Video API node documentation](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video)

[**Luma Concepts Node Docs**  
\
Luma Concepts API node documentation](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)

## [​](http://docs.comfy.org#image-to-video-workflow-with-luma-api-node) Image to Video Workflow with Luma API Node

The Luma Image to Video node requires at least one image input (`first_image` or `last_image`) along with text prompts to determine the video’s motion effects. In this guide, we’ve created an example using `first_image` and `luma_concepts` to showcase Luma AI’s video generation capabilities.

### [​](http://docs.comfy.org#1-download-the-workflow) 1. Download the Workflow

The workflow information is included in the metadata of the video below. Download and drag it into ComfyUI to load the workflow.

Download the following image to use as input:

### [​](http://docs.comfy.org#2-follow-the-workflow-steps) 2. Follow the Workflow Steps

Follow these basic steps to run the workflow:

1. Upload your input image in the `first_image` node
2. (Optional) Write prompts in the Luma Image to Video node to describe how you want the image animated
3. (Optional) Modify the `Luma Concepts` node to control camera movement for professional cinematography
4. Click `Run` or use `Ctrl(cmd) + Enter` to generate the video
5. Once the API returns results, view the generated video in the `Save Video` node. The video will also be saved to the `ComfyUI/output/` directory

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- **Image Input Requirements**: At least one of `first_image` or `last_image` is required, with a maximum of 1 image per input
- **Luma Concepts**: Controls camera movement for professional video effects
- **Seed Parameter**: Only determines if the node should rerun, doesn’t affect generation results
- **Enable Input Nodes**: Right-click on purple “Bypass” mode nodes and set “mode” to “always” to enable inputs
- **Model Selection**: Different video generation models have unique characteristics, adjustable via the model parameter
- **Resolution and Duration**: Adjust output video resolution and length using resolution and duration parameters

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/luma/luma-image-to-video.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-video)

[GPT-Image-1Learn how to use the OpenAI GPT-Image-1 API node to generate images in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/openai/gpt-image-1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Luma Image to Video Node Documentation](http://docs.comfy.org#luma-image-to-video-node-documentation)
- [Image to Video Workflow with Luma API Node](http://docs.comfy.org#image-to-video-workflow-with-luma-api-node)
- [1. Download the Workflow](http://docs.comfy.org#1-download-the-workflow)
- [2. Follow the Workflow Steps](http://docs.comfy.org#2-follow-the-workflow-steps)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)