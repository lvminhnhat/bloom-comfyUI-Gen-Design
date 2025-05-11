[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
  
  - BFL
  - Luma
    
    - [Luma Reference](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-reference)
    - [Luma Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image)
    - [Luma Image to Image](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-image-to-image)
  - Recraft
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

Luma Image to Image - ComfyUI Built-in Node Documentation

# Luma Image to Image - ComfyUI Built-in Node Documentation

Node for modifying images using Luma AI

The Luma Image to Image node allows you to modify existing images using Luma AI technology based on text prompts, while preserving certain features and structure of the original image.

## [​](http://docs.comfy.org#node-function) Node Function

This node connects to Luma AI’s text-to-image API, enabling users to generate images through detailed text prompts. Luma AI is known for its excellent realism and detail, particularly excelling at generating photorealistic content and artistic style images.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the content to generatemodelselect-Select which generation model to useaspect\_ratioselect16:9Set the aspect ratio of the output imageseedinteger0Seed value to determine if node should rerun, but actual results don’t depend on seedstyle\_image\_weightfloat1.0Weight of the style image, range 0.02-1.0, only effective when style\_image is provided

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

Without the following parameter inputs, the node functions in text-to-image mode

ParameterTypeDescriptionimage\_luma\_refLUMA\_REFLuma reference node connection, influences generation results through input images, can consider up to 4 imagesstyle\_imageimageStyle reference image, uses only 1 image, influences the style of generated images, adjusted through `style_image_weight`character\_imageimageAdds character features to the generated results, can be a batch of multiple images, up to 4 images

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageThe generated image

## [​](http://docs.comfy.org#usage-examples) Usage Examples

## [​](http://docs.comfy.org#how-it-works) How It Works

The Luma Image to Image node analyzes the input image and combines it with text prompts to guide the modification process. It uses Luma AI’s generation models to make creative changes to images based on prompts.

Node process:

1. First uploads the input image to ComfyAPI
2. Then sends the image URL with the prompt to Luma API
3. Waits for Luma AI to complete processing
4. Downloads and returns the generated image

The image\_weight parameter controls the degree of influence from the original image - values closer to 0 will preserve more of the original image features, while values closer to 1 allow for more substantial modifications.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated on 2025-05-05)]

```python

class LumaImageModifyNode(ComfyNodeABC):
    """
    Modifies images synchronously based on prompt and aspect ratio.
    """

    RETURN_TYPES = (IO.IMAGE,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/image/Luma"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "image": (IO.IMAGE,),
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Prompt for the image generation",
                    },
                ),
                "image_weight": (
                    IO.FLOAT,
                    {
                        "default": 1.0,
                        "min": 0.02,
                        "max": 1.0,
                        "step": 0.01,
                        "tooltip": "Weight of the image; the closer to 0.0, the less the image will be modified.",
                    },
                ),
                "model": ([model.value for model in LumaImageModel],),
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
            "optional": {},
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    def api_call(
        self,
        prompt: str,
        model: str,
        image: torch.Tensor,
        image_weight: float,
        seed,
        auth_token=None,
        **kwargs,
    ):
        # first, upload image
        download_urls = upload_images_to_comfyapi(
            image, max_images=1, auth_token=auth_token
        )
        image_url = download_urls[0]
        # next, make Luma call with download url provided
        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/luma/generations/image",
                method=HttpMethod.POST,
                request_model=LumaImageGenerationRequest,
                response_model=LumaGeneration,
            ),
            request=LumaImageGenerationRequest(
                prompt=prompt,
                model=model,
                modify_image_ref=LumaModifyImageRef(
                    url=image_url, weight=round(image_weight, 2)
                ),
            ),
            auth_token=auth_token,
        )
        response_api: LumaGeneration = operation.execute()

        operation = PollingOperation(
            poll_endpoint=ApiEndpoint(
                path=f"/proxy/luma/generations/{response_api.id}",
                method=HttpMethod.GET,
                request_model=EmptyRequest,
                response_model=LumaGeneration,
            ),
            completed_statuses=[LumaState.completed],
            failed_statuses=[LumaState.failed],
            status_extractor=lambda x: x.state,
            auth_token=auth_token,
        )
        response_poll = operation.execute()

        img_response = requests.get(response_poll.assets.image)
        img = process_image_response(img_response)
        return (img,)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/luma/luma-image-to-image.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-text-to-image)

[Save SVGA utility node for saving SVG vector graphics to files  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/save-svg)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Examples](http://docs.comfy.org#usage-examples)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)