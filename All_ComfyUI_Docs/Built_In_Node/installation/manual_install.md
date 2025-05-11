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

Manual Installation

# Manual Installation

For Nvidia 50 series (Blackwell) GPUs, please refer to the [System Requirements](http://docs.comfy.org/installation/nvidia-50-series) section to ensure your system meets the requirements for ComfyUI.

- Windows
- Linux
- MacOS

### [​](http://docs.comfy.org#clone-the-repository) Clone the repository

```bash
git clone git@github.com:comfyanonymous/ComfyUI.git
```

More [info](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) on git clone.

If you have not installed Microsoft Visual C++ Redistributable, please install it [here.](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)

### [​](http://docs.comfy.org#install-dependencies) Install Dependencies

1. [Install Miniconda](https://docs.anaconda.com/free/miniconda/index.html#latest-miniconda-installer-links). This will help you install the correct versions of Python and other libraries needed by ComfyUI.
   
   Create an environment with Conda.
   
   ```plaintext
   conda create -n comfyenv
   conda activate comfyenv
   ```
2. Install GPU Dependencies
   
   Nvidia
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch-nightly -c nvidia
   ```
   
   AMD
   
   ```plaintext
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.0
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.0
   ```
   
   Mac ARM Silicon
   
   ```bash
   conda install pytorch-nightly::pytorch torchvision torchaudio -c pytorch-nightly
   ```
3. ```bash
   cd ComfyUI
   pip install -r requirements.txt
   ```
4. Start the application
   
   ```plaintext
   cd ComfyUI
   python main.py
   ```

### [​](http://docs.comfy.org#clone-the-repository) Clone the repository

```bash
git clone git@github.com:comfyanonymous/ComfyUI.git
```

More [info](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) on git clone.

If you have not installed Microsoft Visual C++ Redistributable, please install it [here.](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)

### [​](http://docs.comfy.org#install-dependencies) Install Dependencies

1. [Install Miniconda](https://docs.anaconda.com/free/miniconda/index.html#latest-miniconda-installer-links). This will help you install the correct versions of Python and other libraries needed by ComfyUI.
   
   Create an environment with Conda.
   
   ```plaintext
   conda create -n comfyenv
   conda activate comfyenv
   ```
2. Install GPU Dependencies
   
   Nvidia
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch-nightly -c nvidia
   ```
   
   AMD
   
   ```plaintext
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.0
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.0
   ```
   
   Mac ARM Silicon
   
   ```bash
   conda install pytorch-nightly::pytorch torchvision torchaudio -c pytorch-nightly
   ```
3. ```bash
   cd ComfyUI
   pip install -r requirements.txt
   ```
4. Start the application
   
   ```plaintext
   cd ComfyUI
   python main.py
   ```

### [​](http://docs.comfy.org#clone-the-repository-2) Clone the repository

```bash
git clone git@github.com:comfyanonymous/ComfyUI.git
```

More [info](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) on git clone.

### [​](http://docs.comfy.org#install-dependencies-2) Install Dependencies

1. [Install Miniconda](https://docs.anaconda.com/free/miniconda/index.html#latest-miniconda-installer-links). This will help you install the correct versions of Python and other libraries needed by ComfyUI.
   
   Create an environment with Conda.
   
   ```plaintext
   conda create -n comfyenv
   conda activate comfyenv
   ```
2. Install GPU Dependencies
   
   Nvidia
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch-nightly -c nvidia
   ```
   
   AMD
   
   ```plaintext
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.0
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.0
   ```
   
   Mac ARM Silicon
   
   ```bash
   conda install pytorch-nightly::pytorch torchvision torchaudio -c pytorch-nightly
   ```
3. ```bash
   cd ComfyUI
   pip install -r requirements.txt
   ```
4. Start the application
   
   ```plaintext
   cd ComfyUI
   python main.py
   ```

### [​](http://docs.comfy.org#clone-the-repository-3) Clone the repository

Open [Terminal application](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).

```bash
git clone git@github.com:comfyanonymous/ComfyUI.git
```

More [info](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) on git clone.

### [​](http://docs.comfy.org#install-dependencies-3) Install Dependencies

1. [Install Miniconda](https://docs.anaconda.com/free/miniconda/index.html#latest-miniconda-installer-links). This will help you install the correct versions of Python and other libraries needed by ComfyUI.
   
   Create an environment with Conda.
   
   ```plaintext
   conda create -n comfyenv
   conda activate comfyenv
   ```
2. Install GPU Dependencies
   
   Nvidia
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch-nightly -c nvidia
   ```
   
   AMD
   
   ```plaintext
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.0
   ```
   
   Alternatively, you can install the nightly version of PyTorch.
   
   Install Nightly
   
   Install Nightly version (might be more risky)
   
   ```plaintext
   pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.0
   ```
   
   Mac ARM Silicon
   
   ```bash
   conda install pytorch-nightly::pytorch torchvision torchaudio -c pytorch-nightly
   ```
3. ```bash
   cd ComfyUI
   pip install -r requirements.txt
   ```
4. Start the application
   
   ```plaintext
   cd ComfyUI
   python main.py
   ```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/installation/manual_install.mdx)

[Previous](http://docs.comfy.org/installation/comfyui_portable_windows)

[First Image GenerationThis tutorial will guide you through your first image generation with ComfyUI, covering basic interface operations like workflow loading, model installation, and image generation  
\
Next](http://docs.comfy.org/get_started/first_generation)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)