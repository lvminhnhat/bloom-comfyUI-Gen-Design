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
  
  - [LTX-Video](http://docs.comfy.org/tutorials/video/ltxv)
  - [Hunyuan Video](http://docs.comfy.org/tutorials/video/hunyuan-video)
  - Wan Video
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

ComfyUI Hunyuan Video Examples

# ComfyUI Hunyuan Video Examples

This guide shows how to use Hunyuan Text-to-Video and Image-to-Video workflows in ComfyUI

Hunyuan Video series is developed and open-sourced by [Tencent](https://huggingface.co/tencent), featuring a hybrid architecture that supports both [Text-to-Video](https://github.com/Tencent/HunyuanVideo) and [Image-to-Video](https://github.com/Tencent/HunyuanVideo-I2V) generation with a parameter scale of 13B.

Technical features:

- **Core Architecture:** Uses a DiT (Diffusion Transformer) architecture similar to Sora, effectively fusing text, image, and motion information to improve consistency, quality, and alignment between generated video frames. A unified full-attention mechanism enables multi-view camera transitions while ensuring subject consistency.
- **3D VAE:** The custom 3D VAE compresses videos into a compact latent space, making image-to-video generation more efficient.
- **Superior Image-Video-Text Alignment:** Utilizing MLLM text encoders that excel in both image and video generation, better following text instructions, capturing details, and performing complex reasoning.

You can learn more through the official repositories: [Hunyuan Video](https://github.com/Tencent/HunyuanVideo) and [Hunyuan Video-I2V](https://github.com/Tencent/HunyuanVideo-I2V).

This guide will walk you through setting up both **Text-to-Video** and **Image-to-Video** workflows in ComfyUI.

The workflow images in this tutorial contain metadata with model download information.

Simply drag them into ComfyUI or use the menu `Workflows` -&gt; `Open (ctrl+o)` to load the corresponding workflow, which will prompt you to download the required models.

Alternatively, this guide provides direct model links if automatic downloads fail or you are not using the Desktop version. All models are available [here](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/tree/main/split_files) for download.

## [​](http://docs.comfy.org#shared-models-for-all-workflows) Shared Models for All Workflows

The following models are used in both Text-to-Video and Image-to-Video workflows. Please download and save them to the specified directories:

- [clip\_l.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/text_encoders/clip_l.safetensors?download=true)
- [llava\_llama3\_fp8\_scaled.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/text_encoders/llava_llama3_fp8_scaled.safetensors?download=true)
- [hunyuan\_video\_vae\_bf16.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/vae/hunyuan_video_vae_bf16.safetensors?download=true)

Storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors
│   │   └── llava_llama3_fp8_scaled.safetensors
│   ├── vae/
│   │   └── hunyuan_video_vae_bf16.safetensors
```

## [​](http://docs.comfy.org#hunyuan-text-to-video-workflow) Hunyuan Text-to-Video Workflow

Hunyuan Text-to-Video was open-sourced in December 2024, supporting 5-second short video generation through natural language descriptions in both Chinese and English.

### [​](http://docs.comfy.org#1-workflow) 1. Workflow

Download the image below and drag it into ComfyUI to load the workflow:

### [​](http://docs.comfy.org#2-manual-models-installation) 2. Manual Models Installation

Download [hunyuan\_video\_t2v\_720p\_bf16.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/diffusion_models/hunyuan_video_t2v_720p_bf16.safetensors?download=true) and save it to the `ComfyUI/models/diffusion_models` folder.

Ensure you have all these model files in the correct locations:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors                       // Shared model
│   │   └── llava_llama3_fp8_scaled.safetensors      // Shared model
│   ├── vae/
│   │   └── hunyuan_video_vae_bf16.safetensors       // Shared model
│   └── diffusion_models/
│       └── hunyuan_video_t2v_720p_bf16.safetensors  // T2V model
```

### [​](http://docs.comfy.org#3-steps-to-run-the-workflow) 3. Steps to Run the Workflow

1. Ensure the `DualCLIPLoader` node has loaded these models:
   
   - clip\_name1: clip\_l.safetensors
   - clip\_name2: llava\_llama3\_fp8\_scaled.safetensors
2. Ensure the `Load Diffusion Model` node has loaded `hunyuan_video_t2v_720p_bf16.safetensors`
3. Ensure the `Load VAE` node has loaded `hunyuan_video_vae_bf16.safetensors`
4. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

When the `length` parameter in the `EmptyHunyuanLatentVideo` node is set to 1, the model can generate a static image.

## [​](http://docs.comfy.org#hunyuan-image-to-video-workflow) Hunyuan Image-to-Video Workflow

Hunyuan Image-to-Video model was open-sourced on March 6, 2025, based on the HunyuanVideo framework. It transforms static images into smooth, high-quality videos and also provides LoRA training code to customize special video effects like hair growth, object transformation, etc.

Currently, the Hunyuan Image-to-Video model has two versions:

- v1 “concat”: Better motion fluidity but less adherence to the image guidance
- v2 “replace”: Updated the day after v1, with better image guidance but seemingly less dynamic compared to v1

v1 “concat”

v2 “replace”

### [​](http://docs.comfy.org#shared-model-for-v1-and-v2-versions) Shared Model for v1 and v2 Versions

Download the following file and save it to the `ComfyUI/models/clip_vision` directory:

- [llava\_llama3\_vision.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/clip_vision/llava_llama3_vision.safetensors?download=true)

### [​](http://docs.comfy.org#v1-%E2%80%9Cconcat%E2%80%9D-image-to-video-workflow) V1 “concat” Image-to-Video Workflow

#### [​](http://docs.comfy.org#1-workflow-and-asset) 1. Workflow and Asset

Download the workflow image below and drag it into ComfyUI to load the workflow:

Download the image below, which we’ll use as the starting frame for the image-to-video generation:

#### [​](http://docs.comfy.org#2-related-models-manual-installation) 2. Related models manual installation

- [hunyuan\_video\_image\_to\_video\_720p\_bf16.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/diffusion_models/hunyuan_video_image_to_video_720p_bf16.safetensors?download=true)

Ensure you have all these model files in the correct locations:

```plaintext
ComfyUI/
├── models/
│   ├── clip_vision/
│   │   └── llava_llama3_vision.safetensors                     // I2V shared model
│   ├── text_encoders/
│   │   ├── clip_l.safetensors                                  // Shared model
│   │   └── llava_llama3_fp8_scaled.safetensors                 // Shared model
│   ├── vae/
│   │   └── hunyuan_video_vae_bf16.safetensors                  // Shared model
│   └── diffusion_models/
│       └── hunyuan_video_image_to_video_720p_bf16.safetensors  // I2V v1 "concat" version model
```

#### [​](http://docs.comfy.org#3-steps-to-run-the-workflow-2) 3. Steps to Run the Workflow

1. Ensure that `DualCLIPLoader` has loaded these models:
   
   - clip\_name1: clip\_l.safetensors
   - clip\_name2: llava\_llama3\_fp8\_scaled.safetensors
2. Ensure that `Load CLIP Vision` has loaded `llava_llama3_vision.safetensors`
3. Ensure that `Load Image Model` has loaded `hunyuan_video_image_to_video_720p_bf16.safetensors`
4. Ensure that `Load VAE` has loaded `vae_name: hunyuan_video_vae_bf16.safetensors`
5. Ensure that `Load Diffusion Model` has loaded `hunyuan_video_image_to_video_720p_bf16.safetensors`
6. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

### [​](http://docs.comfy.org#v2-%E2%80%9Creplace%E2%80%9D-image-to-video-workflow) v2 “replace” Image-to-Video Workflow

The v2 workflow is essentially the same as the v1 workflow. You just need to download the **replace** model and use it in the `Load Diffusion Model` node.

#### [​](http://docs.comfy.org#1-workflow-and-asset-2) 1. Workflow and Asset

Download the workflow image below and drag it into ComfyUI to load the workflow:

Download the image below, which we’ll use as the starting frame for the image-to-video generation:

#### [​](http://docs.comfy.org#2-related-models-manual-installation-2) 2. Related models manual installation

- [hunyuan\_video\_v2\_replace\_image\_to\_video\_720p\_bf16.safetensors](https://huggingface.co/Comfy-Org/HunyuanVideo_repackaged/resolve/main/split_files/diffusion_models/hunyuan_video_v2_replace_image_to_video_720p_bf16.safetensors?download=true)

Ensure you have all these model files in the correct locations:

```plaintext
ComfyUI/
├── models/
│   ├── clip_vision/
│   │   └── llava_llama3_vision.safetensors                                // I2V shared model
│   ├── text_encoders/
│   │   ├── clip_l.safetensors                                             // Shared model
│   │   └── llava_llama3_fp8_scaled.safetensors                            // Shared model
│   ├── vae/
│   │   └── hunyuan_video_vae_bf16.safetensors                             // Shared model
│   └── diffusion_models/
│       └── hunyuan_video_v2_replace_image_to_video_720p_bf16.safetensors  // V2 "replace" version model
```

#### [​](http://docs.comfy.org#3-steps-to-run-the-workflow-3) 3. Steps to Run the Workflow

1. Ensure the `DualCLIPLoader` node has loaded these models:
   
   - clip\_name1: clip\_l.safetensors
   - clip\_name2: llava\_llama3\_fp8\_scaled.safetensors
2. Ensure the `Load CLIP Vision` node has loaded `llava_llama3_vision.safetensors`
3. Ensure the `Load Image Model` node has loaded `hunyuan_video_image_to_video_720p_bf16.safetensors`
4. Ensure the `Load VAE` node has loaded `hunyuan_video_vae_bf16.safetensors`
5. Ensure the `Load Diffusion Model` node has loaded `hunyuan_video_v2_replace_image_to_video_720p_bf16.safetensors`
6. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

## [​](http://docs.comfy.org#try-it-yourself) Try it yourself

Here are some images and prompts we provide. Based on that content or make an adjustment to create your own video.

```plaintext
Futuristic robot dancing ballet, dynamic motion, fast motion, fast shot, moving scene
```

* * *

```plaintext
Samurai waving sword and hitting the camera. camera angle movement, zoom in, fast scene, super fast, dynamic
```

* * *

```plaintext
flying car fastly moving and flying through the city
```

* * *

```plaintext
cyberpunk car race in night city, dynamic, super fast, fast shot
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/video/hunyuan-video.mdx)

[Previous](http://docs.comfy.org/tutorials/video/ltxv)

[Wan VideoThis guide demonstrates how to generate videos with first and last frames using Wan2.1 Video in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/video/wan/wan-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Shared Models for All Workflows](http://docs.comfy.org#shared-models-for-all-workflows)
- [Hunyuan Text-to-Video Workflow](http://docs.comfy.org#hunyuan-text-to-video-workflow)
- [1. Workflow](http://docs.comfy.org#1-workflow)
- [2. Manual Models Installation](http://docs.comfy.org#2-manual-models-installation)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow)
- [Hunyuan Image-to-Video Workflow](http://docs.comfy.org#hunyuan-image-to-video-workflow)
- [Shared Model for v1 and v2 Versions](http://docs.comfy.org#shared-model-for-v1-and-v2-versions)
- [V1 “concat” Image-to-Video Workflow](http://docs.comfy.org#v1-%E2%80%9Cconcat%E2%80%9D-image-to-video-workflow)
- [1. Workflow and Asset](http://docs.comfy.org#1-workflow-and-asset)
- [2. Related models manual installation](http://docs.comfy.org#2-related-models-manual-installation)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow-2)
- [v2 “replace” Image-to-Video Workflow](http://docs.comfy.org#v2-%E2%80%9Creplace%E2%80%9D-image-to-video-workflow)
- [1. Workflow and Asset](http://docs.comfy.org#1-workflow-and-asset-2)
- [2. Related models manual installation](http://docs.comfy.org#2-related-models-manual-installation-2)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow-3)
- [Try it yourself](http://docs.comfy.org#try-it-yourself)