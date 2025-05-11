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
  - OpenAI
  - Recraft
    
    - [Recraft Text to Image](http://docs.comfy.org/tutorials/api-nodes/recraft/recraft-text-to-image)

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

Recraft Text to Image API Node ComfyUI Official Example

# Recraft Text to Image API Node ComfyUI Official Example

Learn how to use the Recraft Text to Image API node in ComfyUI

The [Recraft Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-image) node allows you to create high-quality images in various styles using Recraft AI’s image generation technology based on text descriptions.

In this guide, we’ll show you how to set up a text-to-image workflow using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#recraft-text-to-image-api-node-workflow) Recraft Text to Image API Node Workflow

### [​](http://docs.comfy.org#1-download-the-workflow-file) 1. Download the Workflow File

The workflow information is included in the metadata of the image below. Download and drag it into ComfyUI to load the workflow.

### [​](http://docs.comfy.org#2-follow-the-steps-to-run-the-workflow) 2. Follow the Steps to Run the Workflow

Follow these numbered steps to run the basic workflow:

1. (Optional) Change the `Recraft Color RGB` in the `Color` node to your desired color
2. (Optional) Modify the `Recraft Style` node to control the visual style, such as digital art, realistic photo, or logo design. This group includes other style nodes you can enable as needed
3. (Optional) Edit the `prompt` parameter in the `Recraft Text to Image` node. You can also change the `size` parameter
4. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to generate the image
5. After the API returns the result, you can view the generated image in the `Save Image` node. The image will also be saved to the `ComfyUI/output/` directory

> (Optional) We’ve included a **Convert to SVG** group in the workflow. Since the `Recraft Vectorize Image` node in this group consumes additional credits, enable it only when you need to convert the generated image to SVG format

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- **Recraft Style**: Offers various preset styles like realistic photos, digital art, and logo designs
- **Seed Parameter**: Only used to determine if the node should run again, the actual generation result is not affected by the seed value

## [​](http://docs.comfy.org#related-node-documentation) Related Node Documentation

Check the following documentation for detailed parameter settings of the nodes

[**Recraft Text to Image Node Documentation**  
\
Documentation for the Recraft Text to Image API node](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-image)

[**Recraft Style Node Documentation**  
\
Documentation for the Recraft Style - Realistic Image API node](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-realistic-image)

[**Recraft Controls Node Documentation**  
\
Documentation for the Recraft Controls API node](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-controls)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/recraft/recraft-text-to-image.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/openai/dall-e-3)

[Contributing  
\
Next](http://docs.comfy.org/community/contributing)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Recraft Text to Image API Node Workflow](http://docs.comfy.org#recraft-text-to-image-api-node-workflow)
- [1. Download the Workflow File](http://docs.comfy.org#1-download-the-workflow-file)
- [2. Follow the Steps to Run the Workflow](http://docs.comfy.org#2-follow-the-steps-to-run-the-workflow)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)
- [Related Node Documentation](http://docs.comfy.org#related-node-documentation)