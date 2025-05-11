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

ComfyUI Image to Image Workflow

# ComfyUI Image to Image Workflow

This guide will help you understand and complete an image to image workflow

## [​](http://docs.comfy.org#what-is-image-to-image) What is Image to Image

Image to Image is a workflow in ComfyUI that allows users to input an image and generate a new image based on it.

Image to Image can be used in scenarios such as:

- Converting original image styles, like transforming realistic photos into artistic styles
- Converting line art into realistic images
- Image restoration
- Colorizing old photos
- … and other scenarios

To explain it with an analogy: It’s like asking an artist to create a specific piece based on your reference image.

If you carefully compare this tutorial with the [Text to Image](http://docs.comfy.org/tutorials/basic/text-to-image) tutorial, you’ll notice that the Image to Image process is very similar to Text to Image, just with an additional input reference image as a condition. In Text to Image, we let the artist (image model) create freely based on our prompts, while in Image to Image, we let the artist create based on both our reference image and prompts.

## [​](http://docs.comfy.org#comfyui-image-to-image-workflow-example-guide) ComfyUI Image to Image Workflow Example Guide

### [​](http://docs.comfy.org#model-installation) Model Installation

Download the [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) file and put it in your `ComfyUI/models/checkpoints` folder.

### [​](http://docs.comfy.org#image-to-image-workflow-and-input-image) Image to Image Workflow and Input Image

Download the image below and **drag it into ComfyUI** to load the workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

Download the image below and we will use it as the input image:

### [​](http://docs.comfy.org#complete-the-workflow-step-by-step) Complete the Workflow Step by Step

Follow the steps in the diagram below to ensure the workflow runs correctly.

1. Ensure `Load Checkpoint` loads **v1-5-pruned-emaonly-fp16.safetensors**
2. Upload the input image to the `Load Image` node
3. Click `Queue` or press `Ctrl/Cmd + Enter` to generate

## [​](http://docs.comfy.org#key-points-of-image-to-image-workflow) Key Points of Image to Image Workflow

The key to the Image to Image workflow lies in the `denoise` parameter in the `KSampler` node, which should be **less than 1**

If you’ve adjusted the `denoise` parameter and generated images, you’ll notice:

- The smaller the `denoise` value, the smaller the difference between the generated image and the reference image
- The larger the `denoise` value, the larger the difference between the generated image and the reference image

This is because `denoise` determines the strength of noise added to the latent space image after converting the reference image. If `denoise` is 1, the latent space image will become completely random noise, making it the same as the latent space generated by the `empty latent image` node, losing all characteristics of the reference image.

For the corresponding principles, please refer to the principle explanation in the [Text to Image](http://docs.comfy.org/tutorials/basic/text-to-image) tutorial.

## [​](http://docs.comfy.org#try-it-yourself) Try It Yourself

1. Try modifying the `denoise` parameter in the **KSampler** node, gradually changing it from 1 to 0, and observe the changes in the generated images
2. Replace with your own prompts and reference images to generate your own image effects

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/image-to-image.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/text-to-image)

[InpaintThis guide will introduce you to the inpainting workflow in ComfyUI, walk you through an inpainting example, and cover topics like using the mask editor  
\
Next](http://docs.comfy.org/tutorials/basic/inpaint)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [What is Image to Image](http://docs.comfy.org#what-is-image-to-image)
- [ComfyUI Image to Image Workflow Example Guide](http://docs.comfy.org#comfyui-image-to-image-workflow-example-guide)
- [Model Installation](http://docs.comfy.org#model-installation)
- [Image to Image Workflow and Input Image](http://docs.comfy.org#image-to-image-workflow-and-input-image)
- [Complete the Workflow Step by Step](http://docs.comfy.org#complete-the-workflow-step-by-step)
- [Key Points of Image to Image Workflow](http://docs.comfy.org#key-points-of-image-to-image-workflow)
- [Try It Yourself](http://docs.comfy.org#try-it-yourself)