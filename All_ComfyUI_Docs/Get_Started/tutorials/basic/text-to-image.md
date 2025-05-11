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

ComfyUI Text to Image Workflow

# ComfyUI Text to Image Workflow

This guide will help you understand the concept of text-to-image in AI art generation and complete a text-to-image workflow in ComfyUI

This guide aims to introduce you to ComfyUI’s text-to-image workflow and help you understand the functionality and usage of various ComfyUI nodes.

In this document, we will:

- Complete a text-to-image workflow
- Gain a basic understanding of diffusion model principles
- Learn about the functions and roles of workflow nodes
- Get an initial understanding of the SD1.5 model

We’ll start by running a text-to-image workflow, followed by explanations of related concepts. Please choose the relevant sections based on your needs.

## [​](http://docs.comfy.org#about-text-to-image) About Text to Image

**Text to Image** is a fundamental process in AI art generation that creates images from text descriptions, with **diffusion models** at its core.

The text-to-image process requires the following elements:

- **Artist:** The image generation model
- **Canvas:** The latent space
- **Image Requirements (Prompts):** Including positive prompts (elements you want in the image) and negative prompts (elements you don’t want)

This text-to-image generation process can be simply understood as telling your requirements (positive and negative prompts) to an **artist (the image model)**, who then creates what you want based on these requirements.

## [​](http://docs.comfy.org#comfyui-text-to-image-workflow-example-guide) ComfyUI Text to Image Workflow Example Guide

### [​](http://docs.comfy.org#1-preparation) 1. Preparation

Ensure you have at least one SD1.5 model file in your `ComfyUI/models/checkpoints` folder, such as [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors)

