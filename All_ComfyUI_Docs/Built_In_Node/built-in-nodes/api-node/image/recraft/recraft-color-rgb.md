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

Recraft Color RGB - ComfyUI Native Node Documentation

# Recraft Color RGB - ComfyUI Native Node Documentation

Helper node for defining color controls in Recraft image generation

The Recraft Color RGB node lets you define precise RGB color values to control colors in Recraft image generation.

## [​](http://docs.comfy.org#node-function) Node Function

This node creates a color configuration object that connects to the Recraft Controls node to specify colors used in generated images.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionrinteger0Red channel (0-255)ginteger0Green channel (0-255)binteger0Blue channel (0-255)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionrecraft\_colorRecraft ColorColor config object to connect to Recraft Controls

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Recraft Text to Image Workflow Example**  
\
Recraft Text to Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/recraft/recraft-text-to-image)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python
class RecraftColorRGBNode:
    """
    Create Recraft Color by choosing specific RGB values.
    """

    RETURN_TYPES = (RecraftIO.COLOR,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    RETURN_NAMES = ("recraft_color",)
    FUNCTION = "create_color"
    CATEGORY = "api node/image/Recraft"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "r": (IO.INT, {
                    "default": 0,
                    "min": 0,
                    "max": 255,
                    "tooltip": "Red value of color."
                }),
                "g": (IO.INT, {
                    "default": 0,
                    "min": 0,
                    "max": 255,
                    "tooltip": "Green value of color."
                }),
                "b": (IO.INT, {
                    "default": 0,
                    "min": 0,
                    "max": 255,
                    "tooltip": "Blue value of color."
                }),
            },
            "optional": {
                "recraft_color": (RecraftIO.COLOR,),
            }
        }

    def create_color(self, r: int, g: int, b: int, recraft_color: RecraftColorChain=None):
        recraft_color = recraft_color.clone() if recraft_color else RecraftColorChain()
        recraft_color.add(RecraftColor(r, g, b))
        return (recraft_color, )

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/recraft-color-rgb.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-crisp-upscale)

[Recraft Text to ImageA Recraft API node that generates high-quality images from text descriptions  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Source Code](http://docs.comfy.org#source-code)