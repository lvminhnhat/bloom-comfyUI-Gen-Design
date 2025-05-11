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

OpenAI DALL·E 2 - ComfyUI Native Node Documentation

# OpenAI DALL·E 2 - ComfyUI Native Node Documentation

Node for generating images using OpenAI’s DALL·E 2 model

The OpenAI DALL·E 2 node allows you to use OpenAI’s DALL·E 2 API to generate creative images from text descriptions.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt for DALL·E to generate images, supports multi-line inputseedinteger0The result is not actually related to the seed, this parameter only determines whether to re-executesizeselect”1024x1024”Output image size, options: 256x256, 512x512, 1024x1024ninteger1Number of images to generate, range 1-8

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionimageimageNoneOptional reference image for image editingmaskmaskNoneOptional mask for inpainting (white areas will be replaced)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image(s)

## [​](http://docs.comfy.org#features) Features

- Basic function: Generate images from text prompts
- Image editing: When both image and mask parameters are provided, performs image editing (white masked areas will be replaced)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class OpenAIDalle2(ComfyNodeABC):
    """
    Generates images synchronously via OpenAI's DALL·E 2 endpoint.

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
                "size": (
                    IO.COMBO,
                    {
                        "options": ["256x256", "512x512", "1024x1024"],
                        "default": "1024x1024",
                        "tooltip": "Image size",
                    },
                ),
                "n": (
                    IO.INT,
                    {
                        "default": 1,
                        "min": 1,
                        "max": 8,
                        "step": 1,
                        "display": "number",
                        "tooltip": "How many images to generate",
                    },
                ),
                "image": (
                    IO.IMAGE,
                    {
                        "default": None,
                        "tooltip": "Optional reference image for image editing.",
                    },
                ),
                "mask": (
                    IO.MASK,
                    {
                        "default": None,
                        "tooltip": "Optional mask for inpainting (white areas will be replaced)",
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
        image=None,
        mask=None,
        n=1,
        size="1024x1024",
        auth_token=None,
    ):
        model = "dall-e-2"
        path = "/proxy/openai/images/generations"
        content_type = "application/json"
        request_class = OpenAIImageGenerationRequest
        img_binary = None

        if image is not None and mask is not None:
            path = "/proxy/openai/images/edits"
            content_type = "multipart/form-data"
            request_class = OpenAIImageEditRequest

            input_tensor = image.squeeze().cpu()
            height, width, channels = input_tensor.shape
            rgba_tensor = torch.ones(height, width, 4, device="cpu")
            rgba_tensor[:, :, :channels] = input_tensor

            if mask.shape[1:] != image.shape[1:-1]:
                raise Exception("Mask and Image must be the same size")
            rgba_tensor[:, :, 3] = 1 - mask.squeeze().cpu()

            rgba_tensor = downscale_image_tensor(rgba_tensor.unsqueeze(0)).squeeze()

            image_np = (rgba_tensor.numpy() * 255).astype(np.uint8)
            img = Image.fromarray(image_np)
            img_byte_arr = io.BytesIO()
            img.save(img_byte_arr, format="PNG")
            img_byte_arr.seek(0)
            img_binary = img_byte_arr  # .getvalue()
            img_binary.name = "image.png"
        elif image is not None or mask is not None:
            raise Exception("Dall-E 2 image editing requires an image AND a mask")

        # Build the operation
        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=path,
                method=HttpMethod.POST,
                request_model=request_class,
                response_model=OpenAIImageGenerationResponse,
            ),
            request=request_class(
                model=model,
                prompt=prompt,
                n=n,
                size=size,
                seed=seed,
            ),
            files=(
                {
                    "image": img_binary,
                }
                if img_binary
                else None
            ),
            content_type=content_type,
            auth_token=auth_token,
        )

        response = operation.execute()

        img_tensor = validate_and_cast_response(response)
        return (img_tensor,)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/openai/openai-dalle2.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-gpt-image1)

[OpenAI DALL·E 3Node for generating high-quality images using OpenAI's DALL·E 3 model  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/openai/openai-dalle3)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Features](http://docs.comfy.org#features)
- [Source Code](http://docs.comfy.org#source-code)