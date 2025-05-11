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

Luma Text to Video API Node ComfyUI Official Guide

# Luma Text to Video API Node ComfyUI Official Guide

Learn how to use the Luma Text to Video API node in ComfyUI

The [Luma Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video) node allows you to create high-quality, smooth videos from text descriptions using Luma AI’s innovative video generation technology.

In this guide, we’ll show you how to set up a text-to-video workflow using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#luma-text-to-video-node-documentation) Luma Text to Video Node Documentation

Check out the following documentation to learn more about the node parameters:

[**Luma Text to Video Node Docs**  
\
Documentation for the Luma Text to Video API node](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video)

[**Luma Concepts Node Docs**  
\
Documentation for the Luma Concepts API node](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)

## [​](http://docs.comfy.org#text-to-video-workflow-with-luma-api-node) Text to Video Workflow with Luma API Node

The Luma Text to Video node requires text prompts to describe the video content. In this guide, we’ve created examples using `prompt` and `luma_concepts` to showcase Luma AI’s excellent video generation capabilities.

### [​](http://docs.comfy.org#1-download-the-workflow) 1. Download the Workflow

The workflow information is included in the metadata of the video below. Download and drag it into ComfyUI to load the workflow.

### [​](http://docs.comfy.org#2-follow-the-steps) 2. Follow the Steps

Follow these basic steps to run the workflow:

1. Write your prompt in the `Luma Text to Video` node to describe the video content you want
2. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to generate the video
3. After the API returns results, you can view the generated video in the `Save Video` node. The video will also be saved to the `ComfyUI/output/` directory

> (Optional) Modify the `Luma Concepts` node to control camera movements and add professional cinematography

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- **Writing Prompts**: Describe scenes, subjects, actions, and mood in detail for best results
- **Luma Concepts**: Mainly used for camera control to create professional video shots
- **Seed Parameter**: Only determines if the node should rerun, doesn’t affect generation results
- **Model Selection**: Different video models have different features, adjustable via the model parameter
- **Resolution and Duration**: Adjust output video resolution and length using these parameters
- **Ray 1.6 Model Note**: Duration and resolution parameters don’t work when using the Ray 1.6 model

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/luma/luma-text-to-video.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-image)

[Luma Image to VideoLearn how to use the Luma Image to Video API node in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Luma Text to Video Node Documentation](http://docs.comfy.org#luma-text-to-video-node-documentation)
- [Text to Video Workflow with Luma API Node](http://docs.comfy.org#text-to-video-workflow-with-luma-api-node)
- [1. Download the Workflow](http://docs.comfy.org#1-download-the-workflow)
- [2. Follow the Steps](http://docs.comfy.org#2-follow-the-steps)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)