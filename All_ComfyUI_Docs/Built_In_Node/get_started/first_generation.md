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

Getting Started with AI Image Generation

# Getting Started with AI Image Generation

This tutorial will guide you through your first image generation with ComfyUI, covering basic interface operations like workflow loading, model installation, and image generation

This guide aims to help you understand ComfyUI’s basic operations and complete your first image generation. We’ll cover:

1. Loading example workflows
   
   - Loading from ComfyUI’s workflow templates
   - Loading from images with workflow metadata
2. Model installation guidance
   
   - Automatic model installation
   - Manual model installation
   - Using ComfyUI Manager for model installation
3. Completing your first text-to-image generation

## [​](http://docs.comfy.org#about-text-to-image) About Text-to-Image

Text-to-Image is a fundamental AI drawing feature that generates images from text descriptions. It’s one of the most commonly used functions in AI art generation. You can think of the process as telling your requirements (positive and negative prompts) to an artist (the drawing model), who will then create what you want. Detailed explanations about text-to-image will be covered in the [Text to Image](http://docs.comfy.org/tutorials/basic/text-to-image) chapter.

## [​](http://docs.comfy.org#comfyui-text-to-image-workflow-tutorial) ComfyUI Text-to-Image Workflow Tutorial

### [​](http://docs.comfy.org#1-launch-comfyui) 1. Launch ComfyUI

Make sure you’ve followed the installation guide to start ComfyUI and can successfully enter the ComfyUI interface.

If you have not installed ComfyUI, please choose a suitable version to install based on your device.

ComfyUI Desktop (Recommended)

ComfyUI Desktop currently supports standalone installation for **Windows and MacOS (ARM)**, currently in Beta

- Code is open source on [Github](https://github.com/Comfy-Org/desktop)

You can choose the appropriate installation for your system and hardware below

- Windows
- MacOS(Apple Silicon)
- Linux

[**ComfyUI Desktop (Windows) Installation Guide**  
\
Suitable for **Windows** version with **Nvidia** GPU](http://docs.comfy.org/installation/desktop/windows)

[**ComfyUI Desktop (Windows) Installation Guide**  
\
Suitable for **Windows** version with **Nvidia** GPU](http://docs.comfy.org/installation/desktop/windows)

[**ComfyUI Desktop (MacOS) Installation Guide**  
\
Suitable for MacOS with **Apple Silicon**](http://docs.comfy.org/installation/desktop/macos)

ComfyUI Desktop **currently has no Linux prebuilds**, please visit the [Manual Installation](http://docs.comfy.org/installation/manual_install) section to install ComfyUI

ComfyUI Portable (Windows)

[**ComfyUI Portable (Windows) Installation Guide**  
\
Supports **Windows** ComfyUI version running on **Nvidia GPUs** or **CPU-only**, always use the latest commits and completely portable.](http://docs.comfy.org/installation/comfyui_portable_windows)

Manual Installation

[**ComfyUI Manual Installation Guide**  
\
Supports all system types and GPU types (Nvidia, AMD, Intel, Apple Silicon, Ascend NPU, Cambricon MLU)](http://docs.comfy.org/installation/manual_install)

### [​](http://docs.comfy.org#2-load-default-text-to-image-workflow) 2. Load Default Text-to-Image Workflow

ComfyUI usually loads the default text-to-image workflow automatically when launched. However, you can try different methods to load workflows to familiarize yourself with ComfyUI’s basic operations:

- Load from Workflow Template
- Load from Images with Metadata
- Load from workflow.json

Follow the numbered steps in the image:

1. Click the **Fit View** button in the bottom right to ensure any loaded workflow isn’t hidden
2. Click the **folder icon (workflows)** in the sidebar
3. Click the **Browse example workflows** button at the top of the Workflows panel

Continue with:

4. Select the first default workflow **Image Generation** to load it

Alternatively, you can select **Browse workflow templates** from the workflow menu

Follow the numbered steps in the image:

1. Click the **Fit View** button in the bottom right to ensure any loaded workflow isn’t hidden
2. Click the **folder icon (workflows)** in the sidebar
3. Click the **Browse example workflows** button at the top of the Workflows panel

Continue with:

4. Select the first default workflow **Image Generation** to load it

Alternatively, you can select **Browse workflow templates** from the workflow menu

All images generated by ComfyUI contain metadata including workflow information. You can load workflows by:

- Dragging and dropping a ComfyUI-generated image into the interface
- Using menu **Workflows** -&gt; **Open** to open an image

Try loading the workflow using this example image:

ComfyUI workflows can be stored in JSON format. You can export workflows using menu **Workflows** -&gt; **Export**.

Try downloading and loading this example workflow:

[Download text-to-image.json](https://github.com/Comfy-Org/docs/blob/main/public/text-to-image.json)

After downloading, use menu **Workflows** -&gt; **Open** to load the JSON file.

### [​](http://docs.comfy.org#3-model-installation) 3. Model Installation

Most ComfyUI installations don’t include base models by default. After loading the workflow, if you don’t have the [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) model installed, you’ll see this prompt:

All models are stored in `<your ComfyUI installation>/ComfyUI/models/` with subfolders like `checkpoints`, `embeddings`, `vae`, `lora`, `upscale_model`, etc. ComfyUI detects models in these folders and paths configured in `extra_models_config.yaml` at startup.

You can install models through:

- Automatic Download
- ComfyUI Manager
- Manual Installation

After you click the **Download** button, ComfyUI will execute the download, and different behaviors will be performed depending on the version you are using.

- ComfyUI Desktop
- ComfyUI Portable

The desktop version will automatically complete the model download and save it to the `<your ComfyUI installation location>/ComfyUI/models/checkpoints` directory. You can wait for the installation to complete or view the installation progress in the model panel on the sidebar.

If everything goes smoothly, the model should be able to download locally. If the download fails for a long time, please try other installation methods.

The desktop version will automatically complete the model download and save it to the `<your ComfyUI installation location>/ComfyUI/models/checkpoints` directory. You can wait for the installation to complete or view the installation progress in the model panel on the sidebar.

If everything goes smoothly, the model should be able to download locally. If the download fails for a long time, please try other installation methods.

The browser will execute file downloads. Please save the file to the `<your ComfyUI installation location>/ComfyUI_windows_portable/ComfyUI/models/checkpoints` directory after the download is complete.

After you click the **Download** button, ComfyUI will execute the download, and different behaviors will be performed depending on the version you are using.

- ComfyUI Desktop
- ComfyUI Portable

The desktop version will automatically complete the model download and save it to the `<your ComfyUI installation location>/ComfyUI/models/checkpoints` directory. You can wait for the installation to complete or view the installation progress in the model panel on the sidebar.

If everything goes smoothly, the model should be able to download locally. If the download fails for a long time, please try other installation methods.

The desktop version will automatically complete the model download and save it to the `<your ComfyUI installation location>/ComfyUI/models/checkpoints` directory. You can wait for the installation to complete or view the installation progress in the model panel on the sidebar.

If everything goes smoothly, the model should be able to download locally. If the download fails for a long time, please try other installation methods.

The browser will execute file downloads. Please save the file to the `<your ComfyUI installation location>/ComfyUI_windows_portable/ComfyUI/models/checkpoints` directory after the download is complete.

ComfyUI Manager is a tool for managing custom nodes, models, and plugins.

1

Open ComfyUI Manager

Click the `Manager` button to open ComfyUI Manager

2

Open Model Manager

Click `Model Manager`

3

Search and Install Model

1. Search for `v1-5-pruned-emaonly.ckpt`
2. Click `install` on the desired model

Visit [v1-5-pruned-emaonly-fp16.safetensors](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors) and follow this guide:

Save the downloaded file to:

- ComfyUI Desktop
- ComfyUI Portable

Save to `<your ComfyUI installation>/ComfyUI/models/checkpoints`

Save to `<your ComfyUI installation>/ComfyUI/models/checkpoints`

Save to `ComfyUI_windows_portable/ComfyUI/models/checkpoints`

Refresh or restart ComfyUI after saving.

### [​](http://docs.comfy.org#4-load-model-and-generate-your-first-image) 4. Load Model and Generate Your First Image

After installing the model:

1. In the **Load Checkpoint** node, ensure **v1-5-pruned-emaonly-fp16.safetensors** is selected
2. Click `Queue` or press `Ctrl + Enter` to generate

The result will appear in the **Save Image** node. Right-click to save locally.

For detailed text-to-image instructions, see our comprehensive guide:

[**ComfyUI Text-to-Image Workflow Guide**  
\
Click here for detailed text-to-image workflow instructions](http://docs.comfy.org/tutorials/basic/text-to-image)

## [​](http://docs.comfy.org#troubleshooting) Troubleshooting

### [​](http://docs.comfy.org#model-loading-issues) Model Loading Issues

If the `Load Checkpoint` node shows no models or displays “null”, verify your model installation location and try refreshing or restarting ComfyUI.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/get_started/first_generation.mdx)

[Previous](http://docs.comfy.org/installation/manual_install)

[Interface OverviewIn this article, we will briefly introduce the basic user interface of ComfyUI, familiarizing you with the various parts of the ComfyUI interface.  
\
Next](http://docs.comfy.org/interface/overview)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [About Text-to-Image](http://docs.comfy.org#about-text-to-image)
- [ComfyUI Text-to-Image Workflow Tutorial](http://docs.comfy.org#comfyui-text-to-image-workflow-tutorial)
- [1. Launch ComfyUI](http://docs.comfy.org#1-launch-comfyui)
- [2. Load Default Text-to-Image Workflow](http://docs.comfy.org#2-load-default-text-to-image-workflow)
- [3. Model Installation](http://docs.comfy.org#3-model-installation)
- [4. Load Model and Generate Your First Image](http://docs.comfy.org#4-load-model-and-generate-your-first-image)
- [Troubleshooting](http://docs.comfy.org#troubleshooting)
- [Model Loading Issues](http://docs.comfy.org#model-loading-issues)