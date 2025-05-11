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
  - PixVerse
    
    - [PixVerse Template](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-template)
    - [PixVerse Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-text-to-video)
    - [PixVerse Transition Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-transition-video)
    - [PixVerse Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-image-to-video)

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

PixVerse Text to Video - ComfyUI Built-in Node Documentation

# PixVerse Text to Video - ComfyUI Built-in Node Documentation

A node that converts text descriptions into videos using PixVerse AI technology

The PixVerse Text to Video node connects to PixVerse’s text-to-video API, allowing users to generate high-quality videos from text descriptions. Users can customize their creations by adjusting various parameters like video quality, duration, and motion mode.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptstring""Text prompt describing the video contentaspect\_ratioselect-Output video aspect ratioqualityselectPixverseQuality.res\_540pVideo quality levelduration\_secondsselect-Video durationmotion\_modeselect-Video motion modeseedinteger0Random seed for consistent generation results

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionnegative\_promptstring""Elements to exclude from the videopixverse\_templatePIXVERSE\_TEMPLATENoneOptional template for style settings

### [​](http://docs.comfy.org#limitations) Limitations

- 1080p quality only supports normal motion mode with 5-second duration
- Non 5-second durations only support normal motion mode

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-05)]

```python

class PixverseTextToVideoNode(ComfyNodeABC):
    """
    Generates videos synchronously based on prompt and output_size.
    """

    RETURN_TYPES = (IO.VIDEO,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/video/Pixverse"

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
                "aspect_ratio": (
                    [ratio.value for ratio in PixverseAspectRatio],
                ),
                "quality": (
                    [resolution.value for resolution in PixverseQuality],
                    {
                        "default": PixverseQuality.res_540p,
                    },
                ),
                "duration_seconds": ([dur.value for dur in PixverseDuration],),
                "motion_mode": ([mode.value for mode in PixverseMotionMode],),
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 2147483647,
                        "control_after_generate": True,
                        "tooltip": "Seed for video generation.",
                    },
                ),
            },
            "optional": {
                "negative_prompt": (
                    IO.STRING,
                    {
                        "default": "",
                        "forceInput": True,
                        "tooltip": "An optional text description of undesired elements on an image.",
                    },
                ),
                "pixverse_template": (
                    PixverseIO.TEMPLATE,
                    {
                        "tooltip": "An optional template to influence style of generation, created by the Pixverse Template node."
                    }
                )
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    def api_call(
        self,
        prompt: str,
        aspect_ratio: str,
        quality: str,
        duration_seconds: int,
        motion_mode: str,
        seed,
        negative_prompt: str=None,
        pixverse_template: int=None,
        auth_token=None,
        **kwargs,
    ):
        # 1080p is limited to 5 seconds duration
        # only normal motion_mode supported for 1080p or for non-5 second duration
        if quality == PixverseQuality.res_1080p:
            motion_mode = PixverseMotionMode.normal
            duration_seconds = PixverseDuration.dur_5
        elif duration_seconds != PixverseDuration.dur_5:
            motion_mode = PixverseMotionMode.normal

        operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/pixverse/video/text/generate",
                method=HttpMethod.POST,
                request_model=PixverseTextVideoRequest,
                response_model=PixverseVideoResponse,
            ),
            request=PixverseTextVideoRequest(
                prompt=prompt,
                aspect_ratio=aspect_ratio,
                quality=quality,
                duration=duration_seconds,
                motion_mode=motion_mode,
                negative_prompt=negative_prompt if negative_prompt else None,
                template_id=pixverse_template,
                seed=seed,
            ),
            auth_token=auth_token,
        )
        response_api = operation.execute()

        if response_api.Resp is None:
            raise Exception(f"Pixverse request failed: '{response_api.ErrMsg}'")

        operation = PollingOperation(
            poll_endpoint=ApiEndpoint(
                path=f"/proxy/pixverse/video/result/{response_api.Resp.video_id}",
                method=HttpMethod.GET,
                request_model=EmptyRequest,
                response_model=PixverseGenerationStatusResponse,
            ),
            completed_statuses=[PixverseStatus.successful],
            failed_statuses=[PixverseStatus.contents_moderation, PixverseStatus.failed, PixverseStatus.deleted],
            status_extractor=lambda x: x.Resp.status,
            auth_token=auth_token,
        )
        response_poll = operation.execute()

        vid_response = requests.get(response_poll.Resp.url)
        return (VideoFromFile(BytesIO(vid_response.content)),)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pixverse/pixverse-text-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-template)

[PixVerse Transition VideoCreate smooth transition videos between start and end frames using PixVerse AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pixverse/pixverse-transition-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Limitations](http://docs.comfy.org#limitations)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)