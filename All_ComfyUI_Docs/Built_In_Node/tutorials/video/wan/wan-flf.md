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

ComfyUI Wan2.1 FLF2V Native Example

# ComfyUI Wan2.1 FLF2V Native Example

This guide explains how to complete Wan2.1 FLF2V video generation examples in ComfyUI

Wan FLF2V (First-Last Frame Video Generation) is an open-source video generation model developed by the Alibaba Tongyi Wanxiang team. Its open-source license is [Apache 2.0](https://github.com/Wan-Video/Wan2.1?tab=Apache-2.0-1-ov-file). Users only need to provide two images as the starting and ending frames, and the model automatically generates intermediate transition frames, outputting a logically coherent and naturally flowing 720p high-definition video.

**Core Technical Highlights**

1. **Precise First-Last Frame Control**: The matching rate of first and last frames reaches 98%, defining video boundaries through starting and ending scenes, intelligently filling intermediate dynamic changes to achieve scene transitions and object morphing effects.
2. **Stable and Smooth Video Generation**: Using CLIP semantic features and cross-attention mechanisms, the video jitter rate is reduced by 37% compared to similar models, ensuring natural and smooth transitions.
3. **Multi-functional Creative Capabilities**: Supports dynamic embedding of Chinese and English subtitles, generation of anime/realistic/fantasy and other styles, adapting to different creative needs.
4. **720p HD Output**: Directly generates 1280×720 resolution videos without post-processing, suitable for social media and commercial applications.
5. **Open-source Ecosystem Support**: Model weights, code, and training framework are fully open-sourced, supporting deployment on mainstream AI platforms.

**Technical Principles and Architecture**

1. **DiT Architecture**: Based on diffusion models and Diffusion Transformer architecture, combined with Full Attention mechanism to optimize spatiotemporal dependency modeling, ensuring video coherence.
2. **3D Causal Variational Encoder**: Wan-VAE technology compresses HD frames to 1/128 size while retaining subtle dynamic details, significantly reducing memory requirements.
3. **Three-stage Training Strategy**: Starting from 480P resolution pre-training, gradually upgrading to 720P, balancing generation quality and computational efficiency through phased optimization.

**Related Links**

- **GitHub Repository**: [GitHub](https://github.com/Wan-Video/Wan2.1)
- **Hugging Face Model Page**: [Hugging Face](https://huggingface.co/Wan-AI/Wan2.1-FLF2V-14B-720P)
- **ModelScope Community**: [ModelScope](https://www.modelscope.cn/models/Wan-AI/Wan2.1-FLF2V-14B-720P)

## [​](http://docs.comfy.org#wan2-1-flf2v-720p-comfyui-native-workflow-example) Wan2.1 FLF2V 720P ComfyUI Native Workflow Example

### [​](http://docs.comfy.org#1-download-workflow-files-and-related-input-files) 1. Download Workflow Files and Related Input Files

Since this model is trained on high-resolution images, using smaller sizes may not yield good results. In the example, we use a size of 720 * 1280, which may cause users with lower VRAM hard to run smoothly and will take a long time to generate. If needed, please modify the video generation size at the beginning.

Please download the WebP file below, and drag it into ComfyUI to load the corresponding workflow. The workflow has embedded the corresponding model download file information.

Please download the two images below, which we will use as the starting and ending frames of the video

### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

If corresponding

All models involved in this guide can be found [here](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/tree/main/split_files).

**diffusion\_models** Choose one version based on your hardware conditions

- FP16:[wan2.1\_flf2v\_720p\_14B\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/diffusion_models/wan2.1_flf2v_720p_14B_fp16.safetensors?download=true)
- FP8:[wan2.1\_flf2v\_720p\_14B\_fp8\_e4m3fn.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/blob/main/split_files/diffusion_models/wan2.1_flf2v_720p_14B_fp8_e4m3fn.safetensors)

If you have previously tried Wan Video related workflows, you may already have the following files.

Choose one version from **Text encoders** for download,

- [umt5\_xxl\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp16.safetensors?download=true)
- [umt5\_xxl\_fp8\_e4m3fn\_scaled.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp8_e4m3fn_scaled.safetensors?download=true)

**VAE**

- [wan\_2.1\_vae.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/vae/wan_2.1_vae.safetensors?download=true)

**CLIP Vision**

- [clip\_vision\_h.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/clip_vision/clip_vision_h.safetensors?download=true)

File Storage Location

```plaintext
ComfyUI/
├── models/
│   ├── diffusion_models/
│   │   └─── wan2.1_flf2v_720p_14B_fp16.safetensors           # or FP8 version
│   ├── text_encoders/
│   │   └─── umt5_xxl_fp8_e4m3fn_scaled.safetensors           # or your chosen version
│   ├── vae/
│   │   └──  wan_2.1_vae.safetensors
│   └── clip_vision/
│       └──  clip_vision_h.safetensors   
```

### [​](http://docs.comfy.org#3-complete-workflow-execution-step-by-step) 3. Complete Workflow Execution Step by Step

1. Ensure the `Load Diffusion Model` node has loaded `wan2.1_flf2v_720p_14B_fp16.safetensors` or `wan2.1_flf2v_720p_14B_fp8_e4m3fn.safetensors`
2. Ensure the `Load CLIP` node has loaded `umt5_xxl_fp8_e4m3fn_scaled.safetensors`
3. Ensure the `Load VAE` node has loaded `wan_2.1_vae.safetensors`
4. Ensure the `Load CLIP Vision` node has loaded `clip_vision_h.safetensors`
5. Upload the starting frame to the `Start_image` node
6. Upload the ending frame to the `End_image` node
7. (Optional) Modify the positive and negative prompts, both Chinese and English are supported
8. (**Important**) In `WanFirstLastFrameToVideo`, modify the corresponding video size. We default to using a size of 720 * 1280 to achieve better results for the generated video, but this may cause issues running smoothly on lower memory. You can initially try adjusting it to a size such as 480 * 854 to ensure smooth operation, and then adjust it back to 720 * 1280 when you need to generate larger-sized videos to ensure quality results.
9. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute video generation

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/video/wan/wan-flf.mdx)

[Previous](http://docs.comfy.org/tutorials/video/wan/fun-inp)

[ACE-Step Music GenerationThis guide will help you create dynamic music using the ACE-Step model in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/audio/ace-step/ace-step-v1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Wan2.1 FLF2V 720P ComfyUI Native Workflow Example](http://docs.comfy.org#wan2-1-flf2v-720p-comfyui-native-workflow-example)
- [1. Download Workflow Files and Related Input Files](http://docs.comfy.org#1-download-workflow-files-and-related-input-files)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Complete Workflow Execution Step by Step](http://docs.comfy.org#3-complete-workflow-execution-step-by-step)