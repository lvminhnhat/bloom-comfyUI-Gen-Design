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
  
  - HiDream
    
    - [HiDream-I1](http://docs.comfy.org/tutorials/image/hidream/hidream-i1)
    - [HiDream-e1](http://docs.comfy.org/tutorials/image/hidream/hidream-e1)
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

ComfyUI Native HiDream-I1 Text-to-Image Workflow Example

# ComfyUI Native HiDream-I1 Text-to-Image Workflow Example

This guide will walk you through completing a ComfyUI native HiDream-I1 text-to-image workflow example

HiDream-I1 is a text-to-image model officially open-sourced by HiDream-ai on April 7, 2025. The model has 17B parameters and is released under the [MIT license](https://github.com/HiDream-ai/HiDream-I1/blob/main/LICENSE), supporting personal projects, scientific research, and commercial use. It currently performs excellently in multiple benchmark tests.

## [​](http://docs.comfy.org#model-features) Model Features

**Hybrid Architecture Design** A combination of Diffusion Transformer (DiT) and Mixture of Experts (MoE) architecture:

- Based on Diffusion Transformer (DiT), with dual-stream MMDiT modules processing multimodal information and single-stream DiT modules optimizing global consistency.
- Dynamic routing mechanism flexibly allocates computing resources, enhancing complex scene processing capabilities and delivering excellent performance in color restoration, edge processing, and other details.

**Multimodal Text Encoder Integration** Integrates four text encoders:

- OpenCLIP ViT-bigG, OpenAI CLIP ViT-L (visual semantic alignment)
- T5-XXL (long text parsing)
- Llama-3.1-8B-Instruct (instruction understanding) This combination achieves SOTA performance in complex semantic parsing of colors, quantities, spatial relationships, etc., with Chinese prompt support significantly outperforming similar open-source models.

**Original Model Versions**

HiDream-ai provides three versions of the HiDream-I1 model to meet different needs. Below are the links to the original model repositories:

Model NameDescriptionInference StepsRepository LinkHiDream-I1-FullFull version50[🤗 HiDream-I1-Full](https://huggingface.co/HiDream-ai/HiDream-I1-Full)HiDream-I1-DevDistilled dev28[🤗 HiDream-I1-Dev](https://huggingface.co/HiDream-ai/HiDream-I1-Dev)HiDream-I1-FastDistilled fast16[🤗 HiDream-I1-Fast](https://huggingface.co/HiDream-ai/HiDream-I1-Fast)

## [​](http://docs.comfy.org#about-this-workflow-example) About This Workflow Example

In this example, we will use the repackaged version from ComfyOrg. You can find all the model files we’ll use in this example in the [HiDream-I1\_ComfyUI](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/) repository.

Before starting, please update your ComfyUI version to ensure it’s at least after this [commit](https://github.com/comfyanonymous/ComfyUI/commit/9ad792f92706e2179c58b2e5348164acafa69288) to make sure your ComfyUI has native support for HiDream

## [​](http://docs.comfy.org#hidream-i1-workflow) HiDream-I1 Workflow

The model requirements for different ComfyUI native HiDream-I1 workflows are basically the same, with only the [diffusion models](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/tree/main/split_files/diffusion_models) files being different.

If you don’t know which version to choose, please refer to the following suggestions:

- **HiDream-I1-Full** can generate the highest quality images
- **HiDream-I1-Dev** balances high-quality image generation with speed
- **HiDream-I1-Fast** can generate images in just 16 steps, suitable for scenarios requiring real-time iteration

For the **dev** and **fast** versions, negative prompts are not needed, so please set the `cfg` parameter to `1.0` during sampling. We have noted the corresponding parameter settings in the relevant workflows.

The full versions of all three versions require a lot of VRAM - you may need more than 27GB of VRAM to run them smoothly. In the corresponding workflow tutorials, we will use the **fp8** version as a demonstration example to ensure that most users can run it smoothly. However, we will still provide download links for different versions of the model in the corresponding examples, and you can choose the appropriate file based on your VRAM situation.

### [​](http://docs.comfy.org#model-installation) Model Installation

The following model files are common files that we will use. Please click on the corresponding links to download and save them according to the model file save location. We will guide you to download the corresponding **diffusion models** in the corresponding workflows.

**text\_encoders**：

- [clip\_l\_hidream.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/clip_l_hidream.safetensors)
- [clip\_g\_hidream.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/clip_g_hidream.safetensors)
- [t5xxl\_fp8\_e4m3fn\_scaled.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/t5xxl_fp8_e4m3fn_scaled.safetensors) This model has been used in many workflows, you may have already downloaded this file.
- [llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/llama_3.1_8b_instruct_fp8_scaled.safetensors)

**VAE**

- [ae.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/vae/ae.safetensors) This is Flux’s VAE model, if you have used Flux’s workflow before, you may have already downloaded this file.

**diffusion models** We will guide you to download the corresponding model files in the corresponding workflows.

Model file save location

```plaintext
📂 ComfyUI/
├── 📂 models/
│   ├── 📂 text_encoders/
│   │   ├─── clip_l_hidream.safetensors
│   │   ├─── clip_g_hidream.safetensors
│   │   ├─── t5xxl_fp8_e4m3fn_scaled.safetensors
│   │   └─── llama_3.1_8b_instruct_fp8_scaled.safetensors
│   └── 📂 vae/
│   │   └── ae.safetensors
│   └── 📂 diffusion_models/
│       └── ...               # We will guide you to install in the corresponding version workflow       
```

### [​](http://docs.comfy.org#hidream-i1-full-version-workflow) HiDream-I1 Full Version Workflow

#### [​](http://docs.comfy.org#1-model-file-download) 1. Model File Download

Please select the appropriate version based on your hardware. Click the link and download the corresponding model file to save it to the `ComfyUI/models/diffusion_models/` folder.

- FP8 version: [hidream\_i1\_full\_fp8.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_full_fp8.safetensors?download=true) requires more than 16GB of VRAM
- Full version: [hidream\_i1\_full\_f16.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_full_fp16.safetensors?download=true) requires more than 27GB of VRAM

#### [​](http://docs.comfy.org#2-workflow-file-download) 2. Workflow File Download

Please download the image below and drag it into ComfyUI to load the corresponding workflow

#### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step) 3. Complete the Workflow Step by Step

Complete the workflow execution step by step

1. Make sure the `Load Diffusion Model` node is using the `hidream_i1_full_fp8.safetensors` file
2. Make sure the four corresponding text encoders in `QuadrupleCLIPLoader` are loaded correctly
   
   - clip\_l\_hidream.safetensors
   - clip\_g\_hidream.safetensors
   - t5xxl\_fp8\_e4m3fn\_scaled.safetensors
   - llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors
3. Make sure the `Load VAE` node is using the `ae.safetensors` file
4. For the **full** version, you need to set the `shift` parameter in `ModelSamplingSD3` to `3.0`
5. For the `Ksampler` node, you need to make the following settings
   
   - Set `steps` to `50`
   - Set `cfg` to `5.0`
   - (Optional) Set `sampler` to `lcm`
   - (Optional) Set `scheduler` to `normal`
6. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

### [​](http://docs.comfy.org#hidream-i1-dev-version-workflow) HiDream-I1 Dev Version Workflow

#### [​](http://docs.comfy.org#1-model-file-download-2) 1. Model File Download

Please select the appropriate version based on your hardware, click the link and download the corresponding model file to save to the `ComfyUI/models/diffusion_models/` folder.

- FP8 version: [hidream\_i1\_dev\_fp8.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_dev_fp8.safetensors?download=true) requires more than 16GB of VRAM
- Full version: [hidream\_i1\_dev\_bf16.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_dev_bf16.safetensors?download=true) requires more than 27GB of VRAM

#### [​](http://docs.comfy.org#2-workflow-file-download-2) 2. Workflow File Download

Please download the image below and drag it into ComfyUI to load the corresponding workflow

#### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step-2) 3. Complete the Workflow Step by Step

Complete the workflow execution step by step

1. Make sure the `Load Diffusion Model` node is using the `hidream_i1_dev_fp8.safetensors` file
2. Make sure the four corresponding text encoders in `QuadrupleCLIPLoader` are loaded correctly
   
   - clip\_l\_hidream.safetensors
   - clip\_g\_hidream.safetensors
   - t5xxl\_fp8\_e4m3fn\_scaled.safetensors
   - llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors
3. Make sure the `Load VAE` node is using the `ae.safetensors` file
4. For the **dev** version, you need to set the `shift` parameter in `ModelSamplingSD3` to `6.0`
5. For the `Ksampler` node, you need to make the following settings
   
   - Set `steps` to `28`
   - (Important) Set `cfg` to `1.0`
   - (Optional) Set `sampler` to `lcm`
   - (Optional) Set `scheduler` to `normal`
6. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

### [​](http://docs.comfy.org#hidream-i1-fast-version-workflow) HiDream-I1 Fast Version Workflow

#### [​](http://docs.comfy.org#1-model-file-download-3) 1. Model File Download

Please select the appropriate version based on your hardware, click the link and download the corresponding model file to save to the `ComfyUI/models/diffusion_models/` folder.

- FP8 version: [hidream\_i1\_fast\_fp8.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_fast_fp8.safetensors?download=true) requires more than 16GB of VRAM
- Full version: [hidream\_i1\_fast\_bf16.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_i1_fast_fp8.safetensors?download=true) requires more than 27GB of VRAM

#### [​](http://docs.comfy.org#2-workflow-file-download-3) 2. Workflow File Download

Please download the image below and drag it into ComfyUI to load the corresponding workflow

#### [​](http://docs.comfy.org#3-complete-the-workflow-step-by-step-3) 3. Complete the Workflow Step by Step

Complete the workflow execution step by step

1. Make sure the `Load Diffusion Model` node is using the `hidream_i1_fast_fp8.safetensors` file
2. Make sure the four corresponding text encoders in `QuadrupleCLIPLoader` are loaded correctly
   
   - clip\_l\_hidream.safetensors
   - clip\_g\_hidream.safetensors
   - t5xxl\_fp8\_e4m3fn\_scaled.safetensors
   - llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors
3. Make sure the `Load VAE` node is using the `ae.safetensors` file
4. For the **fast** version, you need to set the `shift` parameter in `ModelSamplingSD3` to `3.0`
5. For the `Ksampler` node, you need to make the following settings
   
   - Set `steps` to `16`
   - (Important) Set `cfg` to `1.0`
   - (Optional) Set `sampler` to `lcm`
   - (Optional) Set `scheduler` to `normal`
6. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

## [​](http://docs.comfy.org#other-related-resources) Other Related Resources

### [​](http://docs.comfy.org#gguf-version-models) GGUF Version Models

- [HiDream-I1-Full-gguf](https://huggingface.co/city96/HiDream-I1-Full-gguf)
- [HiDream-I1-Dev-gguf](https://huggingface.co/city96/HiDream-I1-Dev-gguf)

You need to use the “Unet Loader (GGUF)” node in City96’s [ComfyUI-GGUF](https://github.com/city96/ComfyUI-GGUF) to replace the “Load Diffusion Model” node.

### [​](http://docs.comfy.org#nf4-version-models) NF4 Version Models

- [HiDream-I1-nf4](https://github.com/hykilpikonna/HiDream-I1-nf4)
- Use the [ComfyUI-HiDream-Sampler](https://github.com/SanDiegoDude/ComfyUI-HiDream-Sampler) node to use the NF4 version model.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/image/hidream/hidream-i1.mdx)

[Previous](http://docs.comfy.org/tutorials/flux/flux-1-controlnet)

[HiDream-e1This guide will help you understand and complete the ComfyUI native HiDream-I1 text-to-image workflow example  
\
Next](http://docs.comfy.org/tutorials/image/hidream/hidream-e1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Model Features](http://docs.comfy.org#model-features)
- [About This Workflow Example](http://docs.comfy.org#about-this-workflow-example)
- [HiDream-I1 Workflow](http://docs.comfy.org#hidream-i1-workflow)
- [Model Installation](http://docs.comfy.org#model-installation)
- [HiDream-I1 Full Version Workflow](http://docs.comfy.org#hidream-i1-full-version-workflow)
- [1. Model File Download](http://docs.comfy.org#1-model-file-download)
- [2. Workflow File Download](http://docs.comfy.org#2-workflow-file-download)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step)
- [HiDream-I1 Dev Version Workflow](http://docs.comfy.org#hidream-i1-dev-version-workflow)
- [1. Model File Download](http://docs.comfy.org#1-model-file-download-2)
- [2. Workflow File Download](http://docs.comfy.org#2-workflow-file-download-2)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step-2)
- [HiDream-I1 Fast Version Workflow](http://docs.comfy.org#hidream-i1-fast-version-workflow)
- [1. Model File Download](http://docs.comfy.org#1-model-file-download-3)
- [2. Workflow File Download](http://docs.comfy.org#2-workflow-file-download-3)
- [3. Complete the Workflow Step by Step](http://docs.comfy.org#3-complete-the-workflow-step-by-step-3)
- [Other Related Resources](http://docs.comfy.org#other-related-resources)
- [GGUF Version Models](http://docs.comfy.org#gguf-version-models)
- [NF4 Version Models](http://docs.comfy.org#nf4-version-models)