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

ComfyUI Inpainting Workflow

# ComfyUI Inpainting Workflow

This guide will introduce you to the inpainting workflow in ComfyUI, walk you through an inpainting example, and cover topics like using the mask editor

This article will introduce the concept of inpainting in AI image generation and guide you through creating an inpainting workflow in ComfyUI. We’ll cover:

- Using inpainting workflows to modify images
- Using the ComfyUI mask editor to draw masks
- `VAE Encoder (for Inpainting)` node

## [​](http://docs.comfy.org#about-inpainting) About Inpainting

In AI image generation, we often encounter situations where we’re satisfied with the overall image but there are elements we don’t want or that contain errors. Simply regenerating might produce a completely different image, so using inpainting to fix specific parts becomes very useful.

It’s like having an **artist (AI model)** paint a picture, but we’re still not satisfied with the specific details. We need to tell the artist **which areas to adjust (mask)**, and then let them **repaint (inpaint)** according to our requirements.

Common inpainting scenarios include:

- **Defect Repair:** Removing unwanted objects, fixing incorrect AI-generated body parts, etc.
- **Detail Optimization:** Precisely adjusting local elements (like modifying clothing textures, adjusting facial expressions)
- And other scenarios

## [​](http://docs.comfy.org#comfyui-inpainting-workflow-example) ComfyUI Inpainting Workflow Example

### [​](http://docs.comfy.org#model-and-resource-preparation) Model and Resource Preparation

#### [​](http://docs.comfy.org#1-model-installation) 1. Model Installation

Download the [512-inpainting-ema.safetensors](https://huggingface.co/stabilityai/stable-diffusion-2-inpainting/blob/main/512-inpainting-ema.safetensors) file and put it in your `ComfyUI/models/checkpoints` folder:

#### [​](http://docs.comfy.org#2-inpainting-asset) 2. Inpainting Asset

Please download the following image which we’ll use as input:

This image already contains an alpha channel (transparency mask), so you don’t need to manually draw a mask. This tutorial will also cover how to use the mask editor to draw masks.

#### [​](http://docs.comfy.org#3-inpainting-workflow) 3. Inpainting Workflow

Download the image below and **drag it into ComfyUI** to load the workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

### [​](http://docs.comfy.org#comfyui-inpainting-workflow-example-explanation) ComfyUI Inpainting Workflow Example Explanation

Follow the steps in the diagram below to ensure the workflow runs correctly.

1. Ensure `Load Checkpoint` loads `512-inpainting-ema.safetensors`
2. Upload the input image to the `Load Image` node
3. Click `Queue` or use `Ctrl + Enter` to generate

For comparison, here’s the result using the [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) model:

You will find that the results generated by the [512-inpainting-ema.safetensors](https://huggingface.co/stabilityai/stable-diffusion-2-inpainting/blob/main/512-inpainting-ema.safetensors) model have better inpainting effects and more natural transitions. This is because this model is specifically designed for inpainting, which helps us better control the generation area, resulting in improved inpainting effects.

Do you remember the analogy we’ve been using? Different models are like artists with varying abilities, but each artist has their own limits. Choosing the right model can help you achieve better generation results.

You can try these approaches to achieve better results:

1. Modify positive and negative prompts with more specific descriptions
2. Try multiple runs using different seeds in the `KSampler` for different generation results
3. After learning about the mask editor in this tutorial, you can re-inpaint the generated results to achieve satisfactory outcomes.

Next, we’ll learn about using the **Mask Editor**. While our input image already includes an `alpha` transparency channel (the area we want to edit), so manual mask drawing isn’t necessary, you’ll often use the Mask Editor to create masks in practical applications.

### [​](http://docs.comfy.org#using-the-mask-editor) Using the Mask Editor

First right-click the `Save Image` node and select `Copy(Clipspace)`:

Then right-click the **Load Image** node and select `Paste(Clipspace)`:

Right-click the **Load Image** node again and select `Open in MaskEditor`:

1. Adjust brush parameters on the right panel
2. Use eraser to correct mistakes
3. Click `Save` when finished

The drawn content will be used as a Mask input to the VAE Encoder (for Inpainting) node for encoding

Then try adjusting your prompts and generating again until you achieve satisfactory results.

## [​](http://docs.comfy.org#vae-encoder-for-inpainting-node) VAE Encoder (for Inpainting) Node

Comparing this workflow with [Text-to-Image](http://docs.comfy.org/tutorials/basic/text-to-image) and [Image-to-Image](http://docs.comfy.org/tutorials/basic/image-to-image), you’ll notice the main differences are in the VAE section’s conditional inputs. In this workflow, we use the **VAE Encoder (for Inpainting)** node, specifically designed for inpainting to help us better control the generation area and achieve better results.

**Input Types**

Parameter NameFunction`pixels`Input image to be encoded into latent space.`vae`VAE model used to encode the image from pixel space to latent space.`mask`Image mask specifying which areas need modification.`grow_mask_by`Pixel value to expand the original mask outward, ensuring a transition area around the mask to avoid hard edges between inpainted and original areas.

**Output Types**

Parameter NameFunction`latent`Image encoded into latent space by the VAE.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/inpaint.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/image-to-image)

[OutpaintThis guide will introduce you to the outpainting workflow in ComfyUI and walk you through an outpainting example  
\
Next](http://docs.comfy.org/tutorials/basic/outpaint)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [About Inpainting](http://docs.comfy.org#about-inpainting)
- [ComfyUI Inpainting Workflow Example](http://docs.comfy.org#comfyui-inpainting-workflow-example)
- [Model and Resource Preparation](http://docs.comfy.org#model-and-resource-preparation)
- [1. Model Installation](http://docs.comfy.org#1-model-installation)
- [2. Inpainting Asset](http://docs.comfy.org#2-inpainting-asset)
- [3. Inpainting Workflow](http://docs.comfy.org#3-inpainting-workflow)
- [ComfyUI Inpainting Workflow Example Explanation](http://docs.comfy.org#comfyui-inpainting-workflow-example-explanation)
- [Using the Mask Editor](http://docs.comfy.org#using-the-mask-editor)
- [VAE Encoder (for Inpainting) Node](http://docs.comfy.org#vae-encoder-for-inpainting-node)