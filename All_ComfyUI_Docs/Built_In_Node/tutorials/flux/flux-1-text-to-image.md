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

ComfyUI Flux.1 Text-to-Image Workflow Example

# ComfyUI Flux.1 Text-to-Image Workflow Example

This guide provides a brief introduction to the Flux.1 model and guides you through using the Flux.1 model for text-to-image generation with examples including the full version and the FP8 Checkpoint version.

Flux is one of the largest open-source text-to-image generation models, with 12B parameters and an original file size of approximately 23GB. It was developed by [Black Forest Labs](https://blackforestlabs.ai/), a team founded by former Stable Diffusion team members. Flux is known for its excellent image quality and flexibility, capable of generating high-quality, diverse images.

Currently, the Flux.1 model has several main versions:

- **Flux.1 Pro:** The best performing model, closed-source, only available through API calls.
- [**Flux.1 \[dev\]：**](https://huggingface.co/black-forest-labs/FLUX.1-dev) Open-source but limited to non-commercial use, distilled from the Pro version, with performance close to the Pro version.
- [**Flux.1 \[schnell\]：**](https://huggingface.co/black-forest-labs/FLUX.1-schnell) Uses the Apache2.0 license, requires only 4 steps to generate images, suitable for low-spec hardware.

**Flux.1 Model Features**

- **Hybrid Architecture:** Combines the advantages of Transformer networks and diffusion models, effectively integrating text and image information, improving the alignment accuracy between generated images and prompts, with excellent fidelity to complex prompts.
- **Parameter Scale:** Flux has 12B parameters, capturing more complex pattern relationships and generating more realistic, diverse images.
- **Supports Multiple Styles:** Supports diverse styles, with excellent performance for various types of images.

In this example, we’ll introduce text-to-image examples using both Flux.1 Dev and Flux.1 Schnell versions, including the full version model and the simplified FP8 Checkpoint version.

- **Flux Full Version:** Best performance, but requires larger VRAM resources and installation of multiple model files.
- **Flux FP8 Checkpoint:** Requires only one fp8 version of the model, but quality is slightly reduced compared to the full version.

All workflow images’s Metadata contains the corresponding model download information. You can load the workflows by:

- Dragging them directly into ComfyUI
- Or using the menu `Workflows` -&gt; `Open（ctrl+o）`

If you’re not using the Desktop Version or some models can’t be downloaded automatically, please refer to the manual installation sections to save the model files to the corresponding folder. Make sure your ComfyUI is updated to the latest version before starting.

## [​](http://docs.comfy.org#flux-1-full-version-text-to-image-example) Flux.1 Full Version Text-to-Image Example

If you can’t download models from [black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev), make sure you’ve logged into Huggingface and agreed to the corresponding repository’s license agreement.

### [​](http://docs.comfy.org#flux-1-dev) Flux.1 Dev

#### [​](http://docs.comfy.org#1-workflow-file) 1. Workflow File

Please download the image below and drag it into ComfyUI to load the workflow.

#### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

- The `flux1-dev.safetensors` file requires agreeing to the [black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) agreement before downloading via browser.
- If your VRAM is low, you can try using [t5xxl\_fp8\_e4m3fn.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp8_e4m3fn.safetensors?download=true) to replace the `t5xxl_fp16.safetensors` file.

Please download the following model files:

- [clip\_l.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/clip_l.safetensors?download=true)
- [t5xxl\_fp16.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp16.safetensors?download=true) Recommended when your VRAM is greater than 32GB.
- [ae.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/ae.safetensors?download=true)
- [flux1-dev.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-dev/resolve/main/flux1-dev.safetensors)

Storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors
│   │   └── t5xxl_fp16.safetensors
│   ├── vae/
│   │   └── ae.safetensors
│   └── diffusion_models/
│       └── flux1-dev.safetensors
```

#### [​](http://docs.comfy.org#3-steps-to-run-the-workflow) 3. Steps to Run the Workflow

Please refer to the image below to ensure all model files are loaded correctly

1. Ensure the `DualCLIPLoader` node has the following models loaded:
   
   - clip\_name1: t5xxl\_fp16.safetensors
   - clip\_name2: clip\_l.safetensors
2. Ensure the `Load Diffusion Model` node has `flux1-dev.safetensors` loaded
3. Make sure the `Load VAE` node has `ae.safetensors` loaded
4. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

Thanks to Flux’s excellent prompt following capability, we don’t need any negative prompts

### [​](http://docs.comfy.org#flux-1-schnell) Flux.1 Schnell

#### [​](http://docs.comfy.org#1-workflow-file-2) 1. Workflow File

Please download the image below and drag it into ComfyUI to load the workflow.

#### [​](http://docs.comfy.org#2-manual-models-installation) 2. Manual Models Installation

In this workflow, only two model files are different from the Flux1 Dev version workflow. For t5xxl, you can still use the fp16 version for better results.

- **t5xxl\_fp16.safetensors** -&gt; **t5xxl\_fp8.safetensors**
- **flux1-dev.safetensors** -&gt; **flux1-schnell.safetensors**

Complete model file list:

- [clip\_l.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/clip_l.safetensors?download=true)
- [t5xxl\_fp8\_e4m3fn.safetensors](https://huggingface.co/comfyanonymous/flux_text_encoders/resolve/main/t5xxl_fp8_e4m3fn.safetensors?download=true)
- [ae.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/ae.safetensors?download=true)
- [flux1-schnell.safetensors](https://huggingface.co/black-forest-labs/FLUX.1-schnell/resolve/main/flux1-schnell.safetensors)

File storage location:

```plaintext
ComfyUI/
├── models/
│   ├── text_encoders/
│   │   ├── clip_l.safetensors
│   │   └── t5xxl_fp8_e4m3fn.safetensors
│   ├── vae/
│   │   └── ae.safetensors
│   └── diffusion_models/
│       └── flux1-schnell.safetensors
```

#### [​](http://docs.comfy.org#3-steps-to-run-the-workflow-2) 3. Steps to Run the Workflow

1. Ensure the `DualCLIPLoader` node has the following models loaded:
   
   - clip\_name1: t5xxl\_fp8\_e4m3fn.safetensors
   - clip\_name2: clip\_l.safetensors
2. Ensure the `Load Diffusion Model` node has `flux1-schnell.safetensors` loaded
3. Ensure the `Load VAE` node has `ae.safetensors` loaded
4. Click the `Queue` button, or use the shortcut `Ctrl(cmd) + Enter` to run the workflow

## [​](http://docs.comfy.org#flux-1-fp8-checkpoint-version-text-to-image-example) Flux.1 FP8 Checkpoint Version Text-to-Image Example

The fp8 version is a quantized version of the original Flux.1 fp16 version. To some extent, the quality of this version will be lower than that of the fp16 version, but it also requires less VRAM, and you only need to install one model file to try running it.

### [​](http://docs.comfy.org#flux-1-dev-2) Flux.1 Dev

Please download the image below and drag it into ComfyUI to load the workflow.

Please download [flux1-dev-fp8.safetensors](https://huggingface.co/Comfy-Org/flux1-dev/resolve/main/flux1-dev-fp8.safetensors?download=true) and save it to the `ComfyUI/models/checkpoints/` directory.

Ensure that the corresponding `Load Checkpoint` node loads `flux1-dev-fp8.safetensors`, and you can try to run the workflow.

### [​](http://docs.comfy.org#flux-1-schnell-2) Flux.1 Schnell

Please download the image below and drag it into ComfyUI to load the workflow.

Please download [flux1-schnell-fp8.safetensors](https://huggingface.co/Comfy-Org/flux1-schnell/resolve/main/flux1-schnell-fp8.safetensors?download=true) and save it to the `ComfyUI/models/checkpoints/` directory.

Ensure that the corresponding `Load Checkpoint` node loads `flux1-schnell-fp8.safetensors`, and you can try to run the workflow.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/flux/flux-1-text-to-image.mdx)

[Previous](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets)

[Flux.1 fill devThis guide demonstrates how to use Flux.1 fill dev to create Inpainting and Outpainting workflows.  
\
Next](http://docs.comfy.org/tutorials/flux/flux-1-fill-dev)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Flux.1 Full Version Text-to-Image Example](http://docs.comfy.org#flux-1-full-version-text-to-image-example)
- [Flux.1 Dev](http://docs.comfy.org#flux-1-dev)
- [1. Workflow File](http://docs.comfy.org#1-workflow-file)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow)
- [Flux.1 Schnell](http://docs.comfy.org#flux-1-schnell)
- [1. Workflow File](http://docs.comfy.org#1-workflow-file-2)
- [2. Manual Models Installation](http://docs.comfy.org#2-manual-models-installation)
- [3. Steps to Run the Workflow](http://docs.comfy.org#3-steps-to-run-the-workflow-2)
- [Flux.1 FP8 Checkpoint Version Text-to-Image Example](http://docs.comfy.org#flux-1-fp8-checkpoint-version-text-to-image-example)
- [Flux.1 Dev](http://docs.comfy.org#flux-1-dev-2)
- [Flux.1 Schnell](http://docs.comfy.org#flux-1-schnell-2)