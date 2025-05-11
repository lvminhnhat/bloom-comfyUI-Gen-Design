[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Get Started

##### Get Started

- [Introduction](http://docs.comfy.org/get_started/introduction)
- Installation
  
  - [System Requirements](http://docs.comfy.org/installation/system_requirements)
  - Desktop(recommended)
    
    - [Windows Desktop Version](http://docs.comfy.org/installation/desktop/windows)
    - [MacOS Desktop Version](http://docs.comfy.org/installation/desktop/macos)
    - [Linux Desktop Version](http://docs.comfy.org/installation/desktop/linux)
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

Windows Desktop Version

# Windows Desktop Version

This article introduces how to download, install and use ComfyUI Desktop for Windows

**ComfyUI Desktop** is a standalone installation version that can be installed like regular software. It supports quick installation and automatic configuration of the **Python environment and dependencies**, and supports one-click import of existing ComfyUI settings, models, workflows, and files. You can quickly migrate from an existing [ComfyUI Portable version](http://docs.comfy.org/installation/comfyui_portable_windows) to the Desktop version.

ComfyUI Desktop is an open source project, please visit the full code [here](https://github.com/Comfy-Org/desktop)

ComfyUI Desktop hardware requirements:

- NVIDIA GPU

This tutorial will guide you through the software installation process and explain related configuration details.

As **ComfyUI Desktop** is still in **Beta** status, the actual installation process may change

## [​](http://docs.comfy.org#comfyui-desktop-windows-download) ComfyUI Desktop (Windows) Download

Please click the button below to download the installation package for Windows **ComfyUI Desktop**

[Download for Windows (NVIDIA)](https://download.comfy.org/windows/nsis/x64)

## [​](http://docs.comfy.org#comfyui-desktop-installation-steps) ComfyUI Desktop Installation Steps

Double-click the downloaded installation package file, which will first perform an automatic installation and create a **ComfyUI Desktop** shortcut on the desktop

Double-click the corresponding shortcut to enter ComfyUI initialization settings

### [​](http://docs.comfy.org#comfyui-desktop-initialization-process) ComfyUI Desktop Initialization Process

1

Start Screen

- Normal Start
- Maintenance Page

Click **Get Started** to begin initialization

Click **Get Started** to begin initialization

There are many reasons you might have issues installing ComfyUI. Maybe a network connection failed when installing pytorch (15 GB). Or you don’t have git installed. The maintenance page automatically opens when it detects an issue and provides a way to resolve the issue.

You can use it to resolve most issues:

- Create a python virtual environment
- Reinstall all missing core dependencies to your Python virtual environment that’s managed by Desktop
- Install git, VC redis
- Choose a new install location

The default maintenance page displays the current error content

Clicking `All` allows you to view all the content that can be operated on currently

2

Select GPU

The three options are:

1. **Nvidia GPU (Recommended):** Direct support for pytorch and CUDA
2. **Manual Configuration:** You need to manually install and configure the python runtime environment. Don’t select this unless you know how to configure
3. **Enable CPU Mode:** For developers and special cases only. Don’t select this unless you’re sure you need it

Unless there are special circumstances, please select **NVIDIA** as shown and click **Next** to proceed

3

Install location

In this step, you will select the installation location for the following ComfyUI content:

- **Python Environment**
- **Models Model Files**
- **Custom Nodes Custom Nodes**

Recommendations:

- Please select a **solid-state drive** as the installation location, which will increase ComfyUI’s performance when accessing models.
- Please create a separate empty folder as the ComfyUI installation directory
- Please ensure that the corresponding disk has at least around **15G** of disk space to ensure the installation of ComfyUI Desktop

Not all files are installed in this directory, some files will still be installed on the C drive, and if you need to uninstall in the future, you can refer to the uninstallation section of this guide to complete the full uninstallation of ComfyUI Desktop

After completing this step, click **Next** to proceed to the next step

4

Migrate from Existing Installation (Optional)

In this step you can migrate your existing ComfyUI installation content to ComfyUI Desktop. As shown, I selected my original **D:\\ComfyUI\_windows\_portable\\ComfyUI** installation directory. The installer will automatically recognize:

- **User Files**
- **Models:** Will not be copied, only linked with desktop version
- **Custom Nodes:** Nodes will be reinstalled

Don’t worry, this step won’t copy model files. You can check or uncheck options as needed. Click **Next** to continue

5

Desktop Settings

These are preference settings:

1. **Automatic Updates:** Whether to set automatic updates when ComfyUI updates are available
2. **Usage Metrics:** If enabled, we will collect **anonymous usage data** to help improve ComfyUI
3. **Mirror Settings:** Since the program needs internet access to download Python and complete environment installation, if you see a red ❌ during installation indicating this may cause installation failure, please follow the steps below

Expand the mirror settings to find the specific failing mirror. In this screenshot the error is **Python Install Mirror** failure.

For different mirror errors, you can refer to the following content to try to manually find different mirrors and replace them

The following cases mainly apply to users in China.

#### [​](http://docs.comfy.org#python-installation-mirror) Python Installation Mirror

If the default mirror is unavailable, please try using the mirror below.

```plaintext
https://python-standalone.org/mirror/astral-sh/python-build-standalone
```

If you need to find other alternative GitHub mirror addresses, please look for and construct a mirror address pointing to the releases of the `python-build-standalone` repository.

```plaintext
https://github.com/astral-sh/python-build-standalone/releases/download
```

Build a link in the following pattern

```plaintext
https://xxx/astral-sh/python-build-standalone/releases/download
```

#### [​](http://docs.comfy.org#pypi-mirror) PyPI Mirror

- Alibaba Cloud: [https://mirrors.aliyun.com/pypi/simple/](https://mirrors.aliyun.com/pypi/simple/)
- Tencent Cloud: [https://mirrors.cloud.tencent.com/pypi/simple/](https://mirrors.cloud.tencent.com/pypi/simple/)
- University of Science and Technology of China: [https://pypi.mirrors.ustc.edu.cn/simple/](https://pypi.mirrors.ustc.edu.cn/simple/)
- Shanghai Jiao Tong University: [https://pypi.sjtu.edu.cn/simple/](https://pypi.sjtu.edu.cn/simple/)

#### [​](http://docs.comfy.org#torch-mirror) Torch Mirror

- Aliyun: [https://mirrors.aliyun.com/pytorch-wheels/cu121/](https://mirrors.aliyun.com/pytorch-wheels/cu121/)

6

Complete the installation

If everything is correct, the installer will complete and automatically enter the ComfyUI Desktop interface, then the installation is successful

## [​](http://docs.comfy.org#first-image-generation) First Image Generation

After successful installation, you can refer to the section below to start your ComfyUI journey~

[**First Image Generation**  
\
This tutorial will guide you through your first model installation and text-to-image generation](http://docs.comfy.org/get_started/first_generation)

## [​](http://docs.comfy.org#how-to-update-comfyui-desktop) How to Update ComfyUI Desktop

Currently, ComfyUI Desktop updates use automatic detection updates, please ensure that automatic updates are enabled in the settings

You can also choose to manually check for available updates in the `Menu` —&gt; `Help` —&gt; `Check for Updates`

## [​](http://docs.comfy.org#how-to-uninstall-comfyui-desktop) How to Uninstall ComfyUI Desktop

For **ComfyUI Desktop** you can use the system uninstall function in Windows Settings to complete software uninstallation

If you want to completely remove all **ComfyUI Desktop** files, you can manually delete these folders:

- C:\\Users&lt;your username&gt;\\AppData\\Local@comfyorgcomfyui-electron-updater
- C:\\Users&lt;your username&gt;\\AppData\\Local\\Programs@comfyorgcomfyui-electron
- C:\\Users&lt;your username&gt;\\AppData\\Roaming\\ComfyUI

The above operations will not delete your following folders. If you need to delete corresponding files, please delete manually:

- models files
- custom nodes
- input/output directories

## [​](http://docs.comfy.org#troubleshooting) Troubleshooting

### [​](http://docs.comfy.org#display-unsupported-devices) Display unsupported devices

Since ComfyUI Desktop (Windows) only supports **NVIDIA GPUs with CUDA**, you may see this screen if your device is not supported

- Please switch to a supported device
- Or consider using [ComfyUI Portable](http://docs.comfy.org/installation/comfyui_portable_windows) or through [manual installation](http://docs.comfy.org/installation/manual_install) to use ComfyUI

### [​](http://docs.comfy.org#%E2%80%8Berror-identification%E2%80%8B) ​Error identification​

If installation fails, you should see the following screen

It is recommended to take these steps to find the error cause:

1. Click `Show Terminal` to view error output
2. Click `Open Logs` to view installation logs
3. Visit official forum to search for error reports
4. Click `Reinstall` to try reinstalling

Before submitting feedback, it’s recommended to provide the **error output** and **log files** to tools like **GPT**

As shown above, ask the GPT for the cause of the corresponding error, or remove ComfyUI completely and retry the installation.

### [​](http://docs.comfy.org#feedback-installation-failure) Feedback Installation Failure

If you encounter any errors during installation, please check if there are similar error reports or submit errors to us through:

- Github Issues: [https://github.com/Comfy-Org/desktop/issues](https://github.com/Comfy-Org/desktop/issues)
- Comfy Official Forum: [https://forum.comfy.org/](https://forum.comfy.org/)

When submitting error reports, please ensure you include the following logs and configuration files to help us locate and investigate the issue:

1. Log Files

FilenameDescriptionLocationmain.logContains logs related to desktop application and server startup from the Electron processcomfyui.logContains logs related to ComfyUI normal operation, such as core ComfyUI process terminal output

2. Configuration Files

FilenameDescriptionLocationextra\_models\_config.yamlContains additional paths where ComfyUI will search for models and custom nodesconfig.jsonContains application configuration. This file should not be edited directly

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/installation/desktop/windows.mdx)

[Previous](http://docs.comfy.org/installation/system_requirements)

[MacOS Desktop VersionThis article introduces how to download, install and use ComfyUI Desktop for MacOS  
\
Next](http://docs.comfy.org/installation/desktop/macos)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [ComfyUI Desktop (Windows) Download](http://docs.comfy.org#comfyui-desktop-windows-download)
- [ComfyUI Desktop Installation Steps](http://docs.comfy.org#comfyui-desktop-installation-steps)
- [ComfyUI Desktop Initialization Process](http://docs.comfy.org#comfyui-desktop-initialization-process)
- [First Image Generation](http://docs.comfy.org#first-image-generation)
- [How to Update ComfyUI Desktop](http://docs.comfy.org#how-to-update-comfyui-desktop)
- [How to Uninstall ComfyUI Desktop](http://docs.comfy.org#how-to-uninstall-comfyui-desktop)
- [Troubleshooting](http://docs.comfy.org#troubleshooting)
- [Display unsupported devices](http://docs.comfy.org#display-unsupported-devices)
- [​Error identification​](http://docs.comfy.org#%E2%80%8Berror-identification%E2%80%8B)
- [Feedback Installation Failure](http://docs.comfy.org#feedback-installation-failure)