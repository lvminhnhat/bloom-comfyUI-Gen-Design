[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
  
  - BFL
  - Luma
    
    - [Luma Reference](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-reference)
    - [Luma Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image)
    - [Luma Image to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-image-to-image)
  - Recraft
  - Ideogram
  - Stability AI
  - OpenAI
- Video

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

Luma Reference - ComfyUI Built-in Node Documentation

# Luma Reference - ComfyUI Built-in Node Documentation

Helper node providing reference images for Luma image generation

The Luma Reference node allows you to set reference images and weights to guide the creation process of Luma image generation nodes, making the generated images closer to specific features of the reference images.

## [​](http://docs.comfy.org#node-function) Node Function

This node works as a helper tool for Luma generation nodes, allowing users to provide reference images to influence generation results. It enables users to set the weight of reference images to control how much they affect the final result. Multiple Luma Reference nodes can be chained together, with a maximum of 4 working simultaneously according to API requirements.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionimageImage-Input image used as referenceweightFloat1.0Controls the strength of the reference image’s influence (0-1)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionluma\_refLUMA\_REFReference object containing image and weight

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Luma Text to Image Workflow Example**  
\
Luma Text to Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-image)

## [​](http://docs.comfy.org#how-it-works) How It Works

The Luma Reference node receives image input and allows setting a weight value. The node doesn’t directly generate or modify images but creates a reference object containing image data and weight information, which is then passed to Luma generation nodes.

During the generation process, Luma AI analyzes the features of the reference image and incorporates these features into the generation results based on the set weight. Higher weight values mean the generated image will be closer to the reference image’s features, while lower weight values indicate the reference image will only slightly influence the final result.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated on 2025-05-03)]

```python

class LumaReferenceNode(ComfyNodeABC):
    """
    Holds an image and weight for use with Luma Generate Image node.
    """

    RETURN_TYPES = (LumaIO.LUMA_REF,)
    RETURN_NAMES = ("luma_ref",)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "create_luma_reference"
    CATEGORY = "api node/image/Luma"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "image": (
                    IO.IMAGE,
                    {
                        "tooltip": "Image to use as reference.",
                    },
                ),
                "weight": (
                    IO.FLOAT,
                    {
                        "default": 1.0,
                        "min": 0.0,
                        "max": 1.0,
                        "step": 0.01,
                        "tooltip": "Weight of image reference.",
                    },
                ),
            },
            "optional": {"luma_ref": (LumaIO.LUMA_REF,)},
        }

    def create_luma_reference(
        self, image: torch.Tensor, weight: float, luma_ref: LumaReferenceChain = None
    ):
        if luma_ref is not None:
            luma_ref = luma_ref.clone()
        else:
            luma_ref = LumaReferenceChain()
        luma_ref.add(LumaReference(image=image, weight=round(weight, 2)))
        return (luma_ref,)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/luma/luma-reference.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/bfl/flux-pro-ultra-image)

[Luma Text to ImageA node that converts text descriptions into high-quality images using Luma AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)