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
    
    - [Wan Video](http://docs.comfy.org/tutorials/video/wan/wan-video)
    - [Wan2.1 Fun Control](http://docs.comfy.org/tutorials/video/wan/fun-control)
    - [Wan2.1 Fun InP](http://docs.comfy.org/tutorials/video/wan/fun-inp)
    - [First-Last Frame](http://docs.comfy.org/tutorials/video/wan/wan-flf)
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

ComfyUI Wan2.1 Video Examples

# ComfyUI Wan2.1 Video Examples

This guide demonstrates how to generate videos with first and last frames using Wan2.1 Video in ComfyUI

Wan2.1 Video series is a video generation model open-sourced by Alibaba in February 2025 under the [Apache 2.0 license](https://github.com/Wan-Video/Wan2.1?tab=Apache-2.0-1-ov-file). It offers two versions:

- 14B (14 billion parameters)
- 1.3B (1.3 billion parameters) Covering multiple tasks including text-to-video (T2V) and image-to-video (I2V). The model not only outperforms existing open-source models in performance but more importantly, its lightweight version requires only 8GB of VRAM to run, significantly lowering the barrier to entry.

<!--THE END-->

- [Wan2.1 Code Repository](https://github.com/Wan-Video/Wan2.1)
- [Wan2.1 Model Repository](https://huggingface.co/Wan-AI)

## [​](http://docs.comfy.org#wan2-1-comfyui-native-workflow-examples) Wan2.1 ComfyUI Native Workflow Examples

Please update ComfyUI to the latest version before starting the examples to make sure you have native Wan Video support.

## [​](http://docs.comfy.org#model-installation) Model Installation

All models mentioned in this guide can be found [here](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/tree/main/split_files). Below are the common models you’ll need for the examples in this guide, which you can download in advance:

Choose one version from **Text encoders** to download:

- [umt5\_xxl\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp16.safetensors?download=true)
- [umt5\_xxl\_fp8\_e4m3fn\_scaled.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp8_e4m3fn_scaled.safetensors?download=true)

**VAE**

- [wan\_2.1\_vae.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/vae/wan_2.1_vae.safetensors?download=true)

**CLIP Vision**

- [clip\_vision\_h.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/clip_vision/clip_vision_h.safetensors?download=true)

File storage locations:

```plaintext
ComfyUI/
├── models/
│   ├── diffusion_models/
│   ├── ...                  # Let's download the models in the corresponding workflow
│   ├── text_encoders/
│   │   └─── umt5_xxl_fp8_e4m3fn_scaled.safetensors
│   └── vae/
│   │   └──  wan_2.1_vae.safetensors
│   └── clip_vision/
│       └──  clip_vision_h.safetensors   
```

For diffusion models, we’ll use the fp16 precision models in this guide because we’ve found that they perform better than the bf16 versions. If you need other precision versions, please visit [here](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/tree/main/split_files/diffusion_models) to download them.

## [​](http://docs.comfy.org#wan2-1-text-to-video-workflow) Wan2.1 Text-to-Video Workflow

Before starting the workflow, please download [wan2.1\_t2v\_1.3B\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/diffusion_models/wan2.1_t2v_1.3B_fp16.safetensors?download=true) and save it to the `ComfyUI/models/diffusion_models/` directory.

> If you need other t2v precision versions, please visit [here](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/tree/main/split_files/diffusion_models) to download them.

### [​](http://docs.comfy.org#1-workflow-file-download) 1. Workflow File Download

Download the file below and drag it into ComfyUI to load the corresponding workflow:

### [​](http://docs.comfy.org#2-complete-the-workflow-step-by-step) 2. Complete the Workflow Step by Step

1. Make sure the `Load Diffusion Model` node has loaded the `wan2.1_t2v_1.3B_fp16.safetensors` model
2. Make sure the `Load CLIP` node has loaded the `umt5_xxl_fp8_e4m3fn_scaled.safetensors` model
3. Make sure the `Load VAE` node has loaded the `wan_2.1_vae.safetensors` model
4. (Optional) You can modify the video dimensions in the `EmptyHunyuanLatentVideo` node if needed
5. (Optional) If you need to modify the prompts (positive and negative), make changes in the `CLIP Text Encoder` node at number `5`
6. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the video generation

## [​](http://docs.comfy.org#wan2-1-image-to-video-workflow) Wan2.1 Image-to-Video Workflow

**Since Wan Video separates the 480P and 720P models**, we’ll need to provide examples for both resolutions in this guide. In addition to using different models, they also have slight parameter differences.

### [​](http://docs.comfy.org#480p-version) 480P Version

#### [​](http://docs.comfy.org#1-workflow-and-input-image) 1. Workflow and Input Image

Download the image below and drag it into ComfyUI to load the corresponding workflow:

We’ll use the following image as input:

#### [​](http://docs.comfy.org#2-model-download) 2. Model Download

Please download [wan2.1\_i2v\_480p\_14B\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/diffusion_models/wan2.1_i2v_480p_14B_fp16.safetensors?download=true) and save it to the `ComfyUI/models/diffusion_models/` directory.

#### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step) 3. Complete the Workflow Step by Step

1. Make sure the `Load Diffusion Model` node has loaded the `wan2.1_i2v_480p_14B_fp16.safetensors` model
2. Make sure the `Load CLIP` node has loaded the `umt5_xxl_fp8_e4m3fn_scaled.safetensors` model
3. Make sure the `Load VAE` node has loaded the `wan_2.1_vae.safetensors` model
4. Make sure the `Load CLIP Vision` node has loaded the `clip_vision_h.safetensors` model
5. Upload the provided input image in the `Load Image` node
6. (Optional) Enter the video description content you want to generate in the `CLIP Text Encoder` node
7. (Optional) You can modify the video dimensions in the `WanImageToVideo` node if needed
8. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the video generation

### [​](http://docs.comfy.org#720p-version) 720P Version

#### [​](http://docs.comfy.org#1-workflow-and-input-image-2) 1. Workflow and Input Image

Download the image below and drag it into ComfyUI to load the corresponding workflow:

We’ll use the following image as input:

#### [​](http://docs.comfy.org#2-model-download-2) 2. Model Download

Please download [wan2.1\_i2v\_720p\_14B\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/diffusion_models/wan2.1_i2v_720p_14B_fp16.safetensors?download=true) and save it to the `ComfyUI/models/diffusion_models/` directory.

#### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step-2) 3. Complete the Workflow Step by Step

1. Make sure the `Load Diffusion Model` node has loaded the `wan2.1_i2v_720p_14B_fp16.safetensors` model
2. Make sure the `Load CLIP` node has loaded the `umt5_xxl_fp8_e4m3fn_scaled.safetensors` model
3. Make sure the `Load VAE` node has loaded the `wan_2.1_vae.safetensors` model
4. Make sure the `Load CLIP Vision` node has loaded the `clip_vision_h.safetensors` model
5. Upload the provided input image in the `Load Image` node
6. (Optional) Enter the video description content you want to generate in the `CLIP Text Encoder` node
7. (Optional) You can modify the video dimensions in the `WanImageToVideo` node if needed
8. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute the video generation

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/video/wan/wan-video.mdx)

[Previous](http://docs.comfy.org/tutorials/video/hunyuan-video)

[Wan2.1 Fun ControlThis guide demonstrates how to use Wan2.1 Fun Control in ComfyUI to generate videos with control videos  
\
Next](http://docs.comfy.org/tutorials/video/wan/fun-control)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Wan2.1 ComfyUI Native Workflow Examples](http://docs.comfy.org#wan2-1-comfyui-native-workflow-examples)
- [Model Installation](http://docs.comfy.org#model-installation)
- [Wan2.1 Text-to-Video Workflow](http://docs.comfy.org#wan2-1-text-to-video-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download)
- [2. Complete the Workflow Step by Step](http://docs.comfy.org#2-complete-the-workflow-step-by-step)
- [Wan2.1 Image-to-Video Workflow](http://docs.comfy.org#wan2-1-image-to-video-workflow)
- [480P Version](http://docs.comfy.org#480p-version)
- [1. Workflow and Input Image](http://docs.comfy.org#1-workflow-and-input-image)
- [2. Model Download](http://docs.comfy.org#2-model-download)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step)
- [720P Version](http://docs.comfy.org#720p-version)
- [1. Workflow and Input Image](http://docs.comfy.org#1-workflow-and-input-image-2)
- [2. Model Download](http://docs.comfy.org#2-model-download-2)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step-2)