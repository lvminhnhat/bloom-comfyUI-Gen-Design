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

Models

# Models

## [​](http://docs.comfy.org#models-are-essential) Models are essential

Models are essential building blocks for media generation workflows. They can be combined and mixed to achieve different creative effects.

The word ***model*** has many different meanings. Here, it means a data file carrying information that is required for a node graph to do its work. Specifically, it’s a data structure that *models* some function. As a verb, to model something means to represent it or provide an example.

The primary example of a model data file in ComfyUI is an AI ***diffusion model***. This is a large set of data that represents the complex relationships among text strings and images, making it possible to translate words into pictures or vice versa. Other examples of common models used for image generation are language models such as CLIP, and upscaling models such as RealESRGAN.

## [​](http://docs.comfy.org#model-files) Model files

Model files are absolutely required for generative media production. Nothing can happen in a workflow if the model files are not found. Models are not included in the ComfyUI installation, but ComfyUI can often automatically download and install missing model files. Many models can be downloaded and installed from the **ComfyUI Manager** window. Models can also be found at websites such as [huggingface.co](https://huggingface.co), [civitai.green](https://civitai.green), and [github.com](https://github.com).

### [​](http://docs.comfy.org#using-models-in-comfyui) Using Models in ComfyUI

1. Download and place them in the ComfyUI program directory
   
   1. Within the **models** folder, you’ll find subfolders for various types of models, such as **checkpoints**
   2. The **ComfyUI Manager** helps to automate the process of searching, downloading, and installing
   3. Restart ComfyUI if it’s running
2. In your workflow, create the node appropriate to the model type, e.g. **Load Checkpoint**, **Load LoRA**, **Load VAE**
3. In the loader node, choose the model you wish to use
4. Connect the loader node to other nodes in your workflow

### [​](http://docs.comfy.org#file-size) File size

Models can be extremely large files relative to image files. A typical uncompressed image may require a few megabytes of disk storage. Generative AI models can be tens of thousands of times larger, up to tens of gigabytes per model. They take up a great deal of disk space and take a long time to transfer over a network.

## [​](http://docs.comfy.org#model-training-and-refinement) Model training and refinement

A generative AI model is created by training a machine learning program on a very large set of data, such as pairs of images and text descriptions. An AI model doesn’t store the training data explicitly, but rather it stores the correlations that are implicit within the data.

Organizations and companies such as Stability AI and Black Forest Labs release “base” models that carry large amounts of generic information. These are general purpose generative AI models. Commonly, the base models need to be ***refined*** in order to get high quality generative outputs. A dedicated community of people work to refine the base models. The new, refined models produce better output, provide new or different functionality, and/or use fewer resources. Refined models can usually be run on systems with less computing power and/or memory.

## [​](http://docs.comfy.org#auxiliary-models) Auxiliary models

Model functionality can be extended with auxiliary models. For example, art directing a text-to-image workflow to achieve a specific result may be difficult or impossible using a diffusion model alone. Additional models can refine a diffusion model within the workflow graph to produce desired results. Examples include **LoRA** (Low Rank Adaptation), a small model that is trained on a specific subject; **ControlNet**, a model that helps control composition using a guide image; and **Inpainting**, a model that allows certain diffusion models to generate new content within an existing image.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/core-concepts/models.mdx)

[Previous](http://docs.comfy.org/interface/maskeditor)

[DependenciesUnderstand dependencies in ComfyUI  
\
Next](http://docs.comfy.org/essentials/core-concepts/dependencies)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Models are essential](http://docs.comfy.org#models-are-essential)
- [Model files](http://docs.comfy.org#model-files)
- [Using Models in ComfyUI](http://docs.comfy.org#using-models-in-comfyui)
- [File size](http://docs.comfy.org#file-size)
- [Model training and refinement](http://docs.comfy.org#model-training-and-refinement)
- [Auxiliary models](http://docs.comfy.org#auxiliary-models)