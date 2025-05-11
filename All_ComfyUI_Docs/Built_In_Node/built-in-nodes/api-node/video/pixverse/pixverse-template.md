[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
- Video
  
  - MiniMax
  - Google
  - Kling
  - Luma
  - Pika
  - PixVerse
    
    - [PixVerse Template](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-template)
    - [PixVerse Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-text-to-video)
    - [PixVerse Transition Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-transition-video)
    - [PixVerse Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-image-to-video)

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

PixVerse Template - ComfyUI Native Node Documentation

# PixVerse Template - ComfyUI Native Node Documentation

A helper node that provides preset templates for PixVerse video generation

The PixVerse Template node lets you choose from predefined video generation templates to control the style and effects of PixVerse video generation nodes. This helper node connects to PixVerse video generation nodes, allowing users to quickly apply preset video styles without manually adjusting complex parameter combinations.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDescriptiontemplateSelectChoose a template from available video presets

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionpixverse\_templatePixverseIO.TEMPLATEConfiguration object containing the selected template ID

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-05)]

```python

class PixverseTemplateNode:
    """
    Select template for Pixverse Video generation.
    """

    RETURN_TYPES = (PixverseIO.TEMPLATE,)
    RETURN_NAMES = ("pixverse_template",)
    FUNCTION = "create_template"
    CATEGORY = "api node/video/Pixverse"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "template": (list(pixverse_templates.keys()), ),
            }
        }

    def create_template(self, template: str):
        template_id = pixverse_templates.get(template, None)
        if template_id is None:
            raise Exception(f"Template '{template}' is not recognized.")
        # just return the integer
        return (template_id,)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pixverse/pixverse-template.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-image-to-video)

[PixVerse Text to VideoA node that converts text descriptions into videos using PixVerse AI technology  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)