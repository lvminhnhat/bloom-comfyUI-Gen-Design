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

Working with torch.Tensor

# Working with torch.Tensor

## [​](http://docs.comfy.org#pytorch%2C-tensors%2C-and-torch-tensor) pytorch, tensors, and torch.Tensor

All the core number crunching in Comfy is done by [pytorch](https://pytorch.org/). If your custom nodes are going to get into the guts of stable diffusion you will need to become familiar with this library, which is way beyond the scope of this introduction.

However, many custom nodes will need to manipulate images, latents and masks, each of which are represented internally as `torch.Tensor`, so you’ll want to bookmark the [documentation for torch.Tensor](https://pytorch.org/docs/stable/tensors.html).

### [​](http://docs.comfy.org#what-is-a-tensor%3F) What is a Tensor?

`torch.Tensor` represents a tensor, which is the mathematical generalization of a vector or matrix to any number of dimensions. A tensor’s *rank* is the number of dimensions it has (so a vector has *rank* 1, a matrix *rank* 2); its *shape* describes the size of each dimension.

So an RGB image (of height H and width W) might be thought of as three arrays (one for each color channel), each measuring H x W, which could be represented as a tensor with *shape* `[H,W,3]`. In Comfy images almost always come in a batch (even if the batch only contains a single image). `torch` always places the batch dimension first, so Comfy images have *shape* `[B,H,W,3]`, generally written as `[B,H,W,C]` where C stands for Channels.

### [​](http://docs.comfy.org#squeeze%2C-unsqueeze%2C-and-reshape) squeeze, unsqueeze, and reshape

If a tensor has a dimension of size 1 (known as a collapsed dimension), it is equivalent to the same tensor with that dimension removed (a batch with 1 image is just an image). Removing such a collapsed dimension is referred to as squeezing, and inserting one is known as unsqueezing.

Some torch code, and some custom node authors, will return a squeezed tensor when a dimension is collapsed - such as when a batch has only one member. This is a common cause of bugs!

To represent the same data in a different shape is referred to as reshaping. This often requires you to know the underlying data structure, so handle with care!

### [​](http://docs.comfy.org#important-notation) Important notation

`torch.Tensor` supports most Python slice notation, iteration, and other common list-like operations. A tensor also has a `.shape` attribute which returns its size as a `torch.Size` (which is a subclass of `tuple` and can be treated as such).

There are some other important bits of notation you’ll often see (several of these are less common standard Python notation, seen much more frequently when dealing with tensors)

- `torch.Tensor` supports the use of `None` in slice notation to indicate the insertion of a dimension of size 1.
- `:` is frequently used when slicing a tensor; this simply means ‘keep the whole dimension’. It’s like using `a[start:end]` in Python, but omitting the start point and end point.
- `...` represents ‘the whole of an unspecified number of dimensions’. So `a[0, ...]` would extract the first item from a batch regardless of the number of dimensions.
- in methods which require a shape to be passed, it is often passed as a `tuple` of the dimensions, in which a single dimension can be given the size `-1`, indicating that the size of this dimension should be calculated based on the total size of the data.

```python
>>> a = torch.Tensor((1,2))
>>> a.shape
torch.Size([2])
>>> a[:,None].shape 
torch.Size([2, 1])
>>> a.reshape((1,-1)).shape
torch.Size([1, 2])
```

### [​](http://docs.comfy.org#elementwise-operations) Elementwise operations

Many binary on `torch.Tensor` (including ’+’, ’-’, ’\*’, ’/’ and ’==’) are applied elementwise (independantly applied to each element). The operands must be *either* two tensors of the same shape, *or* a tensor and a scalar. So:

```python
>>> import torch
>>> a = torch.Tensor((1,2))
>>> b = torch.Tensor((3,2))
>>> a*b
tensor([3., 4.])
>>> a/b
tensor([0.3333, 1.0000])
>>> a==b
tensor([False,  True])
>>> a==1
tensor([ True, False])
>>> c = torch.Tensor((3,2,1)) 
>>> a==c
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: The size of tensor a (2) must match the size of tensor b (3) at non-singleton dimension 0
```

### [​](http://docs.comfy.org#tensor-truthiness) Tensor truthiness

The ‘truthiness’ value of a Tensor is not the same as that of Python lists.

You may be familiar with the truthy value of a Python list as `True` for any non-empty list, and `False` for `None` or `[]`. By contrast A `torch.Tensor` (with more than one elements) does not have a defined truthy value. Instead you need to use `.all()` or `.any()` to combine the elementwise truthiness:

```python
>>> a = torch.Tensor((1,2))
>>> print("yes" if a else "no")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: Boolean value of Tensor with more than one value is ambiguous
>>> a.all()
tensor(False)
>>> a.any()
tensor(True)
```

This also means that you need to use `if a is not None:` not `if a:` to determine if a tensor variable has been set.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/tensors.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/snippets)

[Javascript Extensions  
\
Next](http://docs.comfy.org/custom-nodes/js/javascript_overview)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [pytorch, tensors, and torch.Tensor](http://docs.comfy.org#pytorch%2C-tensors%2C-and-torch-tensor)
- [What is a Tensor?](http://docs.comfy.org#what-is-a-tensor%3F)
- [squeeze, unsqueeze, and reshape](http://docs.comfy.org#squeeze%2C-unsqueeze%2C-and-reshape)
- [Important notation](http://docs.comfy.org#important-notation)
- [Elementwise operations](http://docs.comfy.org#elementwise-operations)
- [Tensor truthiness](http://docs.comfy.org#tensor-truthiness)