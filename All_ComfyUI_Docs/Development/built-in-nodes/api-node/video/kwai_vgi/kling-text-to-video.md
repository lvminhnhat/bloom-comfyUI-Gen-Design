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

Kling Text to Video - ComfyUI Built-in Node

# Kling Text to Video - ComfyUI Built-in Node

A node that converts text descriptions into videos using Kling’s AI technology

The Kling Text to Video node connects to Kling’s API service to generate videos from text descriptions. Users simply provide descriptive text to create corresponding video content.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionpromptString""Text prompt describing desired video contentnegative\_promptString""Elements to avoid in the videocfg\_scaleFloat7.0Controls how closely to follow the promptmodel\_nameSelect”kling-v2-master”Video generation model to useaspect\_ratioSelectAspectRatio enumOutput video aspect ratiodurationSelectDuration enumLength of generated videomodeSelectMode enumVideo generation mode

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated videoKling IDStringTask identifierDuration (sec)StringVideo length in seconds

## [​](http://docs.comfy.org#how-it-works) How It Works

The node sends text prompts to Kling’s API server, which processes and returns the generated video. The process includes initial request and status polling. When complete, the node downloads and outputs the video.

Users can control the generation by adjusting parameters like negative prompts, configuration scale, and video properties. The system validates prompt length to ensure API compliance.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class KlingTextToVideoNode(KlingNodeBase):
    """Kling Text to Video Node"""

    @staticmethod
    def poll_for_task_status(task_id: str, auth_token: str) -> KlingText2VideoResponse:
        """Polls the Kling API endpoint until the task reaches a terminal state."""
        polling_operation = PollingOperation(
            poll_endpoint=ApiEndpoint(
                path=f"{PATH_TEXT_TO_VIDEO}/{task_id}",
                method=HttpMethod.GET,
                request_model=EmptyRequest,
                response_model=KlingText2VideoResponse,
            ),
            completed_statuses=[
                TaskStatus.succeed.value,
            ],
            failed_statuses=[TaskStatus.failed.value],
            status_extractor=lambda response: (
                response.data.task_status.value
                if response.data and response.data.task_status
                else None
            ),
            auth_token=auth_token,
        )
        return polling_operation.execute()

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": model_field_to_node_input(
                    IO.STRING, KlingText2VideoRequest, "prompt", multiline=True
                ),
                "negative_prompt": model_field_to_node_input(
                    IO.STRING, KlingText2VideoRequest, "negative_prompt", multiline=True
                ),
                "model_name": model_field_to_node_input(
                    IO.COMBO,
                    KlingText2VideoRequest,
                    "model_name",
                    enum_type=ModelName,
                    default="kling-v2-master",
                ),
                "cfg_scale": model_field_to_node_input(
                    IO.FLOAT, KlingText2VideoRequest, "cfg_scale"
                ),
                "mode": model_field_to_node_input(
                    IO.COMBO, KlingText2VideoRequest, "mode", enum_type=Mode
                ),
                "duration": model_field_to_node_input(
                    IO.COMBO, KlingText2VideoRequest, "duration", enum_type=Duration
                ),
                "aspect_ratio": model_field_to_node_input(
                    IO.COMBO,
                    KlingText2VideoRequest,
                    "aspect_ratio",
                    enum_type=AspectRatio,
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    RETURN_TYPES = ("VIDEO", "STRING", "STRING")
    RETURN_NAMES = ("VIDEO", "Kling ID", "Duration (sec)")
    DESCRIPTION = "Kling Text to Video Node"

    def api_call(
        self,
        prompt: str,
        negative_prompt: str,
        model_name: str,
        cfg_scale: float,
        mode: str,
        duration: int,
        aspect_ratio: str,
        camera_control: Optional[CameraControl] = None,
        auth_token: Optional[str] = None,
    ) -> tuple[VideoFromFile, str, str]:
        validate_prompts(prompt, negative_prompt, MAX_PROMPT_LENGTH_T2V)
        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=PATH_TEXT_TO_VIDEO,
                method=HttpMethod.POST,
                request_model=KlingText2VideoRequest,
                response_model=KlingText2VideoResponse,
            ),
            request=KlingText2VideoRequest(
                prompt=prompt if prompt else None,
                negative_prompt=negative_prompt if negative_prompt else None,
                duration=Duration(duration),
                mode=Mode(mode),
                model_name=ModelName(model_name),
                cfg_scale=cfg_scale,
                aspect_ratio=AspectRatio(aspect_ratio),
                camera_control=camera_control,
            ),
            auth_token=auth_token,
        )

        initial_response = initial_operation.execute()
        if not is_valid_initial_response(initial_response):
            error_msg = f"Kling initial request failed. Code: {initial_response.code}, Message: {initial_response.message}, Data: {initial_response.data}"
            logging.error(error_msg)
            raise KlingApiError(error_msg)

        task_id = initial_response.data.task_id
        final_response = self.poll_for_task_status(task_id, auth_token)
        if not is_valid_video_response(final_response):
            error_msg = (
                f"Kling task {task_id} succeeded but no video data found in response."
            )
            logging.error(error_msg)
            raise KlingApiError(error_msg)

        video = final_response.data.task_result.videos[0]
        logging.debug("Kling task %s succeeded. Video URL: %s", task_id, video.url)
        return (
            download_url_to_video_output(video.url),
            str(video.id),
            str(video.duration),
        )

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/kwai_vgi/kling-text-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-controls)

[Kling Image to Video (Camera Control)Image to video conversion node with camera control features  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-i2v)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)