If you haven’t installed it yet, please refer to the model installation section in [Getting Started with ComfyUI AI Art Generation](http://docs.comfy.org/get_started/first_generation).

### [​](http://docs.comfy.org#2-loading-the-text-to-image-workflow) 2. Loading the Text to Image Workflow

Download the image below and **drag it into ComfyUI** to load the workflow:

Images containing workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`.

### [​](http://docs.comfy.org#3-loading-the-model-and-generating-your-first-image) 3. Loading the Model and Generating Your First Image

After installing the image model, follow the steps in the image below to load the model and generate your first image

Follow these steps according to the image numbers:

1. In the **Load Checkpoint** node, use the arrows or click the text area to ensure **v1-5-pruned-emaonly-fp16.safetensors** is selected, and the left/right arrows don’t show **null** text
2. Click the `Queue` button or use the shortcut `Ctrl + Enter` to execute image generation

After the process completes, you should see the resulting image in the **Save Image** node interface, which you can right-click to save locally

If you’re not satisfied with the result, try running the generation multiple times. Each time you run it, **KSampler** will use a different random seed based on the `seed` parameter, so each generation will produce different results

### [​](http://docs.comfy.org#4-start-experimenting) 4. Start Experimenting

Try modifying the text in the **CLIP Text Encoder**

The `Positive` connection to the KSampler node represents positive prompts, while the `Negative` connection represents negative prompts

Here are some basic prompting principles for the SD1.5 model:

- Use English whenever possible
- Separate prompts with English commas `,`
- Use phrases rather than long sentences
- Use specific descriptions
- Use expressions like `(golden hour:1.2)` to increase the weight of specific keywords, making them more likely to appear in the image. `1.2` is the weight, `golden hour` is the keyword
- Use keywords like `masterpiece, best quality, 4k` to improve generation quality

Here are several prompt examples you can try, or use your own prompts for generation:

**1. Anime Style**

Positive prompts:

```plaintext
anime style, 1girl with long pink hair, cherry blossom background, studio ghibli aesthetic, soft lighting, intricate details

masterpiece, best quality, 4k
```

Negative prompts:

```plaintext
low quality, blurry, deformed hands, extra fingers
```

**2. Realistic Style**

Positive prompts:

```plaintext
(ultra realistic portrait:1.3), (elegant woman in crimson silk dress:1.2), 
full body, soft cinematic lighting, (golden hour:1.2), 
(fujifilm XT4:1.1), shallow depth of field, 
(skin texture details:1.3), (film grain:1.1), 
gentle wind flow, warm color grading, (perfect facial symmetry:1.3)
```

Negative prompts:

```plaintext
(deformed, cartoon, anime, doll, plastic skin, overexposed, blurry, extra fingers)
```

**3. Specific Artist Style**

Positive prompts:

```plaintext
fantasy elf, detailed character, glowing magic, vibrant colors, long flowing hair, elegant armor, ethereal beauty, mystical forest, magical aura, high detail, soft lighting, fantasy portrait, Artgerm style
```

Negative prompts:

```plaintext
blurry, low detail, cartoonish, unrealistic anatomy, out of focus, cluttered, flat lighting
```

## [​](http://docs.comfy.org#text-to-image-working-principles) Text to Image Working Principles

The entire text-to-image process can be understood as a **reverse diffusion process**. The [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) we downloaded is a pre-trained model that can **generate target images from pure Gaussian noise**. We only need to input our prompts, and it can generate target images through denoising random noise.

We need to understand two concepts:

1. **Latent Space:** Latent Space is an abstract data representation method in diffusion models. Converting images from pixel space to latent space reduces storage space and makes it easier to train diffusion models and reduce denoising complexity. It’s like architects using blueprints (latent space) for design rather than designing directly on the building (pixel space), maintaining structural features while significantly reducing modification costs
2. **Pixel Space:** Pixel Space is the storage space for images, which is the final image we see, used to store pixel values.

If you want to learn more about diffusion models, you can read these papers:

- [Denoising Diffusion Probabilistic Models (DDPM)](https://arxiv.org/pdf/2006.11239)
- [Denoising Diffusion Implicit Models (DDIM)](https://arxiv.org/pdf/2010.02502)
- [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/pdf/2112.10752)

## [​](http://docs.comfy.org#comfyui-text-to-image-workflow-node-explanation) ComfyUI Text to Image Workflow Node Explanation

### [​](http://docs.comfy.org#a-load-checkpoint-node) A. Load Checkpoint Node

This node is typically used to load the image generation model. A `checkpoint` usually contains three components: `MODEL (UNet)`, `CLIP`, and `VAE`

- `MODEL (UNet)`: The UNet model responsible for noise prediction and image generation during the diffusion process
- `CLIP`: The text encoder that converts our text prompts into vectors that the model can understand, as the model cannot directly understand text prompts
- `VAE`: The Variational AutoEncoder that converts images between pixel space and latent space, as diffusion models work in latent space while our images are in pixel space

### [​](http://docs.comfy.org#b-empty-latent-image-node) B. Empty Latent Image Node

Defines a latent space that outputs to the KSampler node. The Empty Latent Image node constructs a **pure noise latent space**

You can think of its function as defining the canvas size, which determines the dimensions of our final generated image

### [​](http://docs.comfy.org#c-clip-text-encoder-node) C. CLIP Text Encoder Node

Used to encode prompts, which are your requirements for the image

- The `Positive` condition input connected to the KSampler node represents positive prompts (elements you want in the image)
- The `Negative` condition input connected to the KSampler node represents negative prompts (elements you don’t want in the image)

The prompts are encoded into semantic vectors by the `CLIP` component from the `Load Checkpoint` node and output as conditions to the KSampler node

### [​](http://docs.comfy.org#d-ksampler-node) D. KSampler Node

The **KSampler** is the core of the entire workflow, where the entire noise denoising process occurs, ultimately outputting a latent space image

Here’s an explanation of the KSampler node parameters:

Parameter NameDescriptionFunction**model**Diffusion model used for denoisingDetermines the style and quality of generated images**positive**Positive prompt condition encodingGuides generation to include specified elements**negative**Negative prompt condition encodingSuppresses unwanted content**latent\_image**Latent space image to be denoisedServes as the input carrier for noise initialization**seed**Random seed for noise generationControls generation randomness**control\_after\_generate**Seed control mode after generationDetermines seed variation pattern in batch generation**steps**Number of denoising iterationsMore steps mean finer details but longer processing time**cfg**Classifier-free guidance scaleControls prompt constraint strength (too high leads to overfitting)**sampler\_name**Sampling algorithm nameDetermines the mathematical method for denoising path**scheduler**Scheduler typeControls noise decay rate and step size allocation**denoise**Denoising strength coefficientControls noise strength added to latent space, 0.0 preserves original input features, 1.0 is complete noise

In the KSampler node, the latent space uses `seed` as an initialization parameter to construct random noise, and semantic vectors `Positive` and `Negative` are input as conditions to the diffusion model

Then, based on the number of denoising steps specified by the `steps` parameter, denoising is performed. Each denoising step uses the denoising strength coefficient specified by the `denoise` parameter to denoise the latent space and generate a new latent space image

### [​](http://docs.comfy.org#e-vae-decode-node) E. VAE Decode Node

Converts the latent space image output from the **KSampler** into a pixel space image

### [​](http://docs.comfy.org#f-save-image-node) F. Save Image Node

Previews and saves the decoded image from latent space to the local `ComfyUI/output` folder

## [​](http://docs.comfy.org#introduction-to-sd1-5-model) Introduction to SD1.5 Model

**SD1.5 (Stable Diffusion 1.5)** is an AI image generation model developed by [Stability AI](https://stability.ai/). It’s the foundational version of the Stable Diffusion series, trained on **512×512** resolution images, making it particularly good at generating images at this resolution. With a size of about 4GB, it runs smoothly on **consumer-grade GPUs (e.g., 6GB VRAM)**. Currently, SD1.5 has a rich ecosystem, supporting various plugins (like ControlNet, LoRA) and optimization tools. As a milestone model in AI art generation, SD1.5 remains the best entry-level choice thanks to its open-source nature, lightweight architecture, and rich ecosystem. Although newer versions like SDXL/SD3 have been released, its value for consumer-grade hardware remains unmatched.

### [​](http://docs.comfy.org#basic-information) Basic Information

- **Release Date**: October 2022
- **Core Architecture**: Based on Latent Diffusion Model (LDM)
- **Training Data**: LAION-Aesthetics v2.5 dataset (approximately 590M training steps)
- **Open Source Features**: Fully open-source model/code/training data

### [​](http://docs.comfy.org#advantages-and-limitations) Advantages and Limitations

Model Advantages:

- Lightweight: Small size, only about 4GB, runs smoothly on consumer GPUs
- Low Entry Barrier: Supports a wide range of plugins and optimization tools
- Mature Ecosystem: Extensive plugin and tool support
- Fast Generation: Smooth operation on consumer GPUs

Model Limitations:

- Detail Handling: Hands/complex lighting prone to distortion
- Resolution Limits: Quality degrades for direct 1024x1024 generation
- Prompt Dependency: Requires precise English descriptions for control

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/basic/text-to-image.mdx)

[Previous](http://docs.comfy.org/interface/shortcuts)

[Image to ImageThis guide will help you understand and complete an image to image workflow  
\
Next](http://docs.comfy.org/tutorials/basic/image-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [About Text to Image](http://docs.comfy.org#about-text-to-image)
- [ComfyUI Text to Image Workflow Example Guide](http://docs.comfy.org#comfyui-text-to-image-workflow-example-guide)
- [1. Preparation](http://docs.comfy.org#1-preparation)
- [2. Loading the Text to Image Workflow](http://docs.comfy.org#2-loading-the-text-to-image-workflow)
- [3. Loading the Model and Generating Your First Image](http://docs.comfy.org#3-loading-the-model-and-generating-your-first-image)
- [4. Start Experimenting](http://docs.comfy.org#4-start-experimenting)
- [Text to Image Working Principles](http://docs.comfy.org#text-to-image-working-principles)
- [ComfyUI Text to Image Workflow Node Explanation](http://docs.comfy.org#comfyui-text-to-image-workflow-node-explanation)
- [A. Load Checkpoint Node](http://docs.comfy.org#a-load-checkpoint-node)
- [B. Empty Latent Image Node](http://docs.comfy.org#b-empty-latent-image-node)
- [C. CLIP Text Encoder Node](http://docs.comfy.org#c-clip-text-encoder-node)
- [D. KSampler Node](http://docs.comfy.org#d-ksampler-node)
- [E. VAE Decode Node](http://docs.comfy.org#e-vae-decode-node)
- [F. Save Image Node](http://docs.comfy.org#f-save-image-node)
- [Introduction to SD1.5 Model](http://docs.comfy.org#introduction-to-sd1-5-model)
- [Basic Information](http://docs.comfy.org#basic-information)
- [Advantages and Limitations](http://docs.comfy.org#advantages-and-limitations)