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

Ideogram V2 - ComfyUI Built-in Node Documentation

# Ideogram V2 - ComfyUI Built-in Node Documentation

Node for creating high-quality images and text rendering using Ideogram V2 API

The Ideogram V2 node allows you to generate more refined images using Ideogram’s second-generation AI model, with significant improvements in text rendering, image quality, and overall aesthetics.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the content to generateturbobooleanFalseWhether to use turbo mode (faster generation, possibly lower quality)

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionaspect\_ratiodropdown”1:1”Image aspect ratio, effective when resolution is set to “Auto”resolutiondropdown”Auto”Output image resolution, if not set to “Auto”, it will override the aspect\_ratio settingmagic\_prompt\_optiondropdown”AUTO”Determines whether to use MagicPrompt feature during generation, options are \[“AUTO”, “ON”, “OFF”]seedinteger0Random seed value, range 0-2147483647style\_typedropdown”NONE”Generation style type (V2 only), options are \[“AUTO”, “GENERAL”, “REALISTIC”, “DESIGN”, “RENDER\_3D”, “ANIME”]negative\_promptstring""Specifies elements you don’t want to appear in the imagenum\_imagesinteger1Number of images to generate, range 1-8

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image(s)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated on 2025-05-03)]

```python

class IdeogramV2(ComfyNodeABC):
    """
    Generates images synchronously using the Ideogram V2 model.

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
                        "tooltip": "The aspect ratio for image generation. Ignored if resolution is not set to AUTO.",
                    },
                ),
                "resolution": (
                    IO.COMBO,
                    {
                        "options": list(V1_V1_RES_MAP.keys()),
                        "default": "Auto",
                        "tooltip": "The resolution for image generation. If not set to AUTO, this overrides the aspect_ratio setting.",
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
                "style_type": (
                    IO.COMBO,
                    {
                        "options": ["AUTO", "GENERAL", "REALISTIC", "DESIGN", "RENDER_3D", "ANIME"],
                        "default": "NONE",
                        "tooltip": "Style type for generation (V2 only)",
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
                #"color_palette": (
                #    IO.STRING,
                #    {
                #        "multiline": False,
                #        "default": "",
                #        "tooltip": "Color palette preset name or hex colors with weights",
                #    },
                #),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = (IO.IMAGE,)
    FUNCTION = "api_call"
    CATEGORY = "api node/image/ideogram/v2"
    DESCRIPTION = cleandoc(__doc__ or "")
    API_NODE = True

    def api_call(
        self,
        prompt,
        turbo=False,
        aspect_ratio="1:1",
        resolution="Auto",
        magic_prompt_option="AUTO",
        seed=0,
        style_type="NONE",
        negative_prompt="",
        num_images=1,
        color_palette="",
        auth_token=None,
    ):
        aspect_ratio = V1_V2_RATIO_MAP.get(aspect_ratio, None)
        resolution = V1_V1_RES_MAP.get(resolution, None)
        # Determine the model based on turbo setting
        model = "V_2_TURBO" if turbo else "V_2"

        # Handle resolution vs aspect_ratio logic
        # If resolution is not AUTO, it overrides aspect_ratio
        final_resolution = None
        final_aspect_ratio = None

        if resolution != "AUTO":
            final_resolution = resolution
        else:
            final_aspect_ratio = aspect_ratio if aspect_ratio != "ASPECT_1_1" else None

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
                    aspect_ratio=final_aspect_ratio,
                    resolution=final_resolution,
                    magic_prompt_option=(
                        magic_prompt_option if magic_prompt_option != "AUTO" else None
                    ),
                    style_type=style_type if style_type != "NONE" else None,
                    negative_prompt=negative_prompt if negative_prompt else None,
                    color_palette=color_palette if color_palette else None,
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

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/ideogram/ideogram-v2.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-replace-background)

[Ideogram V3Node for creating top-quality images and text rendering using Ideogram's latest V3 API  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v3)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)