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

LTX-Video

# LTX-Video

[LTX-Video](https://huggingface.co/Lightricks/LTX-Video) is a very efficient video model by lightricks. The important thing with this model is to give it long descriptive prompts.

## [​](http://docs.comfy.org#multi-frame-control) Multi Frame Control

Allows you to control the video with a series of images. You can download the input images: [starting frame](https://raw.githubusercontent.com/Comfy-Org/example_workflows/refs/heads/main/ltxv/multi-frame/house1.png) and [ending frame](https://raw.githubusercontent.com/Comfy-Org/example_workflows/refs/heads/main/ltxv/multi-frame/house2.png).

Drag the video directly into ComfyUI to run the workflow.

## [​](http://docs.comfy.org#image-to-video) Image to Video

Allows you to control the video with a first [frame image](https://raw.githubusercontent.com/Comfy-Org/example_workflows/refs/heads/main/ltxv/i2v/girl1.png).

Drag the video directly into ComfyUI to run the workflow.

## [​](http://docs.comfy.org#text-to-video) Text to Video

Drag the video directly into ComfyUI to run the workflow.

## [​](http://docs.comfy.org#requirements) Requirements

Download the following models and place them in the locations specified below:

- [ltx-video-2b-v0.9.5.safetensors](https://huggingface.co/Lightricks/LTX-Video/resolve/main/ltx-video-2b-v0.9.5.safetensors?download=true)
- [t5xxl\_fp16.safetensors](https://huggingface.co/Comfy-Org/mochi_preview_repackaged/resolve/main/split_files/text_encoders/t5xxl_fp16.safetensors?download=true)

```plaintext
├── checkpoints/
│   └── ltx-video-2b-v0.9.5.safetensors
└── text_encoders/
    └── t5xxl_fp16.safetensors
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/video/ltxv.mdx)

[Previous](http://docs.comfy.org/tutorials/3d/hunyuan3D-2)

[Hunyuan VideoThis guide shows how to use Hunyuan Text-to-Video and Image-to-Video workflows in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/video/hunyuan-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Multi Frame Control](http://docs.comfy.org#multi-frame-control)
- [Image to Video](http://docs.comfy.org#image-to-video)
- [Text to Video](http://docs.comfy.org#text-to-video)
- [Requirements](http://docs.comfy.org#requirements)