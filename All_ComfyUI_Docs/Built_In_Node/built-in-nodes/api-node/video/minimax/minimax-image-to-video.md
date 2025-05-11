[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
- Video
  
  - MiniMax
    
    - [MiniMax Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-image-to-video)
    - [MiniMax Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-text-to-video)
  - Google
  - Kling
  - Luma
  - Pika
  - PixVerse

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

MiniMax Image to Video - ComfyUI Native Node Documentation

# MiniMax Image to Video - ComfyUI Native Node Documentation

A node that converts static images to dynamic videos using MiniMax AI

The MiniMax Image to Video node uses MiniMax’s API to generate videos from input images and text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionimageimage-Input image used as the first frame of videoprompt\_textstring""Text prompt to guide video generationmodelselect”I2V-01”Available models: “I2V-01-Director”, “I2V-01”, “I2V-01-live”

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionseedintegerRandom seed for noise generation

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class MinimaxImageToVideoNode(MinimaxTextToVideoNode):
    """
    Generates videos synchronously based on an image and prompt, and optional parameters using Minimax's API.
    """

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "image": (
                    IO.IMAGE,
                    {
                        "tooltip": "Image to use as first frame of video generation"
                    },
                ),
                "prompt_text": (
                    "STRING",
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Text prompt to guide the video generation",
                    },
                ),
                "model": (
                    [
                        "I2V-01-Director",
                        "I2V-01",
                        "I2V-01-live",
                    ],
                    {
                        "default": "I2V-01",
                        "tooltip": "Model to use for video generation",
                    },
                ),
            },
            "optional": {
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 0xFFFFFFFFFFFFFFFF,
                        "control_after_generate": True,
                        "tooltip": "The random seed used for creating the noise.",
                    },
                ),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    RETURN_TYPES = ("VIDEO",)
    DESCRIPTION = "Generates videos from an image and prompts using Minimax's API"
    FUNCTION = "generate_video"
    CATEGORY = "api node/video/Minimax"
    API_NODE = True
    OUTPUT_NODE = True
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/minimax/minimax-image-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-dalle3)

[MiniMax Text to VideoA node that converts text descriptions into videos using MiniMax AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)