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
    
    - [Kling Camera Controls](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-controls)
    - [Kling Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-text-to-video)
    - [Kling Image to Video (Camera Control)](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-i2v)
    - [Kling Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-image-to-video)
    - [Kling Start-End Frame to Video](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-start-end-frame-to-video)
    - [Kling Text to Video (Camera Control)](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-t2v)
  - Luma
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

Kling Image to Video - ComfyUI Built-in Node

# Kling Image to Video - ComfyUI Built-in Node

A node that converts static images to dynamic videos using Kling’s AI technology

The Kling Image to Video node converts static images into dynamic video content using Kling’s image-to-video API.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

All parameters below are required:

ParameterTypeDefaultDescriptionstart\_frameImage-Input source imagepromptString""Text prompt describing video action and contentnegative\_promptString""Elements to avoid in the videocfg\_scaleFloat7.0Controls how closely to follow the promptmodel\_nameSelect”kling-v1-5”Model type to useaspect\_ratioSelect”16:9”Output video aspect ratiodurationSelect”5s”Generated video durationmodeSelect”pro”Video generation mode

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated videovideo\_idStringUnique video identifierdurationStringActual video duration

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class KlingImage2VideoNode(KlingNodeBase):
    """Kling Image to Video Node"""

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "start_frame": model_field_to_node_input(
                    IO.IMAGE, KlingImage2VideoRequest, "image"
                ),
                "prompt": model_field_to_node_input(
                    IO.STRING, KlingImage2VideoRequest, "prompt", multiline=True
                ),
                "negative_prompt": model_field_to_node_input(
                    IO.STRING,
                    KlingImage2VideoRequest,
                    "negative_prompt",
                    multiline=True,
                ),
                "model_name": model_field_to_node_input(
                    IO.COMBO,
                    KlingImage2VideoRequest,
                    "model_name",
                    enum_type=KlingVideoGenModelName,
                ),
                "cfg_scale": model_field_to_node_input(
                    IO.FLOAT, KlingImage2VideoRequest, "cfg_scale"
                ),
                "mode": model_field_to_node_input(
                    IO.COMBO,
                    KlingImage2VideoRequest,
                    "mode",
                    enum_type=KlingVideoGenMode,
                ),
                "aspect_ratio": model_field_to_node_input(
                    IO.COMBO,
                    KlingImage2VideoRequest,
                    "aspect_ratio",
                    enum_type=KlingVideoGenAspectRatio,
                ),
                "duration": model_field_to_node_input(
                    IO.COMBO,
                    KlingImage2VideoRequest,
                    "duration",
                    enum_type=KlingVideoGenDuration,
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = ("VIDEO", "STRING", "STRING")
    RETURN_NAMES = ("VIDEO", "video_id", "duration")
    DESCRIPTION = "Kling Image to Video Node"

    def get_response(self, task_id: str, auth_token: str) -> KlingImage2VideoResponse:
        return poll_until_finished(
            auth_token,
            ApiEndpoint(
                path=f"{PATH_IMAGE_TO_VIDEO}/{task_id}",
                method=HttpMethod.GET,
                request_model=KlingImage2VideoRequest,
                response_model=KlingImage2VideoResponse,
            ),
        )

    def api_call(
        self,
        start_frame: torch.Tensor,
        prompt: str,
        negative_prompt: str,
        model_name: str,
        cfg_scale: float,
        mode: str,
        aspect_ratio: str,
        duration: str,
        camera_control: Optional[KlingCameraControl] = None,
        end_frame: Optional[torch.Tensor] = None,
        auth_token: Optional[str] = None,
    ) -> tuple[VideoFromFile]:
        validate_prompts(prompt, negative_prompt, MAX_PROMPT_LENGTH_I2V)
        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=PATH_IMAGE_TO_VIDEO,
                method=HttpMethod.POST,
                request_model=KlingImage2VideoRequest,
                response_model=KlingImage2VideoResponse,
            ),
            request=KlingImage2VideoRequest(
                model_name=KlingVideoGenModelName(model_name),
                image=tensor_to_base64_string(start_frame),
                image_tail=(
                    tensor_to_base64_string(end_frame)
                    if end_frame is not None
                    else None
                ),
                prompt=prompt,
                negative_prompt=negative_prompt if negative_prompt else None,
                cfg_scale=cfg_scale,
                mode=KlingVideoGenMode(mode),
                aspect_ratio=KlingVideoGenAspectRatio(aspect_ratio),
                duration=KlingVideoGenDuration(duration),
                camera_control=camera_control,
            ),
            auth_token=auth_token,
        )

        task_creation_response = initial_operation.execute()
        validate_task_creation_response(task_creation_response)
        task_id = task_creation_response.data.task_id

        final_response = self.get_response(task_id, auth_token)
        validate_video_result_response(final_response)

        video = get_video_from_response(final_response)
        return video_result_to_node_output(video)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/kwai_vgi/kling-image-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-i2v)

[Kling Start-End Frame to VideoA node that creates smooth video transitions between start and end frames using Kling's AI technology  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-start-end-frame-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)