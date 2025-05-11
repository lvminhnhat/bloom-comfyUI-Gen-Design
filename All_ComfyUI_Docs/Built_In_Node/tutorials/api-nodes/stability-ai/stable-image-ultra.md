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
    
    - [Stable Image Ultra](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-image-ultra)
    - [Stable Diffusion 3.5 Image](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-diffusion-3-5-image)
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

Stability AI Stable Image Ultra API Node ComfyUI Official Example

# Stability AI Stable Image Ultra API Node ComfyUI Official Example

This article will introduce how to use the Stability AI Stable Image Ultra API node’s text-to-image and image-to-image capabilities in ComfyUI

The [Stability Stable Image Ultra](http://docs.comfy.org/built-in-nodes/api-node/image/stability/stability-stable-image-ultra) node allows you to use Stability AI’s Stable Image Ultra model to create high-quality, detailed image content through text prompts or reference images.

In this guide, we will show you how to set up workflows for both text-to-image and image-to-image generation using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#stability-ai-stable-image-ultra-text-to-image-workflow) Stability AI Stable Image Ultra Text-to-Image Workflow

### [​](http://docs.comfy.org#1-workflow-file-download) 1. Workflow File Download

The workflow information is included in the metadata of the image below. Please download and drag it into ComfyUI to load the corresponding workflow.

### [​](http://docs.comfy.org#2-complete-the-workflow-execution-step-by-step) 2. Complete the Workflow Execution Step by Step

You can follow the numbered steps in the image to complete the basic text-to-image workflow:

1. (Optional) Modify the `prompt` parameter in the `Stability AI Stable Image Ultra` node to input your desired image description. More detailed prompts often lead to better image quality. You can use the `(word:weight)` format to control specific word weights, for example: `The sky was crisp (blue:0.3) and (green:0.8)` indicates the sky is blue and green, but green is more prominent.
2. (Optional) Select the `style_preset` parameter to control the visual style of the image. Different preset styles will produce images with different stylistic characteristics, such as “cinematic”, “anime”, etc. Selecting “None” will not apply any specific style.
3. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation.
4. After the API returns the result, you can view the generated image in the `Save Image` node, and the image will also be saved to the `ComfyUI/output/` directory.

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- **Prompt**: The prompt is one of the most important parameters in the generation process. Detailed, clear descriptions will lead to better results. It can include elements like scene, subject, colors, lighting, and style.
- **Style Preset**: Provides multiple preset styles such as cinematic, anime, digital art, etc., which can quickly define the overall style of the image.
- **Negative Prompt**: Used to specify elements you don’t want to appear in the generated image, helping avoid common issues like extra limbs or distorted faces.
- **Seed Parameter**: Can be used to reproduce or fine-tune generation results, helpful for iteration during the creative process.
- Currently, the `Load Image` node is in “Bypass” mode. To enable it, refer to the step guide and right-click on the corresponding node to set “Mode” to “Always” to enable input, which will switch to image-to-image mode.

## [​](http://docs.comfy.org#stability-ai-stable-image-ultra-image-to-image-workflow) Stability AI Stable Image Ultra Image-to-Image Workflow

### [​](http://docs.comfy.org#1-workflow-file-download-2) 1. Workflow File Download

The workflow information is included in the metadata of the image below. Please download and drag it into ComfyUI to load the corresponding workflow.

Download the image below which we will use as input

### [​](http://docs.comfy.org#2-complete-the-workflow-execution-step-by-step-2) 2. Complete the Workflow Execution Step by Step

You can follow the numbered steps in the image to complete the image-to-image workflow:

1. Load a reference image through the `Load Image` node, which will serve as the basis for generation.
2. (Optional) Modify the `prompt` parameter in the `Stability Stable Image Ultra` node to describe elements you want to change or enhance in the reference image.
3. (Optional) Adjust the `image_denoise` parameter (range 0.0-1.0) to control the degree of modification to the original image:
   
   - Values closer to 0.0 will make the generated image more similar to the input reference image
   - Values closer to 1.0 will make the generated image more like pure text-to-image generation
4. (Optional) You can also set `style_preset` and other parameters to further control the generation effect.
5. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation.
6. After the API returns the result, you can view the generated image in the `Save Image` node, and the image will also be saved to the `ComfyUI/output/` directory.

### [​](http://docs.comfy.org#3-additional-notes-2) 3. Additional Notes

**Image Denoise**: This parameter determines how much of the original image’s features are preserved during generation, and is the most crucial adjustment parameter in image-to-image mode. The image below shows the effects of different denoising strengths

- **Reference Image Selection**: Choosing images with clear subjects and good composition usually leads to better results.
- **Prompt Tips**: In image-to-image mode, prompts should focus more on what you want to change or enhance, rather than describing all elements already present in the image.

## [​](http://docs.comfy.org#related-node-documentation) Related Node Documentation

You can refer to the documentation below for detailed parameter settings and more information about the corresponding nodes

[**Stability Stable Image Ultra Node Documentation**  
\
Stability Stable Image Ultra API Node Documentation](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-image-ultra)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/stability-ai/stable-image-ultra.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/black-forest-labs/flux-1-1-pro-ultra-image)

[Stable Diffusion 3.5 ImageThis article will introduce how to use Stability AI Stable Diffusion 3.5 API node's text-to-image and image-to-image capabilities in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-diffusion-3-5-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Stability AI Stable Image Ultra Text-to-Image Workflow](http://docs.comfy.org#stability-ai-stable-image-ultra-text-to-image-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download)
- [2. Complete the Workflow Execution Step by Step](http://docs.comfy.org#2-complete-the-workflow-execution-step-by-step)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)
- [Stability AI Stable Image Ultra Image-to-Image Workflow](http://docs.comfy.org#stability-ai-stable-image-ultra-image-to-image-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download-2)
- [2. Complete the Workflow Execution Step by Step](http://docs.comfy.org#2-complete-the-workflow-execution-step-by-step-2)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes-2)
- [Related Node Documentation](http://docs.comfy.org#related-node-documentation)