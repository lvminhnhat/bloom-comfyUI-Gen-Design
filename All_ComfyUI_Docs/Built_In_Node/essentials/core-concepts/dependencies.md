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

Dependencies

# Dependencies

Understand dependencies in ComfyUI

## [​](http://docs.comfy.org#a-workflow-file-depends-on-other-files) A workflow file depends on other files

We often obtain various workflow files from the community, but frequently find that the workflow cannot run directly after loading. This is because a workflow file depends on other files besides the workflow itself, such as media asset inputs, models, custom nodes, related Python dependencies, etc. ComfyUI workflows can only run normally when all relevant dependencies are satisfied.

ComfyUI workflow dependencies mainly fall into the following categories:

- Assets (media files including audio, video, images, and other inputs)
- Custom nodes
- Python dependencies
- Models (such as Stable Diffusion models, etc.)

## [​](http://docs.comfy.org#assets) Assets

An AI model is an example of an ***asset***. In media production, an asset is some media file that supplies input data. For example, a video editing program operates on movie files stored on disk. The editing program’s project file holds links to these movie file assets, allowing non-destructive editing that doesn’t alter the original movie files.

ComfyUI works the same way. A workflow can only run if all of the required assets are found and loaded. Generative AI models, images, movies, and sounds are some examples of assets that a workflow might depend upon. These are therefore known as ***dependent assets*** or ***asset dependencies***.

## [​](http://docs.comfy.org#custom-nodes) Custom Nodes

Custom nodes are an important component of ComfyUI that extend its functionality. They are created by the community and can be installed to add new capabilities to your workflows.

## [​](http://docs.comfy.org#python-dependencies) Python Dependencies

ComfyUI is a Python-based project. We build a standalone Python environment to run ComfyUI, and all related dependencies are installed in this isolated Python environment.

### [​](http://docs.comfy.org#comfyui-dependencies) ComfyUI Dependencies

