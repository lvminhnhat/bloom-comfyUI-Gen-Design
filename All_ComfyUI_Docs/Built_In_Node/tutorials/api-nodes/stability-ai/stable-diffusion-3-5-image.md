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

Stability AI Stable Diffusion 3.5 API Node ComfyUI Official Example

# Stability AI Stable Diffusion 3.5 API Node ComfyUI Official Example

This article will introduce how to use Stability AI Stable Diffusion 3.5 API node’s text-to-image and image-to-image capabilities in ComfyUI

The [Stability AI Stable Diffusion 3.5 Image](http://docs.comfy.org/zh-CN/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-diffusion-3-5-image) node allows you to use Stability AI’s Stable Diffusion 3.5 model to create high-quality, detail-rich image content through text prompts or reference images.

In this guide, we will show you how to set up workflows for both text-to-image and image-to-image generation using this node.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#stability-ai-stable-diffusion-3-5-text-to-image-workflow) Stability AI Stable Diffusion 3.5 Text-to-Image Workflow

### [​](http://docs.comfy.org#1-workflow-file-download) 1. Workflow File Download

The image below contains workflow information in its `metadata`. Please download and drag it into ComfyUI to load the corresponding workflow.

### [​](http://docs.comfy.org#2-complete-the-workflow-step-by-step) 2. Complete the Workflow Step by Step

You can follow the numbered steps in the image to complete the basic text-to-image workflow:

1. (Optional) Modify the `prompt` parameter in the `Stability AI Stable Diffusion 3.5 Image` node to input your desired image description. More detailed prompts often result in better image quality.
2. (Optional) Select the `model` parameter to choose which SD 3.5 model version to use.
3. (Optional) Select the `style_preset` parameter to control the visual style of the image. Different presets produce images with different stylistic characteristics, such as “cinematic” or “anime”. Select “None” to not apply any specific style.
4. (Optional) Edit the `String(Multiline)` to modify negative prompts, specifying elements you don’t want to appear in the generated image.
5. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation.
6. After the API returns results, you can view the generated image in the `Save Image` node. The image will also be saved to the `ComfyUI/output/` directory.

### [​](http://docs.comfy.org#3-additional-notes) 3. Additional Notes

- **Prompt**: The prompt is one of the most important parameters in the generation process. Detailed, clear descriptions lead to better results. Can include elements like scene, subject, colors, lighting, and style.
- **CFG Scale**: Controls how closely the generator follows the prompt. Higher values make the image more closely match the prompt description, but too high may result in oversaturated or unnatural results.
- **Style Preset**: Offers various preset styles for quickly defining the overall style of the image.
- **Negative Prompt**: Used to specify elements you don’t want to appear in the generated image.
- **Seed Parameter**: Can be used to reproduce or fine-tune generation results, helpful for iteration during creation.
- Currently the `Load Image` node is in “Bypass” mode. To enable it, refer to the step guide and right-click the node to set “Mode” to “Always” to enable input, switching to image-to-image mode.
- `image_denoise` has no effect when there is no input image.

## [​](http://docs.comfy.org#stability-ai-stable-diffusion-3-5-image-to-image-workflow) Stability AI Stable Diffusion 3.5 Image-to-Image Workflow

### [​](http://docs.comfy.org#1-workflow-file-download-2) 1. Workflow File Download

The image below contains workflow information in its `metadata`. Please download and drag it into ComfyUI to load the corresponding workflow.

Download the image below to use as input !\[Stability AI Stable Diffusion 3.5 Image-to-Image Workflow Input Image](

### [​](http://docs.comfy.org#2-complete-the-workflow-step-by-step-2) 2. Complete the Workflow Step by Step

You can follow the numbered steps in the image to complete the image-to-image workflow:

1. Load a reference image through the `Load Image` node, which will serve as the basis for generation.
2. (Optional) Modify the `prompt` parameter in the `Stability AI Stable Diffusion 3.5 Image` node to describe elements you want to change or enhance in the reference image.
3. (Optional) Select the `style_preset` parameter to control the visual style of the image. Different presets produce images with different stylistic characteristics.
4. (Optional|Important) Adjust the `image_denoise` parameter (range 0.0-1.0) to control how much the original image is modified:
   
   - Values closer to 0.0 make the generated image more similar to the input reference image (at 0.0, it’s basically identical to the original)
   - Values closer to 1.0 make the generated image more like pure text-to-image generation (at 1.0, it’s as if no reference image was provided)
5. (Optional) Edit the `String(Multiline)` to modify negative prompts, specifying elements you don’t want to appear in the generated image.
6. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation.
7. After the API returns results, you can view the generated image in the `Save Image` node. The image will also be saved to the `ComfyUI/output/` directory.

### [​](http://docs.comfy.org#3-additional-notes-2) 3. Additional Notes

The image below shows a comparison of results with and without input image using the same parameter settings:

**Image Denoise**: This parameter determines how much of the original image’s features are preserved during generation. It’s the most crucial adjustment parameter in image-to-image mode. The image below shows the effects of different denoising strengths:

- **Reference Image Selection**: Choosing images with clear subjects and good composition usually yields better results.
- **Prompt Tips**: In image-to-image mode, prompts should focus more on elements you want to change or enhance, rather than describing everything already present in the image.
- **Mode Switching**: When an input image is provided, the node automatically switches from text-to-image mode to image-to-image mode, and aspect ratio parameters are ignored.

## [​](http://docs.comfy.org#related-node-details) Related Node Details

You can refer to the documentation below to understand detailed parameter settings for the corresponding node

[**Stability Stable Diffusion 3.5 Image Node Documentation**  
\
Stability Stable Diffusion 3.5 Image API Node Documentation](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-diffusion-3-5-image)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/stability-ai/stable-diffusion-3-5-image.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-image-ultra)

[Ideogram 3.0This guide covers how to use the Ideogram 3.0 API node in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/ideogram/ideogram-v3)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Stability AI Stable Diffusion 3.5 Text-to-Image Workflow](http://docs.comfy.org#stability-ai-stable-diffusion-3-5-text-to-image-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download)
- [2. Complete the Workflow Step by Step](http://docs.comfy.org#2-complete-the-workflow-step-by-step)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes)
- [Stability AI Stable Diffusion 3.5 Image-to-Image Workflow](http://docs.comfy.org#stability-ai-stable-diffusion-3-5-image-to-image-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download-2)
- [2. Complete the Workflow Step by Step](http://docs.comfy.org#2-complete-the-workflow-step-by-step-2)
- [3. Additional Notes](http://docs.comfy.org#3-additional-notes-2)
- [Related Node Details](http://docs.comfy.org#related-node-details)