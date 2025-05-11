[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
- Video
  
  - MiniMax
  - Google
  - Kling
  - Luma
  - Pika
    
    - [Pika 2.2 Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-text-to-video)
    - [Pika 2.2 Scenes](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-scenes)
    - [Pika 2.2 Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-image-to-video)
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

Pika 2.2 Image to Video - ComfyUI Native Node Documentation

# Pika 2.2 Image to Video - ComfyUI Native Node Documentation

A node that converts static images to dynamic videos using Pika AI

The Pika 2.2 Image to Video node connects to Pika’s latest 2.2 API to transform static images into dynamic videos. It preserves the visual features of the original image while adding natural motion based on text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionimageImage-Input image to convert to videoprompt\_textString""Text prompt describing video motion and contentnegative\_promptString""Elements to avoid in the videoseedInteger0Random seed for generationresolutionSelect”1080p”Output video resolutiondurationSelect”5s”Length of generated video

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#how-it-works) How It Works

The node sends the input image and parameters (prompts, resolution, duration, etc.) to Pika’s API server as multipart form data. The API processes this and returns the generated video. Users can control the output by adjusting the prompts, negative prompts, random seed and other parameters.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-05)]

```python

class PikaImageToVideoV2_2(PikaNodeBase):
    """Pika 2.2 Image to Video Node."""

    @classmethod
    def INPUT_TYPES(cls):
        return {
            "required": {
                "image": (
                    IO.IMAGE,
                    {"tooltip": "The image to convert to video"},
                ),
                **cls.get_base_inputs_types(PikaBodyGenerate22I2vGenerate22I2vPost),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    DESCRIPTION = "Sends an image and prompt to the Pika API v2.2 to generate a video."
    RETURN_TYPES = ("VIDEO",)

    def api_call(
        self,
        image: torch.Tensor,
        prompt_text: str,
        negative_prompt: str,
        seed: int,
        resolution: str,
        duration: int,
        auth_token: Optional[str] = None,
    ) -> tuple[VideoFromFile]:
        """API call for Pika 2.2 Image to Video."""
        # Convert image to BytesIO
        image_bytes_io = tensor_to_bytesio(image)
        image_bytes_io.seek(0)  # Reset stream position

        # Prepare file data for multipart upload
        pika_files = {"image": ("image.png", image_bytes_io, "image/png")}

        # Prepare non-file data using the Pydantic model
        pika_request_data = PikaBodyGenerate22I2vGenerate22I2vPost(
            promptText=prompt_text,
            negativePrompt=negative_prompt,
            seed=seed,
            resolution=resolution,
            duration=duration,
        )

        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=PATH_IMAGE_TO_VIDEO,
                method=HttpMethod.POST,
                request_model=PikaBodyGenerate22I2vGenerate22I2vPost,
                response_model=PikaGenerateResponse,
            ),
            request=pika_request_data,
            files=pika_files,
            content_type="multipart/form-data",
            auth_token=auth_token,
        )

        return self.execute_task(initial_operation, auth_token)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pika/pika-image-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-scenes)

[PixVerse TemplateA helper node that provides preset templates for PixVerse video generation  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-template)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)