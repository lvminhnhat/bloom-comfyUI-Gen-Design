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

ComfyUI Native HiDream-e1 Workflow Example

# ComfyUI Native HiDream-e1 Workflow Example

This guide will help you understand and complete the ComfyUI native HiDream-I1 text-to-image workflow example

HiDream-E1 is an interactive image editing large model officially open-sourced by HiDream-ai on April 28, 2025, built based on HiDream-I1.

It allows you to edit images using natural language. The model is released under the [MIT License](https://github.com/HiDream-ai/HiDream-E1?tab=MIT-1-ov-file), supporting use in personal projects, scientific research, and commercial applications. In combination with the previously released [hidream-i1](http://docs.comfy.org/zh-CN/tutorials/advanced/hidream), it enables **creative capabilities from image generation to editing**.

**ComfyUI now natively supports HiDream E1**. In this guide, we will help you complete the workflow example of using HiDream E1 in ComfyUI.

For reference, this workflow takes about 500s for the first run and 370s for the second run with 28 sampling steps on Google Colab L4 with 22.5GB VRAM.

### [​](http://docs.comfy.org#hidream-e1-information) HiDream-E1 Information

**HiDream-E1 Model Download** Currently, HiDream provides a full version. Here is the model information:

NameInference StepsResolutionHuggingFace RepositoryHiDream-E1-Full28768x768[🤗 HiDream-E1-Full](https://huggingface.co/HiDream-ai/HiDream-E1-Full)

-[Github](https://github.com/HiDream-ai/HiDream-E1)

## [​](http://docs.comfy.org#comfyui-native-hidream-e1-workflow-example) ComfyUI Native HiDream-e1 Workflow Example

Please upgrade your ComfyUI to the latest version (latest commit) before starting to ensure your ComfyUI has the relevant support.

### [​](http://docs.comfy.org#1-download-hidream-e1-workflow-and-related-files) 1. Download HiDream-e1 Workflow and Related Files

#### [​](http://docs.comfy.org#1-1-download-workflow-file) 1.1 Download Workflow File

Please download the image below and drag it into ComfyUI. The workflow already contains model download information, and after loading, it will prompt you to download the corresponding models.

#### [​](http://docs.comfy.org#1-2-download-input-image) 1.2 Download Input Image

Please download the image below, which we will use as input

### [​](http://docs.comfy.org#2-manual-model-installation-for-hidream-e1-related-models) 2. Manual Model Installation for HiDream-e1 Related Models

All models mentioned in this guide can be found [here](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/tree/main/split_files). Please download the corresponding files and save them to the appropriate folders.

The following model files are shared models that we will use. Please click the corresponding links to download and save according to the model file storage location. We will guide you to download the corresponding **diffusion models** in the workflow.

**text\_encoders**:

- [clip\_l\_hidream.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/clip_l_hidream.safetensors)
- [clip\_g\_hidream.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/clip_g_hidream.safetensors)
- [t5xxl\_fp8\_e4m3fn\_scaled.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/t5xxl_fp8_e4m3fn_scaled.safetensors) This model has been used in many workflows, you may have already downloaded this file.
- [llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/text_encoders/llama_3.1_8b_instruct_fp8_scaled.safetensors)

**VAE**

- [ae.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/blob/main/split_files/vae/ae.safetensors) This is Flux’s VAE model. If you have used Flux workflows before, you may have already downloaded this file.

**diffusion models**

- [hidream\_e1\_full\_bf16.safetensors](https://huggingface.co/Comfy-Org/HiDream-I1_ComfyUI/resolve/main/split_files/diffusion_models/hidream_e1_full_bf16.safetensors)

Model file storage location

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
│       └── hidream_e1_full_bf16.safetensors   
```

### [​](http://docs.comfy.org#3-complete-the-hidream-e1-workflow-step-by-step) 3. Complete the HiDream-e1 Workflow Step by Step

Follow these steps to complete the workflow:

1. Make sure the `Load Diffusion Model` node has loaded the `hidream_e1_full_bf16.safetensors` model
2. Ensure that the four corresponding text encoders are correctly loaded in the `QuadrupleCLIPLoader`
   
   - clip\_l\_hidream.safetensors
   - clip\_g\_hidream.safetensors
   - t5xxl\_fp8\_e4m3fn\_scaled.safetensors
   - llama\_3.1\_8b\_instruct\_fp8\_scaled.safetensors
3. Make sure the `Load VAE` node is using the `ae.safetensors` file
4. Load the input image we downloaded earlier in the `Load Image` node
5. (Important) Enter **the prompt for how you want to modify the image** in the `Empty Text Encoder(Positive)` node
6. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to generate the image

### [​](http://docs.comfy.org#additional-notes-on-comfyui-hidream-e1-workflow) Additional Notes on ComfyUI HiDream-e1 Workflow

- You may need to modify the prompt multiple times or generate multiple times to get better results
- This model has difficulty maintaining consistency when changing image styles, so try to make your prompts as complete as possible
- As the model supports a resolution of 768\*768, in actual testing with other dimensions, the image performance is poor or even significantly different at other dimensions

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/image/hidream/hidream-e1.mdx)

[Previous](http://docs.comfy.org/tutorials/image/hidream/hidream-i1)

[Hunyuan3D-2This guide will demonstrate how to use Hunyuan3D-2 in ComfyUI to generate 3D assets.  
\
Next](http://docs.comfy.org/tutorials/3d/hunyuan3D-2)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [HiDream-E1 Information](http://docs.comfy.org#hidream-e1-information)
- [ComfyUI Native HiDream-e1 Workflow Example](http://docs.comfy.org#comfyui-native-hidream-e1-workflow-example)
- [1. Download HiDream-e1 Workflow and Related Files](http://docs.comfy.org#1-download-hidream-e1-workflow-and-related-files)
- [1.1 Download Workflow File](http://docs.comfy.org#1-1-download-workflow-file)
- [1.2 Download Input Image](http://docs.comfy.org#1-2-download-input-image)
- [2. Manual Model Installation for HiDream-e1 Related Models](http://docs.comfy.org#2-manual-model-installation-for-hidream-e1-related-models)
- [3. Complete the HiDream-e1 Workflow Step by Step](http://docs.comfy.org#3-complete-the-hidream-e1-workflow-step-by-step)
- [Additional Notes on ComfyUI HiDream-e1 Workflow](http://docs.comfy.org#additional-notes-on-comfyui-hidream-e1-workflow)