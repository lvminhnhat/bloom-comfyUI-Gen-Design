[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
  
  - BFL
  - Luma
  - Recraft
    
    - [Save SVG](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/save-svg)
    - [Recraft Style - Realistic Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-realistic-image)
    - [Recraft Text to Vector](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-vector)
    - [Recraft Creative Upscale](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-creative-upscale)
    - [Recraft Image to Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-to-image)
    - [Recraft Crisp Upscale](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-crisp-upscale)
    - [Recraft Color RGB](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-color-rgb)
    - [Recraft Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-image)
    - [Recraft Image Inpainting](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-inpainting)
    - [Recraft Vectorize Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-vectorize-image)
    - [Recraft Style - Digital Illustration](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-digital-illustration)
    - [Recraft Remove Background](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-remove-background)
    - [Recraft Style - Logo Raster](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-logo-raster)
    - [Recraft Controls](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-controls)
    - [Recraft Replace Background](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-replace-background)
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

Recraft Style - Realistic Image - ComfyUI Native Node Documentation

# Recraft Style - Realistic Image - ComfyUI Native Node Documentation

A helper node for setting realistic photo style in Recraft image generation

The Recraft Style - Realistic Image node helps set up realistic photo styles for Recraft image generation, with various substyle options to control the visual characteristics of generated images.

## [​](http://docs.comfy.org#node-function) Node Function

This node creates a style configuration object that guides Recraft’s image generation process towards realistic photo effects.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionsubstyleselectNoneSpecific substyle of realistic photo (Required)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionrecraft\_styleRecraft StyleStyle config object to connect to Recraft generation nodes

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Recraft Text to Image Workflow Example**  
\
Recraft Text to Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/recraft/recraft-text-to-image)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class RecraftStyleV3RealisticImageNode:
    """
    Select realistic_image style and optional substyle.
    """

    RETURN_TYPES = (RecraftIO.STYLEV3,)
    RETURN_NAMES = ("recraft_style",)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "create_style"
    CATEGORY = "api node/image/Recraft"

    RECRAFT_STYLE = RecraftStyleV3.realistic_image

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "substyle": (get_v3_substyles(s.RECRAFT_STYLE),),
            }
        }

    def create_style(self, substyle: str):
        if substyle == "None":
            substyle = None
        return (RecraftStyle(self.RECRAFT_STYLE, substyle),)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/recraft-style-realistic-image.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/save-svg)

[Recraft Text to VectorA Recraft API node that generates scalable vector graphics from text descriptions  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-vector)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Source Code](http://docs.comfy.org#source-code)