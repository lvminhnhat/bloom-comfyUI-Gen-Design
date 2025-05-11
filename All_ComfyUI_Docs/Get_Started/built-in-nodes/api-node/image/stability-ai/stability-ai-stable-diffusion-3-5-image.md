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

Stability AI Stable Diffusion 3.5 - ComfyUI Native Node Documentation

# Stability AI Stable Diffusion 3.5 - ComfyUI Native Node Documentation

A node that generates high-quality images using Stability AI Stable Diffusion 3.5 model

The Stability AI Stable Diffusion 3.5 Image node uses Stability AI’s Stable Diffusion 3.5 API to generate high-quality images. It supports both text-to-image and image-to-image generation, capable of creating detailed visual content from text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptstring""What you want to see in the output image. Strong, descriptive prompts that clearly define elements, colors and themes will yield better resultsmodelselect-Choose which Stability SD 3.5 model to useaspect\_ratioselect”1:1”Width to height ratio of generated imagestyle\_presetselect”None”Optional preset style for the desired imagecfg\_scalefloat4.0How strictly the diffusion process adheres to the prompt text (higher values keep your image closer to your prompt). Range: 1.0 - 10.0, Step: 0.1seedinteger0Random seed for noise generation (0-4294967294)

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionimageimage-Input image. When provided, the node switches to image-to-image modenegative\_promptstring""Keywords of what you don’t want to see in the output image. This is an advanced featureimage\_denoisefloat0.5Denoising strength for input image. 0.0 yields image identical to input, 1.0 is as if no image was provided at all. Range: 0.0 - 1.0, Step: 0.01. Only effective when image is provided

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Stability AI Stable Diffusion 3.5 Image Workflow Example**  
\
Stability AI Stable Diffusion 3.5 Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/stability-ai/stable-diffusion-3-5-image)

## [​](http://docs.comfy.org#notes) Notes

- When an input image is provided, the node switches from text-to-image mode to image-to-image mode
- In image-to-image mode, aspect ratio parameters are ignored
- Mode selection automatically switches based on whether an image is provided:
  
  - No image provided: text-to-image mode
  - Image provided: image-to-image mode
- If style\_preset is set to “None”, no preset style will be applied

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-07)]

```python
class StabilityStableImageSD_3_5Node:
    """
    Generates images synchronously based on prompt and resolution.
    """

    RETURN_TYPES = (IO.IMAGE,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/image/Stability AI"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "What you wish to see in the output image. A strong, descriptive prompt that clearly defines elements, colors, and subjects will lead to better results."
                    },
                ),
                "model": ([x.value for x in Stability_SD3_5_Model],),
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
                "cfg_scale": (
                    IO.FLOAT,
                    {
                        "default": 4.0,
                        "min": 1.0,
                        "max": 10.0,
                        "step": 0.1,
                        "tooltip": "How strictly the diffusion process adheres to the prompt text (higher values keep your image closer to your prompt)",
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
                        "tooltip": "Keywords of what you do not wish to see in the output image. This is an advanced feature."
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

    def api_call(self, model: str, prompt: str, aspect_ratio: str, style_preset: str, seed: int, cfg_scale: float,
                 negative_prompt: str=None, image: torch.Tensor = None, image_denoise: float=None,
                 auth_token=None):
        validate_string(prompt, strip_whitespace=False)
        # prepare image binary if image present
        image_binary = None
        mode = Stability_SD3_5_GenerationMode.text_to_image
        if image is not None:
            image_binary = tensor_to_bytesio(image, total_pixels=1504*1504).read()
            mode = Stability_SD3_5_GenerationMode.image_to_image
            aspect_ratio = None
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
                path="/proxy/stability/v2beta/stable-image/generate/sd3",
                method=HttpMethod.POST,
                request_model=StabilityStable3_5Request,
                response_model=StabilityStableUltraResponse,
            ),
            request=StabilityStable3_5Request(
                prompt=prompt,
                negative_prompt=negative_prompt,
                aspect_ratio=aspect_ratio,
                seed=seed,
                strength=image_denoise,
                style_preset=style_preset,
                cfg_scale=cfg_scale,
                model=model,
                mode=mode,
            ),
            files=files,
            content_type="multipart/form-data",
            auth_token=auth_token,
        )
        response_api = operation.execute()

        if response_api.finish_reason != "SUCCESS":
            raise Exception(f"Stable Diffusion 3.5 Image generation failed: {response_api.finish_reason}.")

        image_data = base64.b64decode(response_api.image)
        returned_image = bytesio_to_image_tensor(BytesIO(image_data))

        return (returned_image,)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-diffusion-3-5-image.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/stability-ai/stability-ai-stable-image-ultra)

[OpenAI GPT Image 1Node for generating images using OpenAI's GPT-4 Vision model  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-gpt-image1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Notes](http://docs.comfy.org#notes)
- [Source Code](http://docs.comfy.org#source-code)