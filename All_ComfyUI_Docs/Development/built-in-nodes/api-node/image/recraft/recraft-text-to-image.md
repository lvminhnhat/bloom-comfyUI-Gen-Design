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

Recraft Text to Image - ComfyUI Built-in Node Documentation

# Recraft Text to Image - ComfyUI Built-in Node Documentation

A Recraft API node that generates high-quality images from text descriptions

The Recraft Text to Image node lets you generate high-quality images from text prompts by directly connecting to Recraft AI’s image generation API to create images in various styles.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text description for the imagesizeselect1024x1024Output image sizenint1Number of images (1-6)seedint0Random seed value

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionrecraft\_styleRecraft StyleImage style setting, default is “realistic photo”negative\_promptstringElements to exclude from generationrecraft\_controlsRecraft ControlsAdditional control parameters (colors, etc.)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image(s)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python
class RecraftTextToImageNode:
    """
    Generates images synchronously based on prompt and resolution.
    """

    RETURN_TYPES = (IO.IMAGE,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/image/Recraft"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Prompt for the image generation.",
                    },
                ),
                "size": (
                    [res.value for res in RecraftImageSize],
                    {
                        "default": RecraftImageSize.res_1024x1024,
                        "tooltip": "The size of the generated image.",
                    },
                ),
                "n": (
                    IO.INT,
                    {
                        "default": 1,
                        "min": 1,
                        "max": 6,
                        "tooltip": "The number of images to generate.",
                    },
                ),
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 0xFFFFFFFFFFFFFFFF,
                        "control_after_generate": True,
                        "tooltip": "Seed to determine if node should re-run; actual results are nondeterministic regardless of seed.",
                    },
                ),
            },
            "optional": {
                "recraft_style": (RecraftIO.STYLEV3,),
                "negative_prompt": (
                    IO.STRING,
                    {
                        "default": "",
                        "forceInput": True,
                        "tooltip": "An optional text description of undesired elements on an image.",
                    },
                ),
                "recraft_controls": (
                    RecraftIO.CONTROLS,
                    {
                        "tooltip": "Optional additional controls over the generation via the Recraft Controls node."
                    },
                ),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    def api_call(
        self,
        prompt: str,
        size: str,
        n: int,
        seed,
        recraft_style: RecraftStyle = None,
        negative_prompt: str = None,
        recraft_controls: RecraftControls = None,
        auth_token=None,
        **kwargs,
    ):
        default_style = RecraftStyle(RecraftStyleV3.realistic_image)
        if recraft_style is None:
            recraft_style = default_style

        controls_api = None
        if recraft_controls:
            controls_api = recraft_controls.create_api_model()

        if not negative_prompt:
            negative_prompt = None

        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/recraft/image_generation",
                method=HttpMethod.POST,
                request_model=RecraftImageGenerationRequest,
                response_model=RecraftImageGenerationResponse,
            ),
            request=RecraftImageGenerationRequest(
                prompt=prompt,
                negative_prompt=negative_prompt,
                model=RecraftModel.recraftv3,
                size=size,
                n=n,
                style=recraft_style.style,
                substyle=recraft_style.substyle,
                style_id=recraft_style.style_id,
                controls=controls_api,
            ),
            auth_token=auth_token,
        )
        response: RecraftImageGenerationResponse = operation.execute()
        images = []
        for data in response.data:
            image = bytesio_to_image_tensor(
                download_url_to_bytesio(data.url, timeout=1024)
            )
            if len(image.shape) < 4:
                image = image.unsqueeze(0)
            images.append(image)
        output_image = torch.cat(images, dim=0)

        return (output_image,)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/recraft-text-to-image.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-color-rgb)

[Recraft Image InpaintingSelectively modify image regions using Recraft API  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-inpainting)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)