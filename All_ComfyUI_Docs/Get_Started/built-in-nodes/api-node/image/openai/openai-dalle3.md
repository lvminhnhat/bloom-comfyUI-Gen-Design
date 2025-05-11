[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
  
  - BFL
  - Luma
  - Recraft
  - Ideogram
  - Stability AI
  - OpenAI
    
    - [OpenAI GPT Image 1](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-gpt-image1)
    - [OpenAI DALL·E 2](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-dalle2)
    - [OpenAI DALL·E 3](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-dalle3)
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

OpenAI DALL·E 3 - ComfyUI Native Node Documentation

# OpenAI DALL·E 3 - ComfyUI Native Node Documentation

Node for generating high-quality images using OpenAI’s DALL·E 3 model

This node connects to OpenAI’s DALL·E 3 API, allowing users to generate high-quality images through detailed text prompts. DALL·E 3 is OpenAI’s image generation model that offers significantly improved image quality, more accurate prompt understanding, and better detail rendering compared to previous versions.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#input-parameters) Input Parameters

ParameterTypeDefaultDescriptionpromptstring""Detailed text prompt describing what to generateseedinteger0Final result is not related to seed, this parameter only determines whether to re-executequalityselection”standard”Image quality, options: “standard” or “hd”styleselection”natural”Visual style, options: “natural” or “vivid”. “Vivid” makes the model tend to create more surreal and dramatic images, while “natural” generates more realistic, less surreal imagessizeselection”1024x1024”Output image size, options: “1024x1024”, “1024x1792”, or “1792x1024”

### [​](http://docs.comfy.org#output-parameters) Output Parameters

OutputTypeDescriptionIMAGEimageThe generated image result

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class OpenAIDalle3(ComfyNodeABC):
    """
    Generates images synchronously via OpenAI's DALL·E 3 endpoint.

    Uses the proxy at /proxy/openai/images/generations. Returned URLs are short‑lived,
    so download or cache results if you need to keep them.
    """

    def __init__(self):
        pass

    @classmethod
    def INPUT_TYPES(cls) -> InputTypeDict:
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Text prompt for DALL·E",
                    },
                ),
            },
            "optional": {
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 2**31 - 1,
                        "step": 1,
                        "display": "number",
                        "control_after_generate": True,
                        "tooltip": "not implemented yet in backend",
                    },
                ),
                "quality": (
                    IO.COMBO,
                    {
                        "options": ["standard", "hd"],
                        "default": "standard",
                        "tooltip": "Image quality",
                    },
                ),
                "style": (
                    IO.COMBO,
                    {
                        "options": ["natural", "vivid"],
                        "default": "natural",
                        "tooltip": "Vivid causes the model to lean towards generating hyper-real and dramatic images. Natural causes the model to produce more natural, less hyper-real looking images.",
                    },
                ),
                "size": (
                    IO.COMBO,
                    {
                        "options": ["1024x1024", "1024x1792", "1792x1024"],
                        "default": "1024x1024",
                        "tooltip": "Image size",
                    },
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = (IO.IMAGE,)
    FUNCTION = "api_call"
    CATEGORY = "api node/image/openai"
    DESCRIPTION = cleandoc(__doc__ or "")
    API_NODE = True

    def api_call(
        self,
        prompt,
        seed=0,
        style="natural",
        quality="standard",
        size="1024x1024",
        auth_token=None,
    ):
        model = "dall-e-3"

        # build the operation
        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/openai/images/generations",
                method=HttpMethod.POST,
                request_model=OpenAIImageGenerationRequest,
                response_model=OpenAIImageGenerationResponse,
            ),
            request=OpenAIImageGenerationRequest(
                model=model,
                prompt=prompt,
                quality=quality,
                size=size,
                style=style,
                seed=seed,
            ),
            auth_token=auth_token,
        )

        response = operation.execute()

        img_tensor = validate_and_cast_response(response)
        return (img_tensor,)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/openai/openai-dalle3.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-dalle2)

[MiniMax Image to VideoA node that converts static images to dynamic videos using MiniMax AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-image-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Input Parameters](http://docs.comfy.org#input-parameters)
- [Output Parameters](http://docs.comfy.org#output-parameters)
- [Source Code](http://docs.comfy.org#source-code)