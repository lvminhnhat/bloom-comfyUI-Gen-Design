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
    
    - [Luma Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video)
    - [Luma Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video)
    - [Luma Concepts](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)
  - Pika
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

Luma Image to Video - ComfyUI Native API Node Documentation

# Luma Image to Video - ComfyUI Native API Node Documentation

A node that converts static images to dynamic videos using Luma AI

The Luma Image to Video node uses Luma AI’s technology to transform static images into smooth, dynamic videos, bringing your images to life.

## [​](http://docs.comfy.org#node-function) Node Function

This node connects to Luma AI’s image-to-video API, allowing users to create dynamic videos from input images. It understands the image content and generates natural, coherent motion while maintaining the original visual style. Combined with text prompts, users can precisely control the video’s dynamic effects.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing video motion and contentmodelselect-Video generation model to useresolutionselect”540p”Output video resolutiondurationselect-Video length optionsloopbooleanFalseWhether to loop the videoseedinteger0Seed value for node rerun, results are nondeterministic

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionfirst\_imageimageFirst frame of video (required if no last\_image)last\_imageimageLast frame of video (required if no first\_image)luma\_conceptsLUMA\_CONCEPTSConcepts for controlling camera motion and shot style

### [​](http://docs.comfy.org#requirements) Requirements

- Either **first\_image** or **last\_image** must be provided
- Each image input (first\_image and last\_image) accepts only 1 image

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Luma Image to Video Workflow Example**  
\
Luma Image to Video Workflow Tutorial](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-video)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class LumaImageToVideoGenerationNode(ComfyNodeABC):
    """
    Generates videos synchronously based on prompt, input images, and output_size.
    """

    RETURN_TYPES = (IO.VIDEO,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/video/Luma"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Prompt for the video generation",
                    },
                ),
                "model": ([model.value for model in LumaVideoModel],),
                # "aspect_ratio": ([ratio.value for ratio in LumaAspectRatio], {
                #     "default": LumaAspectRatio.ratio_16_9,
                # }),
                "resolution": (
                    [resolution.value for resolution in LumaVideoOutputResolution],
                    {
                        "default": LumaVideoOutputResolution.res_540p,
                    },
                ),
                "duration": ([dur.value for dur in LumaVideoModelOutputDuration],),
                "loop": (
                    IO.BOOLEAN,
                    {
                        "default": False,
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
                "first_image": (
                    IO.IMAGE,
                    {"tooltip": "First frame of generated video."},
                ),
                "last_image": (IO.IMAGE, {"tooltip": "Last frame of generated video."}),
                "luma_concepts": (
                    LumaIO.LUMA_CONCEPTS,
                    {
                        "tooltip": "Optional Camera Concepts to dictate camera motion via the Luma Concepts node."
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
        model: str,
        resolution: str,
        duration: str,
        loop: bool,
        seed,
        first_image: torch.Tensor = None,
        last_image: torch.Tensor = None,
        luma_concepts: LumaConceptChain = None,
        auth_token=None,
        **kwargs,
    ):
        if first_image is None and last_image is None:
            raise Exception(
                "At least one of first_image and last_image requires an input."
            )
        keyframes = self._convert_to_keyframes(first_image, last_image, auth_token)
        duration = duration if model != LumaVideoModel.ray_1_6 else None
        resolution = resolution if model != LumaVideoModel.ray_1_6 else None

        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/luma/generations",
                method=HttpMethod.POST,
                request_model=LumaGenerationRequest,
                response_model=LumaGeneration,
            ),
            request=LumaGenerationRequest(
                prompt=prompt,
                model=model,
                aspect_ratio=LumaAspectRatio.ratio_16_9,  # ignored, but still needed by the API for some reason
                resolution=resolution,
                duration=duration,
                loop=loop,
                keyframes=keyframes,
                concepts=luma_concepts.create_api_model() if luma_concepts else None,
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

        vid_response = requests.get(response_poll.assets.video)
        return (VideoFromFile(BytesIO(vid_response.content)),)

    def _convert_to_keyframes(
        self,
        first_image: torch.Tensor = None,
        last_image: torch.Tensor = None,
        auth_token=None,
    ):
        if first_image is None and last_image is None:
            return None
        frame0 = None
        frame1 = None
        if first_image is not None:
            download_urls = upload_images_to_comfyapi(
                first_image, max_images=1, auth_token=auth_token
            )
            frame0 = LumaImageReference(type="image", url=download_urls[0])
        if last_image is not None:
            download_urls = upload_images_to_comfyapi(
                last_image, max_images=1, auth_token=auth_token
            )
            frame1 = LumaImageReference(type="image", url=download_urls[0])
        return LumaKeyframes(frame0=frame0, frame1=frame1)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/luma/luma-image-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video)

[Luma ConceptsA helper node that provides concept guidance for Luma image generation  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Requirements](http://docs.comfy.org#requirements)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Source Code](http://docs.comfy.org#source-code)