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
  
  - [Hunyuan3D-2](http://docs.comfy.org/tutorials/3d/hunyuan3D-2)
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

ComfyUI Hunyuan3D-2 Examples

# ComfyUI Hunyuan3D-2 Examples

This guide will demonstrate how to use Hunyuan3D-2 in ComfyUI to generate 3D assets.

# [​](http://docs.comfy.org#hunyuan3d-2-0-introduction) Hunyuan3D 2.0 Introduction

[Hunyuan3D 2.0](https://github.com/Tencent/Hunyuan3D-2) is an open-source 3D asset generation model released by Tencent, capable of generating high-fidelity 3D models with high-resolution texture maps through text or images.

Hunyuan3D 2.0 adopts a two-stage generation approach, first generating a geometry model without textures, then synthesizing high-resolution texture maps. This effectively separates the complexity of shape and texture generation. Below are the two core components of Hunyuan3D 2.0:

1. **Geometry Generation Model (Hunyuan3D-DiT)**: Based on a flow diffusion Transformer architecture, it generates untextured geometric models that precisely match input conditions.
2. **Texture Generation Model (Hunyuan3D-Paint)**: Combines geometric conditions and multi-view diffusion techniques to add high-resolution textures to models, supporting PBR materials.

**Key Advantages**

- **High-Precision Generation**: Sharp geometric structures, rich texture colors, support for PBR material generation, achieving near-realistic lighting effects.
- **Diverse Usage Methods**: Provides code calls, Blender plugins, Gradio applications, and online experience through the official website, suitable for different user needs.
- **Lightweight and Compatibility**: The Hunyuan3D-2mini model requires only 5GB VRAM, the standard version needs 6GB VRAM for shape generation, and the complete process (shape + texture) requires only 12GB VRAM.

Recently (March 18, 2025), Hunyuan3D 2.0 also introduced a multi-view shape generation model (Hunyuan3D-2mv), which supports generating more detailed geometric structures from inputs at different angles.

This example includes three workflows:

- Using Hunyuan3D-2mv with multiple view inputs to generate 3D models
- Using Hunyuan3D-2mv-turbo with multiple view inputs to generate 3D models
- Using Hunyuan3D-2 with a single view input to generate 3D models

ComfyUI now natively supports Hunyuan3D-2mv, but does not yet support texture and material generation. Please make sure you have updated to the latest version of [ComfyUI](https://github.com/comfyanonymous/ComfyUI) before starting.

The workflow example PNG images in this tutorial contain workflow JSON in their metadata:

- You can drag them directly into ComfyUI
- Or use the menu `Workflows` -&gt; `Open (ctrl+o)`

This will load the corresponding workflow and prompt you to download the required models. The generated `.glb` format models will be output to the `ComfyUI/output/mesh` folder.

## [​](http://docs.comfy.org#comfyui-hunyuan3d-2mv-workflow-example) ComfyUI Hunyuan3D-2mv Workflow Example

In the Hunyuan3D-2mv workflow, we’ll use multi-view images to generate a 3D model. Note that multiple view images are not mandatory in this workflow - you can use only the `front` view image to generate a 3D model.

### [​](http://docs.comfy.org#1-workflow) 1. Workflow

Please download the images below and drag into ComfyUI to load the workflow.

Download the images below we will use them as input images.

In this example, the input images have already been preprocessed to remove excess background. In actual use, you can use custom nodes like [ComfyUI\_essentials](https://github.com/cubiq/ComfyUI_essentials) to automatically remove excess background.

### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

Download the model below and save it to the corresponding ComfyUI folder

- hunyuan3d-dit-v2-mv: [model.fp16.safetensors](https://huggingface.co/tencent/Hunyuan3D-2mv/resolve/main/hunyuan3d-dit-v2-mv/model.fp16.safetensors?download=true) - after downloading, you can rename it to `hunyuan3d-dit-v2-mv.safetensors`

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── hunyuan3d-dit-v2-mv.safetensors  // renamed file
```

### [​](http://docs.comfy.org#3-steps-to-run-the-workflow) 3. Steps to Run the Workflow

1. Ensure that the Image Only Checkpoint Loader(img2vid model) has loaded our downloaded and renamed `hunyuan3d-dit-v2-mv.safetensors` model
2. Load the corresponding view images in each of the `Load Image` nodes
3. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

If you need to add more views, make sure to load other view images in the `Hunyuan3Dv2ConditioningMultiView` node, and ensure that you load the corresponding view images in the `Load Image` nodes.

## [​](http://docs.comfy.org#hunyuan3d-2mv-turbo-workflow) Hunyuan3D-2mv-turbo Workflow

In the Hunyuan3D-2mv-turbo workflow, we’ll use the Hunyuan3D-2mv-turbo model to generate 3D models. This model is a step distillation version of Hunyuan3D-2mv, allowing for faster 3D model generation. In this version of the workflow, we set `cfg` to 1.0 and add a `flux guidance` node to control the `distilled cfg` generation.

### [​](http://docs.comfy.org#1-workflow-2) 1. Workflow

Please download the images below and drag into ComfyUI to load the workflow.

Download the images below we will use them as input images.

### [​](http://docs.comfy.org#2-manual-model-installation-2) 2. Manual Model Installation

Download the model below and save it to the corresponding ComfyUI folder

- hunyuan3d-dit-v2-mv-turbo: [model.fp16.safetensors](https://huggingface.co/tencent/Hunyuan3D-2mv/resolve/main/hunyuan3d-dit-v2-mv-turbo/model.fp16.safetensors?download=true) - after downloading, you can rename it to `hunyuan3d-dit-v2-mv-turbo.safetensors`

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── hunyuan3d-dit-v2-mv-turbo.safetensors  // renamed file
```

### [​](http://docs.comfy.org#3-steps-to-run-the-workflow-2) 3. Steps to Run the Workflow

1. Ensure that the `Image Only Checkpoint Loader(img2vid model)` node has loaded our renamed `hunyuan3d-dit-v2-mv-turbo.safetensors` model
2. Load the corresponding view images in each of the `Load Image` nodes
3. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

## [​](http://docs.comfy.org#hunyuan3d-2-single-view-workflow) Hunyuan3D-2 Single View Workflow

In the Hunyuan3D-2 workflow, we’ll use the Hunyuan3D-2 model to generate 3D models. This model is not a multi-view model. In this workflow, we use the `Hunyuan3Dv2Conditioning` node instead of the `Hunyuan3Dv2ConditioningMultiView` node.

### [​](http://docs.comfy.org#1-workflow-3) 1. Workflow

Please download the image below and drag it into ComfyUI to load the workflow.

Download the image below we will use it as input image.

### [​](http://docs.comfy.org#2-manual-model-installation-3) 2. Manual Model Installation

Download the model below and save it to the corresponding ComfyUI folder

- hunyuan3d-dit-v2-0: [model.fp16.safetensors](https://huggingface.co/tencent/Hunyuan3D-2/resolve/main/hunyuan3d-dit-v2-0/model.fp16.safetensors?download=true) - after downloading, you can rename it to `hunyuan3d-dit-v2.safetensors`

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── hunyuan3d-dit-v2.safetensors  // renamed file
```

### [​](http://docs.comfy.org#3-steps-to-run-the-workflow-3) 3. Steps to Run the Workflow

1. Ensure that the `Image Only Checkpoint Loader(img2vid model)` node has loaded our renamed `hunyuan3d-dit-v2.safetensors` model
2. Load the image in the `Load Image` node
3. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

## [​](http://docs.comfy.org#community-resources) Community Resources

Below are ComfyUI community resources related to Hunyuan3D-2

- [ComfyUI-Hunyuan3DWrapper](https://github.com/kijai/ComfyUI-Hunyuan3DWrapper)
- [Kijai/Hunyuan3D-2\_safetensors](https://huggingface.co/Kijai/Hunyuan3D-2_safetensors/tree/main)
- [ComfyUI-3D-Pack](https://github.com/MrForExample/ComfyUI-3D-Pack)

## [​](http://docs.comfy.org#hunyuan3d-2-0-open-source-model-series) Hunyuan3D 2.0 Open-Source Model Series

Currently, Hunyuan3D 2.0 has open-sourced multiple models covering the complete 3D generation process. You can visit [Hunyuan3D-2](https://github.com/Tencent/Hunyuan3D-2) for more information.

**Hunyuan3D-2mini Series**

ModelDescriptionDateParametersHuggingfaceHunyuan3D-DiT-v2-miniMini Image to Shape Model2025-03-180.6B[Visit](https://huggingface.co/tencent/Hunyuan3D-2mini/tree/main/hunyuan3d-dit-v2-mini)

**Hunyuan3D-2mv Series**

ModelDescriptionDateParametersHuggingfaceHunyuan3D-DiT-v2-mv-FastGuidance Distillation Version, can halve DIT inference time2025-03-181.1B[Visit](https://huggingface.co/tencent/Hunyuan3D-2mv/tree/main/hunyuan3d-dit-v2-mv-fast)Hunyuan3D-DiT-v2-mvMulti-view Image to Shape Model, suitable for 3D creation requiring multiple angles to understand the scene2025-03-181.1B[Visit](https://huggingface.co/tencent/Hunyuan3D-2mv/tree/main/hunyuan3d-dit-v2-mv)

**Hunyuan3D-2 Series**

ModelDescriptionDateParametersHuggingfaceHunyuan3D-DiT-v2-0-FastGuidance Distillation Model2025-02-031.1B[Visit](https://huggingface.co/tencent/Hunyuan3D-2/tree/main/hunyuan3d-dit-v2-0-fast)Hunyuan3D-DiT-v2-0Image to Shape Model2025-01-211.1B[Visit](https://huggingface.co/tencent/Hunyuan3D-2/tree/main/hunyuan3d-dit-v2-0)Hunyuan3D-Paint-v2-0Texture Generation Model2025-01-211.3B[Visit](https://huggingface.co/tencent/Hunyuan3D-2/tree/main/hunyuan3d-paint-v2-0)Hunyuan3D-Delight-v2-0Image Delight Model2025-01-211.3B[Visit](https://huggingface.co/tencent/Hunyuan3D-2/tree/main/hunyuan3d-delight-v2-0)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/3d/hunyuan3D-2.mdx)

[Previous](http://docs.comfy.org/tutorials/image/hidream/hidream-e1)

[LTX-Video  
\
Next](http://docs.comfy.org/tutorials/video/ltxv)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Hunyuan3D 2.0 Introduction](http://docs.comfy.org#hunyuan3d-2-0-introduction)
- [ComfyUI Hunyuan3D-2mv Workflow Example](http://docs.comfy.org#comfyui-hunyuan3d-2mv-workflow-example)
- [1. Workflow](http://docs.comfy.org#1-workflow)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow)
- [Hunyuan3D-2mv-turbo Workflow](http://docs.comfy.org#hunyuan3d-2mv-turbo-workflow)
- [1. Workflow](http://docs.comfy.org#1-workflow-2)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation-2)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow-2)
- [Hunyuan3D-2 Single View Workflow](http://docs.comfy.org#hunyuan3d-2-single-view-workflow)
- [1. Workflow](http://docs.comfy.org#1-workflow-3)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation-3)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow-3)
- [Community Resources](http://docs.comfy.org#community-resources)
- [Hunyuan3D 2.0 Open-Source Model Series](http://docs.comfy.org#hunyuan3d-2-0-open-source-model-series)