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

ComfyUI ControlNet Usage Example

# ComfyUI ControlNet Usage Example

This guide will introduce you to the basic concepts of ControlNet and demonstrate how to generate corresponding images in ComfyUI

Achieving precise control over image creation in AI image generation cannot be done with just one click. It typically requires numerous generation attempts to produce a satisfactory image. However, the emergence of **ControlNet** has effectively addressed this challenge.

ControlNet is a conditional control generation model based on diffusion models (such as Stable Diffusion), first proposed by [Lvmin Zhang](https://lllyasviel.github.io/) and Maneesh Agrawala et al. in 2023 in the paper [Adding Conditional Control to Text-to-Image Diffusion Models](https://arxiv.org/abs/2302.05543).

ControlNet models significantly enhance the controllability of image generation and the ability to reproduce details by introducing multimodal input conditions, such as edge detection maps, depth maps, and pose keypoints.

These conditioning constraints make image generation more controllable, allowing multiple ControlNet models to be used simultaneously during the drawing process for better results.

Before ControlNet, we could only rely on the model to generate images repeatedly until we were satisfied with the results, which involved a lot of randomness.

With the advent of ControlNet, we can control image generation by introducing additional conditions. For example, we can use a simple sketch to guide the image generation process, producing images that closely align with our sketch.

In this example, we will guide you through installing and using ControlNet models in [ComfyUI](https://github.com/comfyanonymous/ComfyUI), and complete a sketch-controlled image generation example.

The workflows for other types of ControlNet V1.1 models are similar to this example. You only need to select the appropriate model and upload the corresponding reference image based on your needs.

## [​](http://docs.comfy.org#controlnet-image-preprocessing-information) ControlNet Image Preprocessing Information

Different types of ControlNet models typically require different types of reference images:

> Image source: [ComfyUI ControlNet aux](https://github.com/Fannovel16/comfyui_controlnet_aux)

Since the current **Comfy Core** nodes do not include all types of **preprocessors**, in the actual examples in this documentation, we will provide pre-processed images. However, in practical use, you may need to use custom nodes to preprocess images to meet the requirements of different ControlNet models. Below are some relevant custom nodes:

- [ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet)
- [ComfyUI ControlNet aux](https://github.com/Fannovel16/comfyui_controlnet_aux)

## [​](http://docs.comfy.org#comfyui-controlnet-workflow-example-explanation) ComfyUI ControlNet Workflow Example Explanation

### [​](http://docs.comfy.org#1-controlnet-workflow-assets) 1. ControlNet Workflow Assets

Please download the workflow image below and drag it into ComfyUI to load the workflow:

Images with workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`. This image already includes download links for the corresponding models, and dragging it into ComfyUI will automatically prompt for downloads.

Please download the image below, which we will use as input:

### [​](http://docs.comfy.org#2-manual-model-installation) 2. Manual Model Installation

If your network cannot successfully complete the automatic download of the corresponding models, please try manually downloading the models below and placing them in the specified directories:

- [dreamCreationVirtual3DECommerce\_v10.safetensors](https://civitai.com/api/download/models/731340?type=Model&format=SafeTensor&size=full&fp=fp16)
- [vae-ft-mse-840000-ema-pruned.safetensors](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors?download=true)
- [control\_v11p\_sd15\_scribble\_fp16.safetensors](https://huggingface.co/comfyanonymous/ControlNet-v1-1_fp16_safetensors/resolve/main/control_v11p_sd15_scribble_fp16.safetensors?download=true)

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── dreamCreationVirtual3DECommerce_v10.safetensors
│   ├── vae/
│   │   └── vae-ft-mse-840000-ema-pruned.safetensors
│   └── controlnet/
│       └── control_v11p_sd15_scribble_fp16.safetensors
```

In this example, you could also use the VAE model embedded in dreamCreationVirtual3DECommerce\_v10.safetensors, but we’re following the model author’s recommendation to use a separate VAE model.

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution) 3. Step-by-Step Workflow Execution

1. Ensure that `Load Checkpoint` can load **dreamCreationVirtual3DECommerce\_v10.safetensors**
2. Ensure that `Load VAE` can load **vae-ft-mse-840000-ema-pruned.safetensors**
3. Click `Upload` in the `Load Image` node to upload the input image provided earlier
4. Ensure that `Load ControlNet` can load **control\_v11p\_sd15\_scribble\_fp16.safetensors**
5. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

## [​](http://docs.comfy.org#related-node-explanations) Related Node Explanations

### [​](http://docs.comfy.org#load-controlnet-node-explanation) Load ControlNet Node Explanation

Models located in `ComfyUI\models\controlnet` will be detected by ComfyUI and can be loaded through this node.

### [​](http://docs.comfy.org#apply-controlnet-node-explanation) Apply ControlNet Node Explanation

This node accepts the ControlNet model loaded by `load controlnet` and generates corresponding control conditions based on the input image.

**Input Types**

Parameter NameFunction`positive`Positive conditioning`negative`Negative conditioning`control_net`The ControlNet model to be applied`image`Preprocessed image used as reference for ControlNet application`vae`VAE model input`strength`Strength of ControlNet application; higher values increase ControlNet’s influence on the generated image`start_percent`Determines when to start applying ControlNet as a percentage; e.g., 0.2 means ControlNet guidance begins when 20% of diffusion is complete`end_percent`Determines when to stop applying ControlNet as a percentage; e.g., 0.8 means ControlNet guidance stops when 80% of diffusion is complete

**Output Types**

Parameter NameFunction`positive`Positive conditioning data processed by ControlNet`negative`Negative conditioning data processed by ControlNet

You can use chain connections to apply multiple ControlNet models, as shown in the image below. You can also refer to the [Mixing ControlNet Models](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets.mdx) guide to learn more about combining multiple ControlNet models.

You might see the `Apply ControlNet(Old)` node in some early workflows, which is an early version of the ControlNet node. It is currently deprecated and not visible by default in search and node lists. To enable it, go to **Settings** —&gt; **comfy** —&gt; **Node** and enable the `Show deprecated nodes in search` option. However, it’s recommended to use the new node.

## [​](http://docs.comfy.org#start-your-exploration) Start Your Exploration

1. Try creating similar sketches, or even draw your own, and use ControlNet models to generate images to experience the benefits of ControlNet.
2. Adjust the `Control Strength` parameter in the Apply ControlNet node to control the influence of the ControlNet model on the generated image.
3. Visit the [ControlNet-v1-1\_fp16\_safetensors](https://huggingface.co/comfyanonymous/ControlNet-v1-1_fp16_safetensors/tree/main) repository to download other types of ControlNet models and try using them to generate images.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/controlnet/controlnet.mdx)

[Previous](http://docs.comfy.org/tutorials/basic/multiple-loras)

[Pose ControlNetThis guide will introduce you to the basic concepts of Pose ControlNet, and demonstrate how to generate large-sized images in ComfyUI using a two-pass generation approach  
\
Next](http://docs.comfy.org/tutorials/controlnet/pose-controlnet-2-pass)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [ControlNet Image Preprocessing Information](http://docs.comfy.org#controlnet-image-preprocessing-information)
- [ComfyUI ControlNet Workflow Example Explanation](http://docs.comfy.org#comfyui-controlnet-workflow-example-explanation)
- [1. ControlNet Workflow Assets](http://docs.comfy.org#1-controlnet-workflow-assets)
- [2. Manual Model Installation](http://docs.comfy.org#2-manual-model-installation)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution)
- [Related Node Explanations](http://docs.comfy.org#related-node-explanations)
- [Load ControlNet Node Explanation](http://docs.comfy.org#load-controlnet-node-explanation)
- [Apply ControlNet Node Explanation](http://docs.comfy.org#apply-controlnet-node-explanation)
- [Start Your Exploration](http://docs.comfy.org#start-your-exploration)