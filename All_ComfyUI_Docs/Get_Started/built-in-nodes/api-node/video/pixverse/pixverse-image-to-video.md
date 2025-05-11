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

PixVerse Image to Video - ComfyUI Native Node Documentation

# PixVerse Image to Video - ComfyUI Native Node Documentation

A node that converts static images to dynamic videos using PixVerse AI

The PixVerse Image to Video node uses PixVerse’s API to transform static images into dynamic videos. It preserves the visual features of the original image while adding natural motion based on text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionimageImage-Input image to convert to videopromptString""Text prompt describing video motion/contentnegative\_promptString""Elements to avoid in the videoseedInteger-1Random seed (-1 for random)qualitySelect”high”Output video quality levelaspect\_ratioSelect”r16\_9”Output video aspect ratiodurationSelect”seconds\_4”Length of generated videomotion\_modeSelect”standard”Video motion style

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionpixverse\_templatePIXVERSE\_TEMPLATENoneOptional PixVerse template

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-05)]

```python
class PixverseImageToVideoNode(ComfyNodeABC):
    """
    Pixverse Image to Video

    Generates videos from an image and prompts.
    """

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "image": ("IMAGE",),
                "prompt": ("STRING", {"multiline": True, "default": ""}),
                "negative_prompt": ("STRING", {"multiline": True, "default": ""}),
                "seed": ("INT", {"default": -1, "min": -1, "max": 0xffffffffffffffff}),
                "quality": (list(PixverseQuality.__members__.keys()), {"default": "high"}),
                "aspect_ratio": (list(PixverseAspectRatio.__members__.keys()), {"default": "r16_9"}),
                "duration": (list(PixverseDuration.__members__.keys()), {"default": "seconds_4"}),
                "motion_mode": (list(PixverseMotionMode.__members__.keys()), {"default": "standard"}),
            },
            "optional": {
                "pixverse_template": ("PIXVERSE_TEMPLATE",),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    RETURN_TYPES = ("VIDEO",)
    DESCRIPTION = "Generates videos from an image and prompts using Pixverse's API"
    FUNCTION = "generate_video"
    CATEGORY = "api node/video/Pixverse"
    API_NODE = True
    OUTPUT_NODE = True
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pixverse/pixverse-image-to-video.mdx)

[Previous  
\
PixVerse Transition VideoCreate smooth transition videos between start and end frames using PixVerse AI](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-transition-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)