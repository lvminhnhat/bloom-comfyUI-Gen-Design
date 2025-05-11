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

Annotated Examples

# Annotated Examples

A growing collection of fragments of example code…

## [​](http://docs.comfy.org#images-and-masks) Images and Masks

### [​](http://docs.comfy.org#load-an-image) Load an image

Load an image into a batch of size 1 (based on `LoadImage` source code in `nodes.py`)

```python
i = Image.open(image_path)
i = ImageOps.exif_transpose(i)
if i.mode == 'I':
    i = i.point(lambda i: i * (1 / 255))
image = i.convert("RGB")
image = np.array(image).astype(np.float32) / 255.0
image = torch.from_numpy(image)[None,]
```

### [​](http://docs.comfy.org#save-an-image-batch) Save an image batch

Save a batch of images (based on `SaveImage` source code in `nodes.py`)

```python
for (batch_number, image) in enumerate(images):
    i = 255. * image.cpu().numpy()
    img = Image.fromarray(np.clip(i, 0, 255).astype(np.uint8))
    filepath = # some path that takes the batch number into account
    img.save(filepath)
```

### [​](http://docs.comfy.org#invert-a-mask) Invert a mask

Inverting a mask is a straightforward process. Since masks are normalised to the range \[0,1]:

```python
mask = 1.0 - mask
```

### [​](http://docs.comfy.org#convert-a-mask-to-image-shape) Convert a mask to Image shape

```python
# We want [B,H,W,C] with C = 1
if len(mask.shape)==2: # we have [H,W], so insert B and C as dimension 1
    mask = mask[None,:,:,None]
elif len(mask.shape)==3 and mask.shape[2]==1: # we have [H,W,C]
    mask = mask[None,:,:,:]
elif len(mask.shape)==3:                      # we have [B,H,W]
    mask = mask[:,:,:,None]
```

### [​](http://docs.comfy.org#using-masks-as-transparency-layers) Using Masks as Transparency Layers

When used for tasks like inpainting or segmentation, the MASK’s values will eventually be rounded to the nearest integer so that they are binary — 0 indicating regions to be ignored and 1 indicating regions to be targeted. However, this doesn’t happen until the MASK is passed to those nodes. This flexibility allows you to use MASKs as as you would in digital photography contexts as a transparency layer:

```python
# Invert mask back to original transparency layer
mask = 1.0 - mask

# Unsqueeze the `C` (channels) dimension
mask = mask.unsqueeze(-1)

# Concatenate ("cat") along the `C` dimension
rgba_image = torch.cat((rgb_image, mask), dim=-1)
```

## [​](http://docs.comfy.org#noise) Noise

### [​](http://docs.comfy.org#creating-noise-variations) Creating noise variations

Here’s an example of creating a noise object which mixes the noise from two sources. This could be used to create slight noise variations by varying `weight2`.

```python
class Noise_MixedNoise:
    def __init__(self, nosie1, noise2, weight2):
        self.noise1  = noise1
        self.noise2  = noise2
        self.weight2 = weight2

    @property
    def seed(self): return self.noise1.seed

    def generate_noise(self, input_latent:torch.Tensor) -> torch.Tensor:
        noise1 = self.noise1.generate_noise(input_latent)
        noise2 = self.noise2.generate_noise(input_latent)
        return noise1 * (1.0-self.weight2) + noise2 * (self.weight2)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/snippets.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/lists)

[Working with torch.Tensor  
\
Next](http://docs.comfy.org/custom-nodes/backend/tensors)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Images and Masks](http://docs.comfy.org#images-and-masks)
- [Load an image](http://docs.comfy.org#load-an-image)
- [Save an image batch](http://docs.comfy.org#save-an-image-batch)
- [Invert a mask](http://docs.comfy.org#invert-a-mask)
- [Convert a mask to Image shape](http://docs.comfy.org#convert-a-mask-to-image-shape)
- [Using Masks as Transparency Layers](http://docs.comfy.org#using-masks-as-transparency-layers)
- [Noise](http://docs.comfy.org#noise)
- [Creating noise variations](http://docs.comfy.org#creating-noise-variations)