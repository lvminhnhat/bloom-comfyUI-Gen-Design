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

Luma Text to Video - ComfyUI Native Node Documentation

# Luma Text to Video - ComfyUI Native Node Documentation

A node that converts text descriptions to videos using Luma AI

The Luma Text to Video node lets you create high-quality, smooth videos from text descriptions using Luma AI’s video generation technology.

## [​](http://docs.comfy.org#node-function) Node Function

This node connects to Luma AI’s text-to-video API, allowing users to generate dynamic video content from detailed text prompts.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the video content to generatemodelselect-Video generation model to useaspect\_ratioselect”ratio\_16\_9”Video aspect ratioresolutionselect”res\_540p”Video resolutiondurationselect-Video length optionsloopbooleanFalseWhether to loop the videoseedinteger0Seed value for node rerun, results are nondeterministic

When using Ray 1.6 model, duration and resolution parameters will not take effect.

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionluma\_conceptsLUMA\_CONCEPTSCamera concepts to control motion via Luma Concepts node

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Luma Text to Video Workflow Example**  
\
Luma Text to Video Workflow Example](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-video)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class LumaTextToVideoGenerationNode(ComfyNodeABC):
    """
    Generates videos synchronously based on prompt and output_size.
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
                "aspect_ratio": (
                    [ratio.value for ratio in LumaAspectRatio],
                    {
                        "default": LumaAspectRatio.ratio_16_9,
                    },
                ),
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
        aspect_ratio: str,
        resolution: str,
        duration: str,
        loop: bool,
        seed,
        luma_concepts: LumaConceptChain = None,
        auth_token=None,
        **kwargs,
    ):
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
                resolution=resolution,
                aspect_ratio=aspect_ratio,
                duration=duration,
                loop=loop,
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

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/luma/luma-text-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-t2v)

[Luma Image to VideoA node that converts static images to dynamic videos using Luma AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Source Code](http://docs.comfy.org#source-code)