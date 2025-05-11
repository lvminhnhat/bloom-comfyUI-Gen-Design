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
  
  - [Properties](http://docs.comfy.org/custom-nodes/backend/server_overview)
  - [Lifecycle](http://docs.comfy.org/custom-nodes/backend/lifecycle)
  - [Publishing to the Manager](http://docs.comfy.org/custom-nodes/backend/manager)
  - [Datatypes](http://docs.comfy.org/custom-nodes/backend/datatypes)
  - [Images, Latents, and Masks](http://docs.comfy.org/custom-nodes/backend/images_and_masks)
  - [Hidden and Flexible inputs](http://docs.comfy.org/custom-nodes/backend/more_on_inputs)
  - [Lazy Evaluation](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation)
  - [Node Expansion](http://docs.comfy.org/custom-nodes/backend/expansion)
  - [Data lists](http://docs.comfy.org/custom-nodes/backend/lists)
  - [Annotated Examples](http://docs.comfy.org/custom-nodes/backend/snippets)
  - [Working with torch.Tensor](http://docs.comfy.org/custom-nodes/backend/tensors)
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

Data lists

# Data lists

## [​](http://docs.comfy.org#length-one-processing) Length one processing

Internally, the Comfy server represents data flowing from one node to the next as a Python `list`, normally length 1, of the relevant datatype. In normal operation, when a node returns an output, each element in the output `tuple` is separately wrapped in a list (length 1); then when the next node is called, the data is unwrapped and passed to the main function.

You generally don’t need to worry about this, since Comfy does the wrapping and unwrapping.

This isn’t about batches. A batch (of, for instance, latents, or images) is a *single entry* in the list (see [tensor datatypes](http://docs.comfy.org/images_and_masks))

## [​](http://docs.comfy.org#list-processing) List processing

In some circumstance, multiple data instances are processed in a single workflow, in which case the internal data will be a list containing the data instances. An example of this might be processing a series of images one at a time to avoid running out of VRAM, or handling images of different sizes.

By default, Comfy will process the values in the list sequentially:

- if the inputs are `list`s of different lengths, the shorter ones are padded by repeating the last value
- the main method is called once for each value in the input lists
- the outputs are `list`s, each of which is the same length as the longest input

The relevant code can be found in the method `map_node_over_list` in `execution.py`.

However, as Comfy wraps node outputs into a `list` of length one, if the `tuple` returned by a custom node contains a `list`, that `list` will be wrapped, and treated as a single piece of data. In order to tell Comfy that the list being returned should not be wrapped, but treated as a series of data for sequential processing, the node should provide a class attribute `OUTPUT_IS_LIST`, which is a `tuple[bool]`, of the same length as `RETURN_TYPES`, specifying which outputs which should be so treated.

A node can also override the default input behaviour and receive the whole list in a single call. This is done by setting a class attribute `INPUT_IS_LIST` to `True`.

Here’s a (lightly annotated) example from the built in nodes - `ImageRebatch` takes one or more batches of images (received as a list, because `INPUT_IS_LIST - True`) and rebatches them into batches of the requested size.

`INPUT_IS_LIST` is node level - all inputs get the same treatment. So the value of the `batch_size` widget is given by `batch_size[0]`.

```python

class ImageRebatch:
    @classmethod
    def INPUT_TYPES(s):
        return {"required": { "images": ("IMAGE",),
                              "batch_size": ("INT", {"default": 1, "min": 1, "max": 4096}) }}
    RETURN_TYPES = ("IMAGE",)
    INPUT_IS_LIST = True
    OUTPUT_IS_LIST = (True, )
    FUNCTION = "rebatch"
    CATEGORY = "image/batch"

    def rebatch(self, images, batch_size):
        batch_size = batch_size[0]    # everything comes as a list, so batch_size is list[int]

        output_list = []
        all_images = []
        for img in images:                    # each img is a batch of images
            for i in range(img.shape[0]):     # each i is a single image
                all_images.append(img[i:i+1])

        for i in range(0, len(all_images), batch_size): # take batch_size chunks and turn each into a new batch
            output_list.append(torch.cat(all_images[i:i+batch_size], dim=0))  # will die horribly if the image batches had different width or height!

        return (output_list,)
```

#### [​](http://docs.comfy.org#input-is-list) INPUT\_IS\_LIST

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/lists.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/expansion)

[Annotated Examples  
\
Next](http://docs.comfy.org/custom-nodes/backend/snippets)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Length one processing](http://docs.comfy.org#length-one-processing)
- [List processing](http://docs.comfy.org#list-processing)
- [INPUT\_IS\_LIST](http://docs.comfy.org#input-is-list)