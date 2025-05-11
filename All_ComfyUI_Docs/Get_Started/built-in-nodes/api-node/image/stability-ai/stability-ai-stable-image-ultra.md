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
    
    - [Stability Stable Image Ultra](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-image-ultra)
    - [Stability AI SD 3.5 Image](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-diffusion-3-5-image)
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

Stability Stable Image Ultra - ComfyUI Native Node Documentation

# Stability Stable Image Ultra - ComfyUI Native Node Documentation

A node that generates high-quality images using Stability AI’s ultra stable diffusion model

The Stability Stable Image Ultra node uses Stability AI’s Stable Diffusion Ultra API to generate high-quality images. It supports both text-to-image and image-to-image generation, creating detailed and artistic visuals from text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptstring""Text description of what you want to generate. Better results come from clear, descriptive prompts that specify elements, colors and themes. You can control word importance using `(word:weight)` format, where weight is 0-1. For example: `The sky was (blue:0.3) and (green:0.8)` makes the sky more green than blue.aspect\_ratioselect”1:1”Width to height ratio of output imagestyle\_presetselect”None”Optional preset style for generated imageseedinteger0Random seed for noise generation (0-4294967294)

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionimageimage-Input image for image-to-image generationnegative\_promptstring""Describes what you don’t want in the output image. This is an advanced featureimage\_denoisefloat0.5Denoising strength for input image (0.0-1.0). 0.0 keeps input image unchanged, 1.0 is like having no input image

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image

## [​](http://docs.comfy.org#notes) Notes

- image\_denoise has no effect when no input image is provided
- No preset style is applied when style\_preset is “None”
- For image-to-image, input images are converted to the proper format before API submission

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class StabilityStableImageUltraNode:
    """
    Generates images synchronously based on prompt and resolution.
    """

    RETURN_TYPES = (IO.IMAGE,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/image/stability"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "What you wish to see in the output image. A strong, descriptive prompt that clearly defines" +
                                    "What you wish to see in the output image. A strong, descriptive prompt that clearly defines" +
                                    "elements, colors, and subjects will lead to better results. " +
                                    "To control the weight of a given word use the format `(word:weight)`," +
                                    "where `word` is the word you'd like to control the weight of and `weight`" +
                                    "is a value between 0 and 1. For example: `The sky was a crisp (blue:0.3) and (green:0.8)`" +
                                    "would convey a sky that was blue and green, but more green than blue."
                    },
                ),
                "aspect_ratio": ([x.value for x in StabilityAspectRatio],
                    {
                        "default": StabilityAspectRatio.ratio_1_1,
                        "tooltip": "Aspect ratio of generated image.",
                    },
                ),
                "style_preset": (get_stability_style_presets(),
                    {
                        "tooltip": "Optional desired style of generated image.",
                    },
                ),
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 4294967294,
                        "control_after_generate": True,
                        "tooltip": "The random seed used for creating the noise.",
                    },
                ),
            },
            "optional": {
                "image": (IO.IMAGE,),
                "negative_prompt": (
                    IO.STRING,
                    {
                        "default": "",
                        "forceInput": True,
                        "tooltip": "A blurb of text describing what you do not wish to see in the output image. This is an advanced feature."
                    },
                ),
                "image_denoise": (
                    IO.FLOAT,
                    {
                        "default": 0.5,
                        "min": 0.0,
                        "max": 1.0,
                        "step": 0.01,
                        "tooltip": "Denoise of input image; 0.0 yields image identical to input, 1.0 is as if no image was provided at all.",
                    },
                ),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    def api_call(self, prompt: str, aspect_ratio: str, style_preset: str, seed: int,
                 negative_prompt: str=None, image: torch.Tensor = None, image_denoise: float=None,
                 auth_token=None):
        # prepare image binary if image present
        image_binary = None
        if image is not None:
            image_binary = tensor_to_bytesio(image, 1504 * 1504).read()
        else:
            image_denoise = None

        if not negative_prompt:
            negative_prompt = None
        if style_preset == "None":
            style_preset = None

        files = {
            "image": image_binary
        }

        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/stability/v2beta/stable-image/generate/ultra",
                method=HttpMethod.POST,
                request_model=StabilityStableUltraRequest,
                response_model=StabilityStableUltraResponse,
            ),
            request=StabilityStableUltraRequest(
                prompt=prompt,
                negative_prompt=negative_prompt,
                aspect_ratio=aspect_ratio,
                seed=seed,
                strength=image_denoise,
                style_preset=style_preset,
            ),
            files=files,
            content_type="multipart/form-data",
            auth_token=auth_token,
        )
        response_api = operation.execute()

        if response_api.finish_reason != "SUCCESS":
            raise Exception(f"Stable Image Ultra generation failed: {response_api.finish_reason}.")

        image_data = base64.b64decode(response_api.image)
        returned_image = bytesio_to_image_tensor(BytesIO(image_data))

        return (returned_image,)


```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-image-ultra.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v1)

[Stability AI SD 3.5 ImageA node that generates high-quality images using Stability AI Stable Diffusion 3.5 model  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-diffusion-3-5-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Notes](http://docs.comfy.org#notes)
- [Source Code](http://docs.comfy.org#source-code)