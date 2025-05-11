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
  
  - [Flux.1 Text-to-Image](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image)
  - [Flux.1 fill dev](http://docs.comfy.org/tutorials/flux/flux-1-fill-dev)
  - [Flux.1 ControlNet](http://docs.comfy.org/tutorials/flux/flux-1-controlnet)
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

ComfyUI Flux.1 ControlNet Examples

# ComfyUI Flux.1 ControlNet Examples

This guide will demonstrate workflow examples using Flux.1 ControlNet.

## [​](http://docs.comfy.org#flux-1-controlnet-model-introduction) FLUX.1 ControlNet Model Introduction

FLUX.1 Canny and Depth are two powerful models from the [FLUX.1 Tools](https://blackforestlabs.ai/flux-1-tools/) launched by [Black Forest Labs](https://blackforestlabs.ai/). This toolkit is designed to add control and guidance capabilities to FLUX.1, enabling users to modify and recreate real or generated images.

**FLUX.1-Depth-dev** and **FLUX.1-Canny-dev** are both 12B parameter Rectified Flow Transformer models that can generate images based on text descriptions while maintaining the structural features of the input image. The Depth version maintains the spatial structure of the source image through depth map extraction techniques, while the Canny version uses edge detection techniques to preserve the structural features of the source image, allowing users to choose the appropriate control method based on different needs.

Both models have the following features:

- Top-tier output quality and detail representation
- Excellent prompt following ability while maintaining consistency with the original image
- Trained using guided distillation techniques for improved efficiency
- Open weights for the research community
- API interfaces (pro version) and open-source weights (dev version)

Additionally, Black Forest Labs also provides **FLUX.1-Depth-dev-lora** and **FLUX.1-Canny-dev-lora** adapter versions extracted from the complete models. These can be applied to the FLUX.1 \[dev] base model to provide similar functionality with smaller file size, especially suitable for resource-constrained environments.

We will use the full version of **FLUX.1-Canny-dev** and **FLUX.1-Depth-dev-lora** to complete the workflow examples.

All workflow images’s Metadata contains the corresponding model download information. You can load the workflows by:

- Dragging them directly into ComfyUI
- Or using the menu `Workflows` -&gt; `Open（ctrl+o）`

If you’re not using the Desktop Version or some models can’t be downloaded automatically, please refer to the manual installation sections to save the model files to the corresponding folder.

For image preprocessors, you can use the following custom nodes to complete image preprocessing. In this example, we will provide processed images as input.

- [ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet)
- [ComfyUI ControlNet aux](https://github.com/Fannovel16/comfyui_controlnet_aux)

## [​](http://docs.comfy.org#flux-1-canny-dev-complete-version-workflow) FLUX.1-Canny-dev Complete Version Workflow

### [​](http://docs.comfy.org#1-workflow-and-asset) 1. Workflow and Asset

Please download the workflow image below and drag it into ComfyUI to load the workflow

Please download the image below, which we will use as the input image

### [​](http://docs.comfy.org#2-manual-models-installation) 2. Manual Models Installation

If you have previously used the [complete version of Flux related workflows](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image), then you only need to download the **flux1-canny-dev.safetensors** model file. Since you need to first agree to the terms of [black-forest-labs/FLUX.1-Canny-dev](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev), please visit the [black-forest-labs/FLUX.1-Canny-dev](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev) page and make sure you have agreed to the corresponding terms as shown in the image below.

Complete model list:

- [clip\_l.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/clip_l.safetensors?download=true)
- [t5xxl\_fp16.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp16.safetensors?download=true)
- [ae.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/ae.safetensors?download=true)
- [flux1-canny-dev.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev/resolve/main/flux1-canny-dev.safetensors?download=true) (Please ensure you have agreed to the corresponding repo’s terms)

File storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors
│   │   └── t5xxl_fp16.safetensors
│   ├── vae/
│   │   └── ae.safetensors
│   └── diffusion_models/
│       └── flux1-canny-dev.safetensors
```

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution) 3. Step-by-Step Workflow Execution

1. Make sure `ae.safetensors` is loaded in the `Load VAE` node
2. Make sure `flux1-canny-dev.safetensors` is loaded in the `Load Diffusion Model` node
3. Make sure the following models are loaded in the `DualCLIPLoader` node:
   
   - clip\_name1: t5xxl\_fp16.safetensors
   - clip\_name2: clip\_l.safetensors
4. Upload the provided input image in the `Load Image` node
5. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

### [​](http://docs.comfy.org#4-start-your-experimentation) 4. Start Your Experimentation

Try using the [FLUX.1-Depth-dev](https://huggingface.co/black-forest-labs/FLUX.1-Depth-dev) model to complete the Depth version of the workflow

You can use the image below as input

Or use the following custom nodes to complete image preprocessing:

- [ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet)
- [ComfyUI ControlNet aux](https://github.com/Fannovel16/comfyui_controlnet_aux)

## [​](http://docs.comfy.org#flux-1-depth-dev-lora-workflow) FLUX.1-Depth-dev-lora Workflow

The LoRA version workflow builds on the complete version by adding the LoRA model. Compared to the [complete version of the Flux workflow](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image), it adds nodes for loading and using the corresponding LoRA model.

### [​](http://docs.comfy.org#1-workflow-and-asset-2) 1. Workflow and Asset

Please download the workflow image below and drag it into ComfyUI to load the workflow

Please download the image below, which we will use as the input image

### [​](http://docs.comfy.org#2-manual-model-download) 2. Manual Model Download

If you have previously used the [complete version of Flux related workflows](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image), then you only need to download the **flux1-depth-dev-lora.safetensors** model file.

Complete model list:

- [clip\_l.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/clip_l.safetensors?download=true)
- [t5xxl\_fp16.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp16.safetensors?download=true)
- [ae.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/ae.safetensors?download=true)
- [flux1-dev.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-dev/resolve/main/flux1-dev.safetensors?download=true)
- [flux1-depth-dev-lora.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-Depth-dev-lora/resolve/main/flux1-depth-dev-lora.safetensors?download=true)

File storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors
│   │   └── t5xxl_fp16.safetensors
│   ├── vae/
│   │   └── ae.safetensors
│   ├── diffusion_models/
│   │   └── flux1-dev.safetensors
│   └── loras/
│       └── flux1-depth-dev-lora.safetensors
```

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution-2) 3. Step-by-Step Workflow Execution

1. Make sure `flux1-dev.safetensors` is loaded in the `Load Diffusion Model` node
2. Make sure `flux1-depth-dev-lora.safetensors` is loaded in the `LoraLoaderModelOnly` node
3. Make sure the following models are loaded in the `DualCLIPLoader` node:
   
   - clip\_name1: t5xxl\_fp16.safetensors
   - clip\_name2: clip\_l.safetensors
4. Upload the provided input image in the `Load Image` node
5. Make sure `ae.safetensors` is loaded in the `Load VAE` node
6. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

### [​](http://docs.comfy.org#4-start-your-experimentation-2) 4. Start Your Experimentation

Try using the [FLUX.1-Canny-dev-lora](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev-lora) model to complete the Canny version of the workflow

Use [ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet) or [ComfyUI ControlNet aux](https://github.com/Fannovel16/comfyui_controlnet_aux) to complete image preprocessing

## [​](http://docs.comfy.org#community-versions-of-flux-controlnets) Community Versions of Flux Controlnets

XLab and InstantX + Shakker Labs have released Controlnets for Flux.

**InstantX:**

- [FLUX.1-dev-Controlnet-Canny](https://huggingface.co/InstantX/FLUX.1-dev-Controlnet-Canny/blob/main/diffusion_pytorch_model.safetensors)
- [FLUX.1-dev-ControlNet-Depth](https://huggingface.co/Shakker-Labs/FLUX.1-dev-ControlNet-Depth/blob/main/diffusion_pytorch_model.safetensors)
- [FLUX.1-dev-ControlNet-Union-Pro](https://huggingface.co/Shakker-Labs/FLUX.1-dev-ControlNet-Union-Pro/blob/main/diffusion_pytorch_model.safetensors)

**XLab**: [flux-controlnet-collections](https://huggingface.co/XLabs-AI/flux-controlnet-collections)

Place these files in the `ComfyUI/models/controlnet` directory.

You can visit [Flux Controlnet Example](https://raw.githubusercontent.com/comfyanonymous/ComfyUI_examples/refs/heads/master/flux/flux_controlnet_example.png) to get the corresponding workflow image, and use the image from [here](https://raw.githubusercontent.com/comfyanonymous/ComfyUI_examples/refs/heads/master/flux/girl_in_field.png) as the input image.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/flux/flux-1-controlnet.mdx)

[Previous](http://docs.comfy.org/tutorials/flux/flux-1-fill-dev)

[HiDream-I1This guide will walk you through completing a ComfyUI native HiDream-I1 text-to-image workflow example  
\
Next](http://docs.comfy.org/tutorials/image/hidream/hidream-i1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [FLUX.1 ControlNet Model Introduction](http://docs.comfy.org#flux-1-controlnet-model-introduction)
- [FLUX.1-Canny-dev Complete Version Workflow](http://docs.comfy.org#flux-1-canny-dev-complete-version-workflow)
- [1. Workflow and Asset](http://docs.comfy.org#1-workflow-and-asset)
- [2. Manual Models Installation](http://docs.comfy.org#2-manual-models-installation)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution)
- [4. Start Your Experimentation](http://docs.comfy.org#4-start-your-experimentation)
- [FLUX.1-Depth-dev-lora Workflow](http://docs.comfy.org#flux-1-depth-dev-lora-workflow)
- [1. Workflow and Asset](http://docs.comfy.org#1-workflow-and-asset-2)
- [2. Manual Model Download](http://docs.comfy.org#2-manual-model-download)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution-2)
- [4. Start Your Experimentation](http://docs.comfy.org#4-start-your-experimentation-2)
- [Community Versions of Flux Controlnets](http://docs.comfy.org#community-versions-of-flux-controlnets)