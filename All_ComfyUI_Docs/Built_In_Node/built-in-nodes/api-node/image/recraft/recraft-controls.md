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

Recraft Controls - ComfyUI Native Node Documentation

# Recraft Controls - ComfyUI Native Node Documentation

Node providing advanced control parameters for Recraft image generation

The Recraft Controls node lets you define control parameters (like colors and background colors) to guide Recraft’s image generation process. This node combines multiple control inputs into a unified control object.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptioncolorsRecraft ColorColor controls for image generationbackground\_colorRecraft ColorBackground color control

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionrecraft\_controlsRecraft ControlsControl config object for Recraft generation nodes

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Recraft Text to Image Workflow Example**  
\
Recraft Text to Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/recraft/recraft-text-to-image)

## [​](http://docs.comfy.org#how-it-works) How It Works

Node process:

1. Collects input control parameters (colors and background\_color)
2. Combines these parameters into a structured control object
3. Outputs this control object for connecting to Recraft generation nodes

When connected to Recraft generation nodes, these control parameters influence the AI generation process. The AI considers multiple factors beyond just the text prompt’s semantic content. If color inputs are configured, the AI will try to use these colors appropriately in the generated image.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python
class RecraftControlsNode:
    """
    Create Recraft Controls for customizing Recraft generation.
    """

    RETURN_TYPES = (RecraftIO.CONTROLS,)
    RETURN_NAMES = ("recraft_controls",)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "create_controls"
    CATEGORY = "api node/image/Recraft"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
            },
            "optional": {
                "colors": (RecraftIO.COLOR,),
                "background_color": (RecraftIO.COLOR,),
            }
        }

    def create_controls(self, colors: RecraftColorChain=None, background_color: RecraftColorChain=None):
        return (RecraftControls(colors=colors, background_color=background_color), )

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/recraft-controls.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-logo-raster)

[Recraft Replace BackgroundA Recraft API node that automatically detects foreground subjects and replaces backgrounds  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-replace-background)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)