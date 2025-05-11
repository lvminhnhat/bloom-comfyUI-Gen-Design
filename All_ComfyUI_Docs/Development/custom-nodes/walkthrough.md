[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Development

##### ComfyUI Server

- [Server Overview](http://docs.comfy.org/essentials/comfyui-server/comms_overview)
- [Messages](http://docs.comfy.org/essentials/comfyui-server/comms_messages)
- [Execution Model Inversion Guide](http://docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide)

##### CLI

- [Getting Started](http://docs.comfy.org/comfy-cli/getting-started)
- [Reference](http://docs.comfy.org/comfy-cli/reference)

##### Develop Custom Nodes

- [Overview](http://docs.comfy.org/custom-nodes/overview)
- [Getting Started](http://docs.comfy.org/custom-nodes/walkthrough)
- Backend
- UI
- [Workflow templates](http://docs.comfy.org/custom-nodes/workflow_templates)
- [Tips](http://docs.comfy.org/custom-nodes/tips)

##### Registry

- [Overview](http://docs.comfy.org/registry/overview)
- [Publishing Nodes](http://docs.comfy.org/registry/publishing)
- [Standards](http://docs.comfy.org/registry/standards)
- [Custom Node CI/CD](http://docs.comfy.org/registry/cicd)
- [pyproject.toml](http://docs.comfy.org/registry/specifications)
- [](http://docs.comfy.org/)

##### Specifications

- Workflow JSON
- Node Definitions

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

Getting Started

# Getting Started

This page will take you step-by-step through the process of creating a custom node.

Our example will take a batch of images, and return one of the images. Initially, the node will return the image which is, on average, the lightest in color; we’ll then extend it to have a range of selection criteria, and then finally add some client side code.

This page assumes very little knowledge of Python or Javascript.

After this walkthrough, dive into the details of [backend code](http://docs.comfy.org/backend/server_overview), and [frontend code](http://docs.comfy.org/backend/server_overview).

## [​](http://docs.comfy.org#write-a-basic-node) Write a basic node

### [​](http://docs.comfy.org#prerequisites) Prerequisites

- A working ComfyUI [installation](http://docs.comfy.org/installation/manual_install). For development, we recommend installing ComfyUI manually.
- A working comfy-cli [installation](http://docs.comfy.org/comfy-cli/getting-started).

### [​](http://docs.comfy.org#setting-up) Setting up

```bash
cd ComfyUI/custom_nodes
comfy node scaffold
```

After answering a few questions, you’ll have a new directory set up.

```bash
 ~  % comfy node scaffold
You've downloaded .cookiecutters/cookiecutter-comfy-extension before. Is it okay to delete and re-download it? [y/n] (y): y
  [1/9] full_name (): Comfy
  [2/9] email (you@gmail.com): me@comfy.org
  [3/9] github_username (your_github_username): comfy
  [4/9] project_name (My Custom Nodepack): FirstComfyNode
  [5/9] project_slug (firstcomfynode): 
  [6/9] project_short_description (A collection of custom nodes for ComfyUI): 
  [7/9] version (0.0.1): 
  [8/9] Select open_source_license
    1 - GNU General Public License v3
    2 - MIT license
    3 - BSD license
    4 - ISC license
    5 - Apache Software License 2.0
    6 - Not open source
    Choose from [1/2/3/4/5/6] (1): 1
  [9/9] include_web_directory_for_custom_javascript [y/n] (n): y
Initialized empty Git repository in firstcomfynode/.git/
✓ Custom node project created successfully!
```

### [​](http://docs.comfy.org#defining-the-node) Defining the node

Add the following code to the end of `src/nodes.py`:

src/nodes.py

```python
class ImageSelector:
    CATEGORY = "example"
    @classmethod    
    def INPUT_TYPES(s):
        return { "required":  { "images": ("IMAGE",), } }
    RETURN_TYPES = ("IMAGE",)
    FUNCTION = "choose_image"
```

The basic structure of a custom node is described in detail [here](http://docs.comfy.org/custom-nodes/backend/server_overview).

A custom node is defined using a Python class, which must include these four things: `CATEGORY`, which specifies where in the add new node menu the custom node will be located, `INPUT_TYPES`, which is a class method defining what inputs the node will take (see [later](http://docs.comfy.org/custom-nodes/backend/server_overview#input-types) for details of the dictionary returned), `RETURN_TYPES`, which defines what outputs the node will produce, and `FUNCTION`, the name of the function that will be called when the node is executed.

Notice that the data type for input and output is `IMAGE` (singular) even though we expect to receive a batch of images, and return just one. In Comfy, `IMAGE` means image batch, and a single image is treated as a batch of size 1.

### [​](http://docs.comfy.org#the-main-function) The main function

The main function, `choose_image`, receives named arguments as defined in `INPUT_TYPES`, and returns a `tuple` as defined in `RETURN_TYPES`. Since we’re dealing with images, which are internally stored as `torch.Tensor`,

```python
import torch
```

Then add the function to your class. The datatype for image is `torch.Tensor` with shape `[B,H,W,C]`, where `B` is the batch size and `C` is the number of channels - 3, for RGB. If we iterate over such a tensor, we will get a series of `B` tensors of shape `[H,W,C]`. The `.flatten()` method turns this into a one dimensional tensor, of length `H*W*C`, `torch.mean()` takes the mean, and `.item()` turns a single value tensor into a Python float.

```python
def choose_image(self, images):
    brightness = list(torch.mean(image.flatten()).item() for image in images)
    brightest = brightness.index(max(brightness))
    result = images[brightest].unsqueeze(0)
    return (result,)
```

Notes on those last two lines:

- `images[brightest]` will return a Tensor of shape `[H,W,C]`. `unsqueeze` is used to insert a (length 1) dimension at, in this case, dimension zero, to give us `[B,H,W,C]` with `B=1`: a single image.
- in `return (result,)`, the trailing comma is essential to ensure you return a tuple.

### [​](http://docs.comfy.org#register-the-node) Register the node

To make Comfy recognize the new node, it must be available at the package level. Modify the `NODE_CLASS_MAPPINGS` variable at the end of `src/nodes.py`. You must restart ComfyUI to see any changes.

src/nodes.py

```python

NODE_CLASS_MAPPINGS = {
    "Example" : Example,
    "Image Selector" : ImageSelector,
}

# Optionally, you can rename the node in the `NODE_DISPLAY_NAME_MAPPINGS` dictionary.
NODE_DISPLAY_NAME_MAPPINGS = {
    "Example": "Example Node",
    "Image Selector": "Image Selector",
}
```

For a detailed explanation of how ComfyUI discovers and loads custom nodes, see the [node lifecycle documentation](http://docs.comfy.org/custom-nodes/backend/lifecycle).

## [​](http://docs.comfy.org#add-some-options) Add some options

That node is maybe a bit boring, so we might add some options; a widget that allows you to choose the brightest image, or the reddest, bluest, or greenest. Edit your `INPUT_TYPES` to look like:

```python
@classmethod    
def INPUT_TYPES(s):
    return { "required":  { "images": ("IMAGE",), 
                            "mode": (["brightest", "reddest", "greenest", "bluest"],)} }
```

Then update the main function. We’ll use a fairly naive definition of ‘reddest’ as being the average `R` value of the pixels divided by the average of all three colors. So:

```python
def choose_image(self, images, mode):
    batch_size = images.shape[0]
    brightness = list(torch.mean(image.flatten()).item() for image in images)
    if (mode=="brightest"):
        scores = brightness
    else:
        channel = 0 if mode=="reddest" else (1 if mode=="greenest" else 2)
        absolute = list(torch.mean(image[:,:,channel].flatten()).item() for image in images)
        scores = list( absolute[i]/(brightness[i]+1e-8) for i in range(batch_size) )
    best = scores.index(max(scores))
    result = images[best].unsqueeze(0)
    return (result,)
```

## [​](http://docs.comfy.org#tweak-the-ui) Tweak the UI

Maybe we’d like a bit of visual feedback, so let’s send a little text message to be displayed.

### [​](http://docs.comfy.org#send-a-message-from-server) Send a message from server

This requires two lines to be added to the Python code:

```python
from server import PromptServer
```

and, at the end of the `choose_image` method, add a line to send a message to the front end (`send_sync` takes a message type, which should be unique, and a dictionary)

```python
PromptServer.instance.send_sync("example.imageselector.textmessage", {"message":f"Picked image {best+1}"})
return (result,)
```

### [​](http://docs.comfy.org#write-a-client-extension) Write a client extension

To add some Javascript to the client, create a subdirectory, `web/js` in your custom node directory, and modify the end of `__init__.py` to tell Comfy about it by exporting `WEB_DIRECTORY`:

```python
WEB_DIRECTORY = "./web/js"
__all__ = ['NODE_CLASS_MAPPINGS', 'WEB_DIRECTORY']
```

The client extension is saved as a `.js` file in the `web/js` subdirectory, so create `image_selector/web/js/imageSelector.js` with the code below. (For more, see [client side coding](http://docs.comfy.org/js/javascript_overview)).

```javascript
app.registerExtension({
	name: "example.imageselector",
    async setup() {
        function messageHandler(event) { alert(event.detail.message); }
        app.api.addEventListener("example.imageselector.textmessage", messageHandler);
    },
})
```

All we’ve done is register an extension and add a listener for the message type we are sending in the `setup()` method. This reads the dictionary we sent (which is stored in `event.detail`).

Stop the Comfy server, start it again, reload the webpage, and run your workflow.

### [​](http://docs.comfy.org#the-complete-example) The complete example

The complete example is available [here](https://gist.github.com/robinjhuang/fbf54b7715091c7b478724fc4dffbd03). You can download the example workflow [JSON file](https://github.com/Comfy-Org/docs/blob/main/public/workflow.json) or view it below:

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/walkthrough.mdx)

[Previous](http://docs.comfy.org/custom-nodes/overview)

[PropertiesProperties of a custom node  
\
Next](http://docs.comfy.org/custom-nodes/backend/server_overview)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Write a basic node](http://docs.comfy.org#write-a-basic-node)
- [Prerequisites](http://docs.comfy.org#prerequisites)
- [Setting up](http://docs.comfy.org#setting-up)
- [Defining the node](http://docs.comfy.org#defining-the-node)
- [The main function](http://docs.comfy.org#the-main-function)
- [Register the node](http://docs.comfy.org#register-the-node)
- [Add some options](http://docs.comfy.org#add-some-options)
- [Tweak the UI](http://docs.comfy.org#tweak-the-ui)
- [Send a message from server](http://docs.comfy.org#send-a-message-from-server)
- [Write a client extension](http://docs.comfy.org#write-a-client-extension)
- [The complete example](http://docs.comfy.org#the-complete-example)