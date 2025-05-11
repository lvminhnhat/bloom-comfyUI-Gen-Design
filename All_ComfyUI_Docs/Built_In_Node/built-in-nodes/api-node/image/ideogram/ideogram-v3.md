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

Ideogram V3 - ComfyUI Native Node Documentation

# Ideogram V3 - ComfyUI Native Node Documentation

Node for creating top-quality images and text rendering using Ideogram’s latest V3 API

This node connects to the Ideogram V3 API to perform image generation tasks.

Currently, this node supports two image generation modes:

- **Text-to-Image Mode** - Generate new images from text prompts
- **Inpainting Mode** - Regenerate specific areas by providing an original image and mask

### [​](http://docs.comfy.org#text-to-image-mode) Text-to-Image Mode

This is the default mode, activated when no image or mask inputs are provided. Simply provide a prompt and the desired parameters:

1. Describe the image you want in the prompt field
2. Select an appropriate aspect ratio or resolution
3. Adjust other parameters like magic prompt, seed, and rendering quality
4. Run the node to generate the image

### [​](http://docs.comfy.org#inpainting-mode) Inpainting Mode

**Important Note**: This mode requires both image and mask inputs. If only one is provided, the node will throw an error.

1. Connect the original image to the `image` input port
2. Create a mask with the same dimensions as the original image, where white areas represent parts to be regenerated
3. Connect the mask to the `mask` input port
4. Describe what you want to generate in the masked area in the prompt
5. Run the node to perform local editing

## [​](http://docs.comfy.org#parameter-descriptions) Parameter Descriptions

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the content to generateaspect\_ratiocombo”1:1”Image aspect ratio (text-to-image mode only)resolutioncombo”Auto”Image resolution, overrides aspect ratio when setmagic\_prompt\_optioncombo”AUTO”Magic prompt enhancement: AUTO, ON, or OFFseedint0Random seed value, 0 for random generationnum\_imagesint1Number of images to generate (1-8)rendering\_speedcombo”BALANCED”Rendering speed: BALANCED, TURBO, or QUALITY

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionimageimageInput image for inpainting mode (**must be provided with mask**)maskmaskMask for inpainting, white areas will be replaced (**must be provided with image**)

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageGenerated image

## [​](http://docs.comfy.org#how-it-works) How It Works

The Ideogram V3 node uses state-of-the-art AI models to process user input, capable of understanding complex design intentions and text layout requirements. It supports two main modes:

