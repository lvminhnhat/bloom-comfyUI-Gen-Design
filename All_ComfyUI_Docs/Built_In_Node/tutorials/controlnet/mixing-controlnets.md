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
  
  - [ControlNet](http://docs.comfy.org/tutorials/controlnet/controlnet)
  - [Pose ControlNet](http://docs.comfy.org/tutorials/controlnet/pose-controlnet-2-pass)
  - [Depth ControlNet](http://docs.comfy.org/tutorials/controlnet/depth-controlnet)
  - [Depth T2I Adapter](http://docs.comfy.org/tutorials/controlnet/depth-t2i-adapter)
  - [Mixing ControlNet](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets)
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

ComfyUI Mixing ControlNet Examples

# ComfyUI Mixing ControlNet Examples

In this example, we will demonstrate how to mix multiple ControlNets and learn to use multiple ControlNet models to control image generation

In AI image generation, a single control condition often fails to meet the requirements of complex scenes. Mixing multiple ControlNets allows you to control different regions or aspects of an image simultaneously, achieving more precise control over image generation.

In certain scenarios, mixing ControlNets can leverage the characteristics of different control conditions to achieve more refined conditional control:

1. **Scene Complexity**: Complex scenes require multiple control conditions working together
2. **Fine-grained Control**: By adjusting the strength parameter of each ControlNet, you can precisely control the degree of influence for each part
3. **Complementary Effects**: Different types of ControlNets can complement each other, compensating for the limitations of single controls
4. **Creative Expression**: Combining different controls can produce unique creative effects

### [​](http://docs.comfy.org#how-to-mix-controlnets) How to Mix ControlNets

When mixing multiple ControlNets, each ControlNet influences the image generation process according to its applied area. ComfyUI enables multiple ControlNet conditions to be applied sequentially in a layered manner through chain connections in the `Apply ControlNet` node:

## [​](http://docs.comfy.org#comfyui-controlnet-regional-division-mixing-example) ComfyUI ControlNet Regional Division Mixing Example

In this example, we will use a combination of **Pose ControlNet** and **Scribble ControlNet** to generate a scene containing multiple elements: a character on the left controlled by Pose ControlNet and a cat on a scooter on the right controlled by Scribble ControlNet.

### [​](http://docs.comfy.org#1-controlnet-mixing-workflow-assets) 1. ControlNet Mixing Workflow Assets

Please download the workflow image below and drag it into ComfyUI to load the workflow:

This workflow image contains Metadata, and can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`. The system will automatically detect and prompt to download the required models.

Input pose image (controls the character pose on the left):

Input scribble image (controls the cat and scooter on the right):

### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

If your network cannot successfully complete the automatic download of the corresponding models, please try manually downloading the models below and placing them in the specified directories:

- [awpainting\_v14.safetensors](https://civitai.com/api/download/models/624939?type=Model&format=SafeTensor&size=full&fp=fp16)
- [control\_v11p\_sd15\_scribble\_fp16.safetensors](https://huggingface.co/comfyanonymous/ControlNet-v1-1_fp16_safetensors/resolve/main/control_v11p_sd15_scribble_fp16.safetensors?download=true)
- [control\_v11p\_sd15\_openpose\_fp16.safetensors](https://huggingface.co/comfyanonymous/ControlNet-v1-1_fp16_safetensors/resolve/main/control_v11p_sd15_openpose_fp16.safetensors?download=true)
- [vae-ft-mse-840000-ema-pruned.safetensors](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors?download=true)

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── awpainting_v14.safetensors
│   ├── controlnet/
│   │   └── control_v11p_sd15_scribble_fp16.safetensors
│   │   └── control_v11p_sd15_openpose_fp16.safetensors
│   ├── vae/
│   │   └── vae-ft-mse-840000-ema-pruned.safetensors
```

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution) 3. Step-by-Step Workflow Execution

Follow these steps according to the numbered markers in the image:

1. Ensure that `Load Checkpoint` can load **awpainting\_v14.safetensors**
2. Ensure that `Load VAE` can load **vae-ft-mse-840000-ema-pruned.safetensors**

First ControlNet group using the Openpose model: 3. Ensure that `Load ControlNet Model` loads **control\_v11p\_sd15\_openpose\_fp16.safetensors** 4. Click `Upload` in the `Load Image` node to upload the pose image provided earlier

Second ControlNet group using the Scribble model: 5. Ensure that `Load ControlNet Model` loads **control\_v11p\_sd15\_scribble\_fp16.safetensors** 6. Click `Upload` in the `Load Image` node to upload the scribble image provided earlier 7. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

## [​](http://docs.comfy.org#workflow-explanation) Workflow Explanation

#### [​](http://docs.comfy.org#strength-balance) Strength Balance

When controlling different regions of an image, balancing the strength parameters is particularly important:

- If the ControlNet strength for one region is significantly higher than another, it may cause that region’s control effect to overpower and suppress the other region
- It’s recommended to set similar strength values for ControlNets controlling different regions, for example, both set to 1.0

#### [​](http://docs.comfy.org#prompt-techniques) Prompt Techniques

For regional division mixing, the prompt needs to include descriptions of both regions:

```plaintext
"A woman in red dress, a cat riding a scooter, detailed background, high quality"
```

Such a prompt covers both the character and the cat on the scooter, ensuring the model pays attention to both control regions.

## [​](http://docs.comfy.org#multi-dimensional-control-applications-for-a-single-subject) Multi-dimensional Control Applications for a Single Subject

In addition to the regional division mixing shown in this example, another common mixing approach is to apply multi-dimensional control to the same subject. For example:

- **Pose + Depth**: Control character posture and spatial sense
- **Pose + Canny**: Control character posture and edge details
- **Pose + Reference**: Control character posture while referencing a specific style

In this type of application, reference images for multiple ControlNets should be aligned to the same subject, and their strengths should be adjusted to ensure proper balance.

By combining different types of ControlNets and specifying their control regions, you can achieve precise control over elements in your image.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/controlnet/mixing-controlnets.mdx)

[Previous](http://docs.comfy.org/tutorials/controlnet/depth-t2i-adapter)

[Flux.1 Text-to-ImageThis guide provides a brief introduction to the Flux.1 model and guides you through using the Flux.1 model for text-to-image generation with examples including the full version and the FP8 Checkpoint version.  
\
Next](http://docs.comfy.org/tutorials/flux/flux-1-text-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [How to Mix ControlNets](http://docs.comfy.org#how-to-mix-controlnets)
- [ComfyUI ControlNet Regional Division Mixing Example](http://docs.comfy.org#comfyui-controlnet-regional-division-mixing-example)
- [1. ControlNet Mixing Workflow Assets](http://docs.comfy.org#1-controlnet-mixing-workflow-assets)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution)
- [Workflow Explanation](http://docs.comfy.org#workflow-explanation)
- [Strength Balance](http://docs.comfy.org#strength-balance)
- [Prompt Techniques](http://docs.comfy.org#prompt-techniques)
- [Multi-dimensional Control Applications for a Single Subject](http://docs.comfy.org#multi-dimensional-control-applications-for-a-single-subject)