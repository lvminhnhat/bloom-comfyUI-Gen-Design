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

System Requirements

# System Requirements

This guide introduces some system requirements for ComfyUI, including hardware and software requirements

In this guide, we will introduce the system requirements for installing ComfyUI. Due to frequent updates of ComfyUI, this document may not be updated in a timely manner. Please refer to the relevant instructions in [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

Regardless of which version of ComfyUI you use, it runs in a separate Python environment.

You can refer to the following sections to learn about the installation methods for different systems and versions of ComfyUI. In the installation of different versions, we have simply described the system requirements.

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

## [​](http://docs.comfy.org#nvidia-50-series-gpu-requirements) Nvidia 50 Series GPU Requirements

To make your Nvidia 50 series GPU (Blackwell architecture) work properly with ComfyUI, you need a PyTorch version that supports CUDA 12.8 or newer. Currently (March 2025), the stable version of PyTorch does not yet support the Blackwell architecture, so you need to use a nightly build version.

Related discussions on this issue are concentrated [here](https://github.com/comfyanonymous/ComfyUI/discussions/6643).

### [​](http://docs.comfy.org#for-windows-users) For Windows Users

**Recommended Option:** Download the standalone ComfyUI Portable version with nightly pytorch 2.7 cu128:

- [Click here to download](https://github.com/comfyanonymous/ComfyUI/releases/download/latest/ComfyUI_windows_portable_nvidia_or_cpu_nightly_pytorch.7z)

**Other Options:** Older torch 2.6 Windows package:

- [Click here to download the standalone ComfyUI package with a cuda 12.8 torch build](https://github.com/comfyanonymous/ComfyUI/releases/download/latest/ComfyUI_cu128_50XX.7z)

### [​](http://docs.comfy.org#manual-installation) Manual Installation

Windows and Linux users can install the PyTorch nightly version using the following command:

```bash
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu128
```

### [​](http://docs.comfy.org#docker-container-alternative) Docker Container Alternative

You can try the PyTorch container provided by Nvidia, which might offer better performance.

Container address: [https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch)

Usage method:

```bash
docker run -p 8188:8188 --gpus all -it --rm nvcr.io/nvidia/pytorch:25.01-py3
```

Inside the Docker container, execute the following commands:

```bash
git clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI
grep -v 'torchaudio\|torchvision' requirements.txt > temp_requirements.txt
pip install -r temp_requirements.txt
python main.py --listen
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/installation/system_requirements.mdx)

[Previous](http://docs.comfy.org/get_started/introduction)

[Windows Desktop VersionThis article introduces how to download, install and use ComfyUI Desktop for Windows  
\
Next](http://docs.comfy.org/installation/desktop/windows)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Nvidia 50 Series GPU Requirements](http://docs.comfy.org#nvidia-50-series-gpu-requirements)
- [For Windows Users](http://docs.comfy.org#for-windows-users)
- [Manual Installation](http://docs.comfy.org#manual-installation)
- [Docker Container Alternative](http://docs.comfy.org#docker-container-alternative)