1. **Generation Mode**: Creates new images from text prompts
2. **Edit Mode**: Uses original image + mask combination, replacing only the areas specified by the mask

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class IdeogramV3(ComfyNodeABC):
    """
    Generates images synchronously using the Ideogram V3 model.

    Supports both regular image generation from text prompts and image editing with mask.
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
                        "tooltip": "Prompt for the image generation or editing",
                    },
                ),
            },
            "optional": {
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
                "aspect_ratio": (
                    IO.COMBO,
                    {
                        "options": list(V3_RATIO_MAP.keys()),
                        "default": "1:1",
                        "tooltip": "The aspect ratio for image generation. Ignored if resolution is not set to Auto.",
                    },
                ),
                "resolution": (
                    IO.COMBO,
                    {
                        "options": V3_RESOLUTIONS,
                        "default": "Auto",
                        "tooltip": "The resolution for image generation. If not set to Auto, this overrides the aspect_ratio setting.",
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
                "num_images": (
                    IO.INT,
                    {"default": 1, "min": 1, "max": 8, "step": 1, "display": "number"},
                ),
                "rendering_speed": (
                    IO.COMBO,
                    {
                        "options": ["BALANCED", "TURBO", "QUALITY"],
                        "default": "BALANCED",
                        "tooltip": "Controls the trade-off between generation speed and quality",
                    },
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = (IO.IMAGE,)
    FUNCTION = "api_call"
    CATEGORY = "api node/image/ideogram/v3"
    DESCRIPTION = cleandoc(__doc__ or "")
    API_NODE = True

    def api_call(
        self,
        prompt,
        image=None,
        mask=None,
        resolution="Auto",
        aspect_ratio="1:1",
        magic_prompt_option="AUTO",
        seed=0,
        num_images=1,
        rendering_speed="BALANCED",
        auth_token=None,
    ):
        # Check if both image and mask are provided for editing mode
        if image is not None and mask is not None:
            # Edit mode
            path = "/proxy/ideogram/ideogram-v3/edit"

            # Process image and mask
            input_tensor = image.squeeze().cpu()

            # Validate mask dimensions match image
            if mask.shape[1:] != image.shape[1:-1]:
                raise Exception("Mask and Image must be the same size")

            # Process image
            img_np = (input_tensor.numpy() * 255).astype(np.uint8)
            img = Image.fromarray(img_np)
            img_byte_arr = io.BytesIO()
            img.save(img_byte_arr, format="PNG")
            img_byte_arr.seek(0)
            img_binary = img_byte_arr
            img_binary.name = "image.png"

            # Process mask - white areas will be replaced
            mask_np = (mask.squeeze().cpu().numpy() * 255).astype(np.uint8)
            mask_img = Image.fromarray(mask_np)
            mask_byte_arr = io.BytesIO()
            mask_img.save(mask_byte_arr, format="PNG")
            mask_byte_arr.seek(0)
            mask_binary = mask_byte_arr
            mask_binary.name = "mask.png"

            # Create edit request
            edit_request = IdeogramV3EditRequest(
                prompt=prompt,
                rendering_speed=rendering_speed,
            )

            # Add optional parameters
            if magic_prompt_option != "AUTO":
                edit_request.magic_prompt = magic_prompt_option
            if seed != 0:
                edit_request.seed = seed
            if num_images > 1:
                edit_request.num_images = num_images

            # Execute the operation for edit mode
            operation = SynchronousOperation(
                endpoint=ApiEndpoint(
                    path=path,
                    method=HttpMethod.POST,
                    request_model=IdeogramV3EditRequest,
                    response_model=IdeogramGenerateResponse,
                ),
                request=edit_request,
                files={
                    "image": img_binary,
                    "mask": mask_binary,
                },
                content_type="multipart/form-data",
                auth_token=auth_token,
            )

        elif image is not None or mask is not None:
            # If only one of image or mask is provided, raise an error
            raise Exception("Ideogram V3 image editing requires both an image AND a mask")
        else:
            # Generation mode
            path = "/proxy/ideogram/ideogram-v3/generate"

            # Create generation request
            gen_request = IdeogramV3Request(
                prompt=prompt,
                rendering_speed=rendering_speed,
            )

            # Handle resolution vs aspect ratio
            if resolution != "Auto":
                gen_request.resolution = resolution
            elif aspect_ratio != "1:1":
                v3_aspect = V3_RATIO_MAP.get(aspect_ratio)
                if v3_aspect:
                    gen_request.aspect_ratio = v3_aspect

            # Add optional parameters
            if magic_prompt_option != "AUTO":
                gen_request.magic_prompt = magic_prompt_option
            if seed != 0:
                gen_request.seed = seed
            if num_images > 1:
                gen_request.num_images = num_images

            # Execute the operation for generation mode
            operation = SynchronousOperation(
                endpoint=ApiEndpoint(
                    path=path,
                    method=HttpMethod.POST,
                    request_model=IdeogramV3Request,
                    response_model=IdeogramGenerateResponse,
                ),
                request=gen_request,
                auth_token=auth_token,
            )

        # Execute the operation and process response
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

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/ideogram/ideogram-v3.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v2)

[Ideogram V1Node for creating precise text rendering images using Ideogram API  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/ideogram/ideogram-v1)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Text-to-Image Mode](http://docs.comfy.org#text-to-image-mode)
- [Inpainting Mode](http://docs.comfy.org#inpainting-mode)
- [Parameter Descriptions](http://docs.comfy.org#parameter-descriptions)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)