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

Images, Latents, and Masks

# Images, Latents, and Masks

When working with these datatypes, you will need to know about the `torch.Tensor` class. Complete documentation is [here](https://pytorch.org/docs/stable/tensors.html), or an introduction to the key concepts required for Comfy [here](http://docs.comfy.org/tensors).

If your node has a single output which is a tensor, remember to return `(image,)` not `(image)`

Most of the concepts below are illustrated in the [example code snippets](http://docs.comfy.org/snippets).

## [​](http://docs.comfy.org#images) Images

An IMAGE is a `torch.Tensor` with shape `[B,H,W,C]`, `C=3`. If you are going to save or load images, you will need to convert to and from `PIL.Image` format - see the code snippets below! Note that some `pytorch` operations offer (or expect) `[B,C,H,W]`, known as ‘channel first’, for reasons of computational efficiency. Just be careful.

### [​](http://docs.comfy.org#working-with-pil-image) Working with PIL.Image

If you want to load and save images, you’ll want to use PIL:

```python
from PIL import Image, ImageOps
```

## [​](http://docs.comfy.org#masks) Masks

A MASK is a `torch.Tensor` with shape `[B,H,W]`. In many contexts, masks have binary values (0 or 1), which are used to indicate which pixels should undergo specific operations. In some cases values between 0 and 1 are used indicate an extent of masking, (for instance, to alter transparency, adjust filters, or composite layers).

### [​](http://docs.comfy.org#masks-from-the-load-image-node) Masks from the Load Image Node

The `LoadImage` node uses an image’s alpha channel (the “A” in “RGBA”) to create MASKs. The values from the alpha channel are normalized to the range \[0,1] (torch.float32) and then inverted. The `LoadImage` node always produces a MASK output when loading an image. Many images (like JPEGs) don’t have an alpha channel. In these cases, `LoadImage` creates a default mask with the shape `[1, 64, 64]`.

### [​](http://docs.comfy.org#understanding-mask-shapes) Understanding Mask Shapes

In libraries like `numpy`, `PIL`, and many others, single-channel images (like masks) are typically represented as 2D arrays, shape `[H,W]`. This means the `C` (channel) dimension is implicit, and thus unlike IMAGE types, batches of MASKs have only three dimensions: `[B, H, W]`. It is not uncommon to encounter a mask which has had the `B` dimension implicitly squeezed, giving a tensor `[H,W]`.

To use a MASK, you will often have to match shapes by unsqueezing to produce a shape `[B,H,W,C]` with `C=1` To unsqueezing the `C` dimension, so you should `unsqueeze(-1)`, to unsqueeze `B`, you `unsqueeze(0)`. If your node receives a MASK as input, you would be wise to always check `len(mask.shape)`.

## [​](http://docs.comfy.org#latents) Latents

A LATENT is a `dict`; the latent sample is referenced by the key `samples` and has shape `[B,C,H,W]`, with `C=4`.

LATENT is channel first, IMAGE is channel last

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/images_and_masks.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/datatypes)

[Hidden and Flexible inputs  
\
Next](http://docs.comfy.org/custom-nodes/backend/more_on_inputs)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Images](http://docs.comfy.org#images)
- [Working with PIL.Image](http://docs.comfy.org#working-with-pil-image)
- [Masks](http://docs.comfy.org#masks)
- [Masks from the Load Image Node](http://docs.comfy.org#masks-from-the-load-image-node)
- [Understanding Mask Shapes](http://docs.comfy.org#understanding-mask-shapes)
- [Latents](http://docs.comfy.org#latents)