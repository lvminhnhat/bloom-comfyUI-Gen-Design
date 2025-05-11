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
    
    - [Ideogram V2](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v2)
    - [Ideogram V3](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3)
    - [Ideogram V1](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v1)
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

Ideogram V1 - ComfyUI Native Node Documentation

# Ideogram V1 - ComfyUI Native Node Documentation

Node for creating precise text rendering images using Ideogram API

The Ideogram V1 node allows you to generate images with high-quality text rendering capabilities using Ideogram’s text-to-image API.

## [​](http://docs.comfy.org#parameter-description) Parameter Description

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the content to generateturbobooleanFalseWhether to use turbo mode (faster but possibly lower quality)aspect\_ratioselect”1:1”Image aspect ratiomagic\_prompt\_optionselect”AUTO”Determines whether to use MagicPrompt in generation, options: AUTO, ON, OFFseedinteger0Random seed value (0-2147483647)negative\_promptstring""Specifies elements you don’t want in the imagenum\_imagesinteger1Number of images to generate (1-8)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image result

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated on 2025-05-03)]

```python
class IdeogramV1(ComfyNodeABC):
    """
    Generates images synchronously using the Ideogram V1 model.

    Images links are available for a limited period of time; if you would like to keep the image, you must download it.
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
                        "tooltip": "Prompt for the image generation",
                    },
                ),
                "turbo": (
                    IO.BOOLEAN,
                    {
                        "default": False,
                        "tooltip": "Whether to use turbo mode (faster generation, potentially lower quality)",
                    }
                ),
            },
            "optional": {
                "aspect_ratio": (
                    IO.COMBO,
                    {
                        "options": list(V1_V2_RATIO_MAP.keys()),
                        "default": "1:1",
                        "tooltip": "The aspect ratio for image generation.",
                    },
                ),
                "magic_prompt_option": (
                    IO.COMBO,
                    {
                        "options": ["AUTO", "ON", "OFF"],
                        "default": "AUTO",
                        "tooltip": "Determine if MagicPrompt should be used in generation",
                    },
                ),
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 2147483647,
                        "step": 1,
                        "control_after_generate": True,
                        "display": "number",
                    },
                ),
                "negative_prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Description of what to exclude from the image",
                    },
                ),
                "num_images": (
                    IO.INT,
                    {"default": 1, "min": 1, "max": 8, "step": 1, "display": "number"},
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = (IO.IMAGE,)
    FUNCTION = "api_call"
    CATEGORY = "api node/image/ideogram/v1"
    DESCRIPTION = cleandoc(__doc__ or "")
    API_NODE = True

    def api_call(
        self,
        prompt,
        turbo=False,
        aspect_ratio="1:1",
        magic_prompt_option="AUTO",
        seed=0,
        negative_prompt="",
        num_images=1,
        auth_token=None,
    ):
        # Determine the model based on turbo setting
        aspect_ratio = V1_V2_RATIO_MAP.get(aspect_ratio, None)
        model = "V_1_TURBO" if turbo else "V_1"

        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/ideogram/generate",
                method=HttpMethod.POST,
                request_model=IdeogramGenerateRequest,
                response_model=IdeogramGenerateResponse,
            ),
            request=IdeogramGenerateRequest(
                image_request=ImageRequest(
                    prompt=prompt,
                    model=model,
                    num_images=num_images,
                    seed=seed,
                    aspect_ratio=aspect_ratio if aspect_ratio != "ASPECT_1_1" else None,
                    magic_prompt_option=(
                        magic_prompt_option if magic_prompt_option != "AUTO" else None
                    ),
                    negative_prompt=negative_prompt if negative_prompt else None,
                )
            ),
            auth_token=auth_token,
        )

        response = operation.execute()

        if not response.data or len(response.data) == 0:
            raise Exception("No images were generated in the response")

        image_urls = [image_data.url for image_data in response.data if image_data.url]

        if not image_urls:
            raise Exception("No image URLs were generated in the response")

        return (download_and_process_images(image_urls),)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/ideogram/ideogram-v1.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3)

[Stability Stable Image UltraA node that generates high-quality images using Stability AI's ultra stable diffusion model  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-image-ultra)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameter Description](http://docs.comfy.org#parameter-description)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)