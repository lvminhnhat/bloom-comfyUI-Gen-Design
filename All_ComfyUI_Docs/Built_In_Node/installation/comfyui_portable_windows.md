[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Get Started

##### Get Started

- [Introduction](http://docs.comfy.org/get_started/introduction)
- Installation
  
  - [System Requirements](http://docs.comfy.org/installation/system_requirements)
  - Desktop(recommended)
  - [ComfyUI(portable) Windows](http://docs.comfy.org/installation/comfyui_portable_windows)
  - [Manual Installation](http://docs.comfy.org/installation/manual_install)
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

ComfyUI(portable) Windows

# ComfyUI(portable) Windows

This tutorial will guide you on how to download and start using ComfyUI Portable and run the corresponding programs

For Nvidia 50 series (Blackwell) GPUs, please refer to the [System Requirements](http://docs.comfy.org/installation/nvidia-50-series) section to ensure your system meets the requirements for ComfyUI.

**ComfyUI Portable** is a standalone packaged complete ComfyUI Windows version that has integrated an independent **Python (python\_embeded)** required for ComfyUI to run. You only need to extract it to use it. Currently, the portable version supports running through **Nvidia GPU** or **CPU**.

This guide section will walk you through installing ComfyUI Portable.

## [​](http://docs.comfy.org#download-comfyui-portable) Download ComfyUI Portable

You can get the latest ComfyUI Portable download link by clicking the link below

[Download ComfyUI Portable](https://github.com/comfyanonymous/ComfyUI/releases/latest/download/ComfyUI_windows_portable_nvidia.7z)

After downloading, you can use decompression software like [7-ZIP](https://7-zip.org/) to extract the compressed package

The file structure and description after extracting the portable version are as follows:

```plaintext
ComfyUI_windows_portable
├── 📂ComfyUI                   // ComfyUI main program
├── 📂python_embeded            // Independent Python environment
├── 📂update                    // Batch scripts for upgrading portable version
├── README_VERY_IMPORTANT.txt   // ComfyUI Portable usage instructions in English
├── run_cpu.bat                 // Double click to start ComfyUI (CPU only)
└── run_nvidia_gpu.bat          // Double click to start ComfyUI (Nvidia GPU)
```

## [​](http://docs.comfy.org#how-to-launch-comfyui) How to Launch ComfyUI

Double click either `run_nvidia_gpu.bat` or `run_cpu.bat` depending on your computer’s configuration to launch ComfyUI. You will see the command running as shown in the image below

When you see something similar to the image

```plaintext
To see the GUI go to: http://127.0.0.1:8188
```

At this point, your ComfyUI service has started. Normally, ComfyUI will automatically open your default browser and navigate to `http://127.0.0.1:8188`. If it doesn’t open automatically, please manually open your browser and visit this address.

During use, please do not close the corresponding command line window, otherwise ComfyUI will stop running

## [​](http://docs.comfy.org#first-image-generation) First Image Generation

After successful installation, you can refer to the section below to start your ComfyUI journey~

[**First Image Generation**  
\
This tutorial will guide you through your first model installation and text-to-image generation](http://docs.comfy.org/get_started/first_generation)

## [​](http://docs.comfy.org#additional-comfyui-portable-instructions) Additional ComfyUI Portable Instructions

### [​](http://docs.comfy.org#1-upgrading-comfyui-portable) 1. Upgrading ComfyUI Portable

You can use the batch commands in the update folder to upgrade your ComfyUI Portable version

```plaintext
ComfyUI_windows_portable
└─ 📂update
   ├── update.py
   ├── update_comfyui.bat                          // Update ComfyUI to the latest commit version
   ├── update_comfyui_and_python_dependencies.bat  // Only use when you have issues with your runtime environment
   └── update_comfyui_stable.bat                   // Update ComfyUI to the latest stable version
```

### [​](http://docs.comfy.org#2-comfyui-model-sharing-and-custom-model-directory-configuration) 2. ComfyUI Model Sharing and Custom Model Directory Configuration

If you are also using [A1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) or want to customize your model storage location, you can modify the following file to complete the configuration

```plaintext
ComfyUI_windows_portable
└─ 📂ComfyUI
  └── extra_model_paths.yaml.example  // This file is the configuration template
```

Please copy and rename the `extra_model_paths.yaml.example` to `extra_model_paths.yaml`.

Below is the original configuration file content, which you can modify according to your needs

```yaml
#Rename this to extra_model_paths.yaml and ComfyUI will load it


#config for a1111 ui
#all you have to do is change the base_path to where yours is installed
a111:
    base_path: path/to/stable-diffusion-webui/

    checkpoints: models/Stable-diffusion
    configs: models/Stable-diffusion
    vae: models/VAE
    loras: |
         models/Lora
         models/LyCORIS
    upscale_models: |
                  models/ESRGAN
                  models/RealESRGAN
                  models/SwinIR
    embeddings: embeddings
    hypernetworks: models/hypernetworks
    controlnet: models/ControlNet

#config for comfyui
#your base path should be either an existing comfy install or a central folder where you store all of your models, loras, etc.

#comfyui:
#     base_path: path/to/comfyui/
#     # You can use is_default to mark that these folders should be listed first, and used as the default dirs for eg downloads
#     #is_default: true
#     checkpoints: models/checkpoints/
#     clip: models/clip/
#     clip_vision: models/clip_vision/
#     configs: models/configs/
#     controlnet: models/controlnet/
#     diffusion_models: |
#                  models/diffusion_models
#                  models/unet
#     embeddings: models/embeddings/
#     loras: models/loras/
#     upscale_models: models/upscale_models/
#     vae: models/vae/

#other_ui:
#    base_path: path/to/ui
#    checkpoints: models/checkpoints
#    gligen: models/gligen
#    custom_nodes: path/custom_nodes

```

For example, if your WebUI is located at `D:\stable-diffusion-webui\`, you can modify the corresponding configuration to

```yaml
a111:
    base_path: D:\stable-diffusion-webui\
    checkpoints: models/Stable-diffusion
    configs: models/Stable-diffusion
    vae: models/VAE
    loras: |
         models/Lora
         models/LyCORIS
    upscale_models: |
                  models/ESRGAN
                  models/RealESRGAN
                  models/SwinIR
    embeddings: embeddings
    hypernetworks: models/hypernetworks
    controlnet: models/ControlNet
```

This way, models under paths like `D:\stable-diffusion-webui\models\Stable-diffusion\` can be detected and used by ComfyUI. Similarly, you can add other custom model location configurations

### [​](http://docs.comfy.org#3-setting-up-lan-access-for-comfyui-portable) 3. Setting Up LAN Access for ComfyUI Portable

If your ComfyUI is running on a local network and you want other devices to access ComfyUI, you can modify the `run_nvidia_gpu.bat` or `run_cpu.bat` file using Notepad to complete the configuration. This is mainly done by adding `--listen` to specify the listening address. Below is an example of the `run_nvidia_gpu.bat` file command with the `--listen` parameter added

```plaintext
.\python_embeded\python.exe -s ComfyUI\main.py --listen --windows-standalone-build
pause
```

After enabling ComfyUI, you will notice the final running address will become

```plaintext
Starting server

To see the GUI go to: http://0.0.0.0:8188
To see the GUI go to: http://[::]:8188
```

You can press `WIN + R` and type `cmd` to open the command prompt, then enter `ipconfig` to view your local IP address. Other devices can then access ComfyUI by entering `http://your-local-IP:8188` in their browser.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/installation/comfyui_portable_windows.mdx)

[Previous](http://docs.comfy.org/installation/desktop/linux)

[Manual Installation  
\
Next](http://docs.comfy.org/installation/manual_install)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Download ComfyUI Portable](http://docs.comfy.org#download-comfyui-portable)
- [How to Launch ComfyUI](http://docs.comfy.org#how-to-launch-comfyui)
- [First Image Generation](http://docs.comfy.org#first-image-generation)
- [Additional ComfyUI Portable Instructions](http://docs.comfy.org#additional-comfyui-portable-instructions)
- [1. Upgrading ComfyUI Portable](http://docs.comfy.org#1-upgrading-comfyui-portable)
- [2. ComfyUI Model Sharing and Custom Model Directory Configuration](http://docs.comfy.org#2-comfyui-model-sharing-and-custom-model-directory-configuration)
- [3. Setting Up LAN Access for ComfyUI Portable](http://docs.comfy.org#3-setting-up-lan-access-for-comfyui-portable)