You can view ComfyUI’s current dependencies in the [requirements.txt](https://github.com/comfyanonymous/ComfyUI/blob/master/requirements.txt) file:

```text
comfyui-frontend-package==1.14.5
torch
torchsde
torchvision
torchaudio
numpy>=1.25.0
einops
transformers>=4.28.1
tokenizers>=0.13.3
sentencepiece
safetensors>=0.4.2
aiohttp>=3.11.8
yarl>=1.18.0
pyyaml
Pillow
scipy
tqdm
psutil

#non essential dependencies:
kornia>=0.7.1
spandrel
soundfile
av
```

As ComfyUI evolves, we may adjust dependencies accordingly, such as adding new dependencies or removing ones that are no longer needed. So if you use Git to update ComfyUI, you need to run the following command in the corresponding environment after pulling the latest updates:

```bash
pip install -r requirements.txt
```

This ensures that ComfyUI’s dependencies are up to date for proper operation. You can also modify specific package dependency versions to upgrade or downgrade certain dependencies.

Additionally, ComfyUI’s frontend [ComfyUI\_frontend](https://github.com/Comfy-Org/ComfyUI_frontend) is currently maintained as a separate project. We update the `comfyui-frontend-package` dependency version after the corresponding version stabilizes. If you need to switch to a different frontend version, you can check the version information [here](https://pypi.org/project/comfyui-frontend-package/#history).

### [​](http://docs.comfy.org#custom-node-dependencies) Custom Node Dependencies

Thanks to the efforts of many authors in the ComfyUI community, we can extend ComfyUI’s functionality by using different custom nodes, enabling impressive creativity.

Typically, each custom node has its own dependencies and a separate `requirements.txt` file. If you use [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager) to install custom nodes, ComfyUI Manager will usually automatically install the corresponding dependencies.

There are also cases where you need to install dependencies manually. Currently, all custom nodes are installed in the `ComfyUI/custom_nodes` directory.

You need to navigate to the corresponding plugin directory in your ComfyUI Python environment and run `pip install -r requirements.txt` to install the dependencies.

If you’re using the [Windows Portable version](http://docs.comfy.org/installation/comfyui_portable_windows), you can use the following command in the `ComfyUI_windows_portable` directory:

```plaintext
python_embeded\python.exe -m pip install -r ComfyUI\custom_nodes\<custom_node_name>\requirements.txt
```

to install the dependencies for the corresponding node.

### [​](http://docs.comfy.org#dependency-conflicts) Dependency Conflicts

Dependency conflicts are a common issue when using ComfyUI. You might find that after installing or updating a custom node, previously installed custom nodes can no longer be found in ComfyUI’s node library, or error pop-ups appear. One possible reason is dependency conflicts.

There can be many reasons for dependency conflicts, such as:

1. Custom node version locking

Some plugins may fix the exact version of a dependency library (e.g., `open_clip_torch==2.26.1`), while other plugins may require a higher version (e.g., `open_clip_torch>=2.29.0`), making it impossible to satisfy both version requirements simultaneously.

**Solution**: You can try changing the fixed version dependency to a range constraint, such as `open_clip_torch>=2.26.1`, and then reinstall the dependencies to resolve these issues.

2. Environment pollution

During the installation of custom node dependencies, it may overwrite versions of libraries already installed by other plugins. For example, multiple plugins may depend on `PyTorch` but require different CUDA versions, and the later installed plugin will break the existing environment.

**Solutions**:

- You can try manually installing specific versions of dependencies in the Python virtual environment to resolve such issues.
- Or create different Python virtual environments for different plugins to resolve these issues.
- Try installing plugins one by one, restarting ComfyUI after each installation to observe if dependency conflicts occur.

<!--THE END-->

3. Custom node dependency versions incompatible with ComfyUI dependency versions

These types of dependency conflicts may be more difficult to resolve, and you may need to upgrade/downgrade ComfyUI or change the dependency versions of custom nodes to resolve these issues.

**Solution**: These types of dependency conflicts may be more difficult to resolve, and you may need to upgrade/downgrade ComfyUI or change the dependency versions of custom nodes to resolve these issues.

## [​](http://docs.comfy.org#models) Models

Models are a significant asset dependency for ComfyUI. Various custom nodes and workflows are built around specific models, such as the Stable Diffusion series, Flux series, Ltxv, and others. These models are an essential foundation for creation with ComfyUI, so we need to ensure that the models we use are properly available. Typically, our models are saved in the corresponding directory under `ComfyUI/models/`. Of course, you can also create an [extra\_model\_paths.yaml](https://github.com/comfyanonymous/ComfyUI/blob/master/extra_model_paths.yaml.example) by modifying the template to make additional model paths recognized by ComfyUI. This allows multiple ComfyUI instances to share the same model library, reducing disk usage.

## [​](http://docs.comfy.org#software) Software

An advanced application like ComfyUI also has ***software dependencies***. These are libraries of programming code and data that are required for the application to run. Custom nodes are examples of software dependencies. On an even more fundamental level, the Python programming environment is the ultimate dependency for ComfyUI. The correct version of Python is required to run a particular version of ComfyUI. Updates to Python, ComfyUI, and custom nodes can all be handled from the **ComfyUI Manager** window.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/core-concepts/dependencies.mdx)

[Previous](http://docs.comfy.org/essentials/core-concepts/models)

[ShortcutsKeyboard and mouse shortcuts for ComfyUI and related settings  
\
Next](http://docs.comfy.org/interface/shortcuts)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [A workflow file depends on other files](http://docs.comfy.org#a-workflow-file-depends-on-other-files)
- [Assets](http://docs.comfy.org#assets)
- [Custom Nodes](http://docs.comfy.org#custom-nodes)
- [Python Dependencies](http://docs.comfy.org#python-dependencies)
- [ComfyUI Dependencies](http://docs.comfy.org#comfyui-dependencies)
- [Custom Node Dependencies](http://docs.comfy.org#custom-node-dependencies)
- [Dependency Conflicts](http://docs.comfy.org#dependency-conflicts)
- [Models](http://docs.comfy.org#models)
- [Software](http://docs.comfy.org#software)