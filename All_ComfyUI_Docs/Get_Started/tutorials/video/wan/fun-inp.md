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

ComfyUI Wan2.1 Fun InP Video Examples

# ComfyUI Wan2.1 Fun InP Video Examples

This guide demonstrates how to use Wan2.1 Fun InP in ComfyUI to generate videos with first and last frame control

## [​](http://docs.comfy.org#about-wan2-1-fun-inp) About Wan2.1-Fun-InP

**Wan-Fun InP** is an open-source video generation model released by Alibaba, part of the Wan2.1-Fun series, focusing on generating videos from images with first and last frame control.

**Key features**:

- **First and last frame control**: Supports inputting both first and last frame images to generate transitional video between them, enhancing video coherence and creative freedom. Compared to earlier community versions, Alibaba’s official model produces more stable and significantly higher quality results.
- **Multi-resolution support**: Supports generating videos at 512×512, 768×768, 1024×1024 and other resolutions to accommodate different scenario requirements.

**Model versions**:

- **1.3B** Lightweight: Suitable for local deployment and quick inference with **lower VRAM requirements**
- **14B** High-performance: Model size reaches 32GB+, offering better results but requiring **higher VRAM**

Below are the relevant model weights and code repositories:

- [Wan2.1-Fun-1.3B-Input](https://huggingface.co/alibaba-pai/Wan2.1-Fun-1.3B-Input)
- [Wan2.1-Fun-14B-Input](https://huggingface.co/alibaba-pai/Wan2.1-Fun-14B-Input)
- Code repository: [VideoX-Fun](https://github.com/aigc-apps/VideoX-Fun)

Currently, ComfyUI natively supports the Wan2.1 Fun InP model. Before starting this tutorial, please update your ComfyUI to ensure your version is after [this commit](https://github.com/comfyanonymous/ComfyUI/commit/0a1f8869c9998bbfcfeb2e97aa96a6d3e0a2b5df).

## [​](http://docs.comfy.org#wan2-1-fun-inp-workflow) Wan2.1 Fun InP Workflow

Download the image below and drag it into ComfyUI to load the workflow:

### [​](http://docs.comfy.org#1-workflow-file-download) 1. Workflow File Download

### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

If automatic model downloading is ineffective, please download the models manually and save them to the corresponding folders.

The following models can be found at [Wan\_2.1\_ComfyUI\_repackaged](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged) and [Wan2.1-Fun](https://huggingface.co/collections/alibaba-pai/wan21-fun-67e4fb3b76ca01241eb7e334)

**Diffusion models** - choose 1.3B or 14B. The 14B version has a larger file size (32GB) and higher VRAM requirements:

- [wan2.1\_fun\_inp\_1.3B\_bf16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/diffusion_models/wan2.1_fun_inp_1.3B_bf16.safetensors?download=true)
- [Wan2.1-Fun-14B-InP](https://huggingface.co/alibaba-pai/Wan2.1-Fun-14B-InP/resolve/main/diffusion_pytorch_model.safetensors?download=true): Rename to `Wan2.1-Fun-14B-InP.safetensors` after downloading

**Text encoders** - choose one of the following models (fp16 precision has a larger size and higher performance requirements):

- [umt5\_xxl\_fp16.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp16.safetensors?download=true)
- [umt5\_xxl\_fp8\_e4m3fn\_scaled.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/text_encoders/umt5_xxl_fp8_e4m3fn_scaled.safetensors?download=true)

**VAE**

- [wan\_2.1\_vae.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/vae/wan_2.1_vae.safetensors?download=true)

**CLIP Vision**

- [clip\_vision\_h.safetensors](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/main/split_files/clip_vision/clip_vision_h.safetensors?download=true)

File storage location:

```plaintext
📂 ComfyUI/
├── 📂 models/
│   ├── 📂 diffusion_models/
│   │   └── wan2.1_fun_inp_1.3B_bf16.safetensors
│   ├── 📂 text_encoders/
│   │   └─── umt5_xxl_fp8_e4m3fn_scaled.safetensors
│   └── 📂 vae/
│   │   └── wan_2.1_vae.safetensors
│   └── 📂 clip_vision/
│       └──  clip_vision_h.safetensors                 
```

### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step) 3. Complete the Workflow Step by Step

1. Ensure the `Load Diffusion Model` node has loaded `wan2.1_fun_inp_1.3B_bf16.safetensors`
2. Ensure the `Load CLIP` node has loaded `umt5_xxl_fp8_e4m3fn_scaled.safetensors`
3. Ensure the `Load VAE` node has loaded `wan_2.1_vae.safetensors`
4. Ensure the `Load CLIP Vision` node has loaded `clip_vision_h.safetensors`
5. Upload the starting frame to the `Load Image` node (renamed to `Start_image`)
6. Upload the ending frame to the second `Load Image` node
7. (Optional) Modify the prompt (both English and Chinese are supported)
8. (Optional) Adjust the video size in `WanFunInpaintToVideo`, avoiding overly large dimensions
9. Click the `Run` button or use the shortcut `Ctrl(cmd) + Enter` to execute video generation

### [​](http://docs.comfy.org#4-workflow-notes) 4. Workflow Notes

Please make sure to use the correct model, as `wan2.1_fun_inp_1.3B_bf16.safetensors` and `wan2.1_fun_control_1.3B_bf16.safetensors` are stored in the same folder and have very similar names. Ensure you’re using the right model.

- When using Wan Fun InP, you may need to frequently modify prompts to ensure the accuracy of the corresponding scene transitions.

## [​](http://docs.comfy.org#other-wan2-1-fun-inp-or-video-related-custom-node-packages) Other Wan2.1 Fun InP or video-related custom node packages

- [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
- [ComfyUI-WanVideoWrapper](https://github.com/kijai/ComfyUI-WanVideoWrapper)
- [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/video/wan/fun-inp.mdx)

[Previous](http://docs.comfy.org/tutorials/video/wan/fun-control)

[First-Last FrameThis guide explains how to complete Wan2.1 FLF2V video generation examples in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/video/wan/wan-flf)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [About Wan2.1-Fun-InP](http://docs.comfy.org#about-wan2-1-fun-inp)
- [Wan2.1 Fun InP Workflow](http://docs.comfy.org#wan2-1-fun-inp-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step)
- [4. Workflow Notes](http://docs.comfy.org#4-workflow-notes)
- [Other Wan2.1 Fun InP or video-related custom node packages](http://docs.comfy.org#other-wan2-1-fun-inp-or-video-related-custom-node-packages)