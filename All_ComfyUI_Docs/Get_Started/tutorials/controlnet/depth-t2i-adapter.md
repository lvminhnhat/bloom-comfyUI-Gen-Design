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

ComfyUI Depth T2I Adapter Usage Example

# ComfyUI Depth T2I Adapter Usage Example

This guide will introduce you to the basic concepts of Depth T2I Adapter and demonstrate how to generate corresponding images in ComfyUI

## [​](http://docs.comfy.org#introduction-to-t2i-adapter) Introduction to T2I Adapter

[T2I-Adapter](https://huggingface.co/TencentARC/T2I-Adapter) is a lightweight adapter developed by [Tencent ARC Lab](https://github.com/TencentARC) designed to enhance the structural, color, and style control capabilities of text-to-image generation models (such as Stable Diffusion). It works by aligning external conditions (such as edge detection maps, depth maps, sketches, or color reference images) with the model’s internal features, achieving high-precision control without modifying the original model structure. With only about 77M parameters (approximately 300MB in size), its inference speed is about 3 times faster than [ControlNet](https://github.com/lllyasviel/ControlNet-v1-1-nightly), and it supports multiple condition combinations (such as sketch + color grid). Application scenarios include line art to image conversion, color style transfer, multi-element scene generation, and more.

### [​](http://docs.comfy.org#comparison-between-t2i-adapter-and-controlnet) Comparison Between T2I Adapter and ControlNet

Although their functions are similar, there are notable differences in implementation and application:

1. **Lightweight Design**: T2I Adapter has fewer parameters and a smaller memory footprint
2. **Inference Speed**: T2I Adapter is typically about 3 times faster than ControlNet
3. **Control Precision**: ControlNet offers more precise control in certain scenarios, while T2I Adapter is more suitable for lightweight control
4. **Multi-condition Combination**: T2I Adapter shows more significant resource advantages when combining multiple conditions

### [​](http://docs.comfy.org#main-types-of-t2i-adapter) Main Types of T2I Adapter

T2I Adapter provides various types to control different aspects:

- **Depth**: Controls the spatial structure and depth relationships in images
- **Line Art (Canny/Sketch)**: Controls image edges and lines
- **Keypose**: Controls character poses and actions
- **Segmentation (Seg)**: Controls scene layout through semantic segmentation
- **Color**: Controls the overall color scheme of images

In ComfyUI, using T2I Adapter is similar to [ControlNet](http://docs.comfy.org/tutorials/controlnet/controlnet.mdx) in terms of interface and workflow. In this example, we will demonstrate how to use a depth T2I Adapter to control an interior scene.

## [​](http://docs.comfy.org#value-of-depth-t2i-adapter-applications) Value of Depth T2I Adapter Applications

Depth maps have several important applications in image generation:

1. **Spatial Layout Control**: Accurately describes three-dimensional spatial structures, suitable for interior design and architectural visualization
2. **Object Positioning**: Controls the relative position and size of objects in a scene, suitable for product showcases and scene construction
3. **Perspective Relationships**: Maintains reasonable perspective and proportions, suitable for landscape and urban scene generation
4. **Light and Shadow Layout**: Natural light and shadow distribution based on depth information, enhancing realism

We will use interior design as an example to demonstrate how to use the depth T2I Adapter, but these techniques are applicable to other scenarios as well.

## [​](http://docs.comfy.org#comfyui-depth-t2i-adapter-workflow-example-explanation) ComfyUI Depth T2I Adapter Workflow Example Explanation

### [​](http://docs.comfy.org#1-depth-t2i-adapter-workflow-assets) 1. Depth T2I Adapter Workflow Assets

Please download the workflow image below and drag it into ComfyUI to load the workflow:

Images with workflow JSON in their metadata can be directly dragged into ComfyUI or loaded using the menu `Workflows` -&gt; `Open (ctrl+o)`. This image already includes download links for the corresponding models, and dragging it into ComfyUI will automatically prompt for downloads.

Please download the image below, which we will use as input:

### [​](http://docs.comfy.org#2-model-installation) 2. Model Installation

If your network cannot successfully complete the automatic download of the corresponding models, please try manually downloading the models below and placing them in the specified directories:

- [interiordesignsuperm\_v2.safetensors](https://civitai.com/api/download/models/93152?type=Model&format=SafeTensor&size=full&fp=fp16)
- [t2iadapter\_depth\_sd15v2.pth](https://huggingface.co/TencentARC/T2I-Adapter/resolve/main/models/t2iadapter_depth_sd15v2.pth?download=true)

```plaintext
ComfyUI/
├── models/
│   ├── checkpoints/
│   │   └── interiordesignsuperm_v2.safetensors
│   └── controlnet/
│       └── t2iadapter_depth_sd15v2.pth
```

### [​](http://docs.comfy.org#3-step-by-step-workflow-execution) 3. Step-by-Step Workflow Execution

1. Ensure that `Load Checkpoint` can load **interiordesignsuperm\_v2.safetensors**
2. Ensure that `Load ControlNet` can load **t2iadapter\_depth\_sd15v2.pth**
3. Click `Upload` in the `Load Image` node to upload the input image provided earlier
4. Click the `Queue` button or use the shortcut `Ctrl(cmd) + Enter` to execute the image generation

## [​](http://docs.comfy.org#general-tips-for-using-t2i-adapter) General Tips for Using T2I Adapter

### [​](http://docs.comfy.org#input-image-quality-optimization) Input Image Quality Optimization

Regardless of the application scenario, high-quality input images are key to successfully using T2I Adapter:

1. **Moderate Contrast**: Control images (such as depth maps, line art) should have clear contrast, but not excessively extreme
2. **Clear Boundaries**: Ensure that major structures and element boundaries are clearly distinguishable in the control image
3. **Noise Control**: Try to avoid excessive noise in control images, especially for depth maps and line art
4. **Reasonable Layout**: Control images should have a reasonable spatial layout and element distribution

## [​](http://docs.comfy.org#characteristics-of-t2i-adapter-usage) Characteristics of T2I Adapter Usage

One major advantage of T2I Adapter is its ability to easily combine multiple conditions for complex control effects:

1. **Depth + Edge**: Control spatial layout while maintaining clear structural edges, suitable for architecture and interior design
2. **Line Art + Color**: Control shapes while specifying color schemes, suitable for character design and illustrations
3. **Pose + Segmentation**: Control character actions while defining scene areas, suitable for complex narrative scenes

Mixing different T2I Adapters, or combining them with other control methods (such as ControlNet, regional prompts, etc.), can further expand creative possibilities. To achieve mixing, simply chain multiple `Apply ControlNet` nodes together in the same way as described in [Mixing ControlNet](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets.mdx).

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/controlnet/depth-t2i-adapter.mdx)

[Previous](http://docs.comfy.org/tutorials/controlnet/depth-controlnet)

[Mixing ControlNetIn this example, we will demonstrate how to mix multiple ControlNets and learn to use multiple ControlNet models to control image generation  
\
Next](http://docs.comfy.org/tutorials/controlnet/mixing-controlnets)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Introduction to T2I Adapter](http://docs.comfy.org#introduction-to-t2i-adapter)
- [Comparison Between T2I Adapter and ControlNet](http://docs.comfy.org#comparison-between-t2i-adapter-and-controlnet)
- [Main Types of T2I Adapter](http://docs.comfy.org#main-types-of-t2i-adapter)
- [Value of Depth T2I Adapter Applications](http://docs.comfy.org#value-of-depth-t2i-adapter-applications)
- [ComfyUI Depth T2I Adapter Workflow Example Explanation](http://docs.comfy.org#comfyui-depth-t2i-adapter-workflow-example-explanation)
- [1. Depth T2I Adapter Workflow Assets](http://docs.comfy.org#1-depth-t2i-adapter-workflow-assets)
- [2. Model Installation](http://docs.comfy.org#2-model-installation)
- [3. Step-by-Step Workflow Execution](http://docs.comfy.org#3-step-by-step-workflow-execution)
- [General Tips for Using T2I Adapter](http://docs.comfy.org#general-tips-for-using-t2i-adapter)
- [Input Image Quality Optimization](http://docs.comfy.org#input-image-quality-optimization)
- [Characteristics of T2I Adapter Usage](http://docs.comfy.org#characteristics-of-t2i-adapter-usage)