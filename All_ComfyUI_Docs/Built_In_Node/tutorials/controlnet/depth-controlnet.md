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

ComfyUI Depth ControlNet Usage Example

# ComfyUI Depth ControlNet Usage Example

This guide will introduce you to the basic concepts of Depth ControlNet and demonstrate how to generate corresponding images in ComfyUI

## [​](http://docs.comfy.org#introduction-to-depth-maps-and-depth-controlnet) Introduction to Depth Maps and Depth ControlNet

A depth map is a special type of image that uses grayscale values to represent the distance between objects in a scene and the observer or camera. In a depth map, the grayscale value is inversely proportional to distance: brighter areas (closer to white) indicate objects that are closer, while darker areas (closer to black) indicate objects that are farther away.

Depth ControlNet is a ControlNet model specifically trained to understand and utilize depth map information. It helps AI correctly interpret spatial relationships, ensuring that generated images conform to the spatial structure specified by the depth map, thereby enabling precise control over three-dimensional spatial layouts.

### [​](http://docs.comfy.org#application-scenarios-for-depth-maps-with-controlnet) Application Scenarios for Depth Maps with ControlNet

Depth maps have numerous applications in various scenarios:

1. **Portrait Scenes**: Control the spatial relationship between subjects and backgrounds, avoiding distortion in critical areas such as faces
2. **Landscape Scenes**: Control the hierarchical relationships between foreground, middle ground, and background
3. **Architectural Scenes**: Control the spatial structure and perspective relationships of buildings
4. **Product Showcase**: Control the separation and spatial positioning of products against their backgrounds

In this example, we will use a depth map to generate an architectural visualization scene.

## [​](http://docs.comfy.org#comfyui-controlnet-workflow-example-explanation) ComfyUI ControlNet Workflow Example Explanation

### [​](http://docs.comfy.org#1-controlnet-workflow-assets) 1. ControlNet Workflow Assets

Please download the workflow image below and drag it into ComfyUI to load the workflow:

Images with workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`. This image already includes download links for the corresponding models, and dragging it into ComfyUI will automatically prompt for downloads.

Please download the image below, which we will use as input:

### [​](http://docs.comfy.org#2-model-installation) 2. Model Installation

If your network cannot successfully complete the automatic download of the corresponding models, please try manually downloading the models below and placing them in the specified directories:

- [architecturerealmix\_v11.safetensors](https://civitai.com/api/download/models/431755?type=Model&format=SafeTensor&size=full&fp=fp16)
- [control\_v11f1p\_sd15\_depth\_fp16.safetensors](https://huggingface.co/comfyanonymous/ControlNet-v1-1_fp16_safetensors/resolve/main/control_v11f1p_sd15_depth_fp16.safetensors?download=true)

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── architecturerealmix_v11.safetensors
│   └── controlnet/
│       └── control_v11f1p_sd15_depth_fp16.safetensors
```

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution) 3. Step-by-Step Workflow Execution

1. Ensure that `Load Checkpoint` can load **architecturerealmix\_v11.safetensors**
2. Ensure that `Load ControlNet` can load **control\_v11f1p\_sd15\_depth\_fp16.safetensors**
3. Click `Upload` in the `Load Image` node to upload the depth image provided earlier
4. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

## [​](http://docs.comfy.org#combining-depth-control-with-other-techniques) Combining Depth Control with Other Techniques

Based on different creative needs, you can combine Depth ControlNet with other types of ControlNet to achieve better results:

1. **Depth + Lineart**: Maintain spatial relationships while reinforcing outlines, suitable for architecture, products, and character design
2. **Depth + Pose**: Control character posture while maintaining correct spatial relationships, suitable for character scenes

For more information on using multiple ControlNet models together, please refer to the [Mixing ControlNet](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets.mdx) example.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/controlnet/depth-controlnet.mdx)

[Previous](http://docs.comfy.org/tutorials/controlnet/pose-controlnet-2-pass)

[Depth T2I AdapterThis guide will introduce you to the basic concepts of Depth T2I Adapter and demonstrate how to generate corresponding images in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/controlnet/depth-t2i-adapter)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Introduction to Depth Maps and Depth ControlNet](http://docs.comfy.org#introduction-to-depth-maps-and-depth-controlnet)
- [Application Scenarios for Depth Maps with ControlNet](http://docs.comfy.org#application-scenarios-for-depth-maps-with-controlnet)
- [ComfyUI ControlNet Workflow Example Explanation](http://docs.comfy.org#comfyui-controlnet-workflow-example-explanation)
- [1. ControlNet Workflow Assets](http://docs.comfy.org#1-controlnet-workflow-assets)
- [2. Model Installation](http://docs.comfy.org#2-model-installation)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution)
- [Combining Depth Control with Other Techniques](http://docs.comfy.org#combining-depth-control-with-other-techniques)