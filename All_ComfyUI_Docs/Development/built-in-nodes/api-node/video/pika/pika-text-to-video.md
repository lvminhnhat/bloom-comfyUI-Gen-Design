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

Pika 2.2 Text to Video - ComfyUI Native Node Documentation

# Pika 2.2 Text to Video - ComfyUI Native Node Documentation

A node that converts text descriptions into videos using Pika AI

The Pika 2.2 Text to Video node uses Pika’s 2.2 API to create videos from text descriptions. It connects to Pika’s text-to-video API, allowing users to generate videos using text prompts with various control parameters.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionprompt\_textString""Text prompt describing the video contentnegative\_promptString""Elements to exclude from the videoseedInteger0Random seed for generationresolutionSelect”1080p”Output video resolutiondurationSelect”5s”Length of generated videoaspect\_ratioFloat1.7777777777777777Video aspect ratio, range 0.4-2.5, step 0.001

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-05)]

```python

class PikaTextToVideoNodeV2_2(PikaNodeBase):
    """Pika 2.2 Text to Video Node."""

    @classmethod
    def INPUT_TYPES(cls):
        return {
            "required": {
                **cls.get_base_inputs_types(PikaBodyGenerate22T2vGenerate22T2vPost),
                "aspect_ratio": model_field_to_node_input(
                    IO.FLOAT,
                    PikaBodyGenerate22T2vGenerate22T2vPost,
                    "aspectRatio",
                    step=0.001,
                    min=0.4,
                    max=2.5,
                    default=1.7777777777777777,
                ),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    RETURN_TYPES = ("VIDEO",)
    DESCRIPTION = "Sends a text prompt to the Pika API v2.2 to generate a video."

    def api_call(
        self,
        prompt_text: str,
        negative_prompt: str,
        seed: int,
        resolution: str,
        duration: int,
        aspect_ratio: float,
        auth_token: Optional[str] = None,
    ) -> tuple[VideoFromFile]:
        """API call for Pika 2.2 Text to Video."""
        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=PATH_TEXT_TO_VIDEO,
                method=HttpMethod.POST,
                request_model=PikaBodyGenerate22T2vGenerate22T2vPost,
                response_model=PikaGenerateResponse,
            ),
            request=PikaBodyGenerate22T2vGenerate22T2vPost(
                promptText=prompt_text,
                negativePrompt=negative_prompt,
                seed=seed,
                resolution=resolution,
                duration=duration,
                aspectRatio=aspect_ratio,
            ),
            auth_token=auth_token,
            content_type="application/x-www-form-urlencoded",
        )

        return self.execute_task(initial_operation, auth_token)


```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pika/pika-text-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)

[Pika 2.2 ScenesA node that creates coherent scene videos from multiple images using Pika AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-scenes)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)