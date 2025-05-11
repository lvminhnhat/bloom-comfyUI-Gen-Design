[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
- Video
  
  - MiniMax
    
    - [MiniMax Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-image-to-video)
    - [MiniMax Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-text-to-video)
  - Google
  - Kling
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

MiniMax Text to Video - ComfyUI Native Node Documentation

# MiniMax Text to Video - ComfyUI Native Node Documentation

A node that converts text descriptions into videos using MiniMax AI

The MiniMax Text to Video node connects to MiniMax’s API to generate high-quality, smooth videos from text prompts. It supports different video generation models to create short video clips in various styles.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionprompt\_textString""Text prompt that guides the video generationmodelSelect”T2V-01”Video model to use, options are “T2V-01” and “T2V-01-Director”seedInteger0Random seed for noise generation, defaults to 0

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class MinimaxTextToVideoNode:
    """
    Generates videos synchronously based on a prompt, and optional parameters using Minimax's API.
    """

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt_text": (
                    "STRING",
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Text prompt to guide the video generation",
                    },
                ),
                "model": (
                    [
                        "T2V-01",
                        "T2V-01-Director",
                    ],
                    {
                        "default": "T2V-01",
                        "tooltip": "Model to use for video generation",
                    },
                ),
            },
            "optional": {
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 0xFFFFFFFFFFFFFFFF,
                        "control_after_generate": True,
                        "tooltip": "The random seed used for creating the noise.",
                    },
                ),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    RETURN_TYPES = ("VIDEO",)
    DESCRIPTION = "Generates videos from prompts using Minimax's API"
    FUNCTION = "generate_video"
    CATEGORY = "api node/video/Minimax"
    API_NODE = True
    OUTPUT_NODE = True

    def generate_video(
        self,
        prompt_text,
        seed=0,
        model="T2V-01",
        image: torch.Tensor=None, # used for ImageToVideo
        subject: torch.Tensor=None, # used for SubjectToVideo
        auth_token=None,
    ):
        '''
        Function used between Minimax nodes - supports T2V, I2V, and S2V, based on provided arguments.
        '''
        # upload image, if passed in
        image_url = None
        if image is not None:
            image_url = upload_images_to_comfyapi(image, max_images=1, auth_token=auth_token)[0]

        # TODO: figure out how to deal with subject properly, API returns invalid params when using S2V-01 model
        subject_reference = None
        if subject is not None:
            subject_url = upload_images_to_comfyapi(subject, max_images=1, auth_token=auth_token)[0]
            subject_reference = [SubjectReferenceItem(image=subject_url)]


        video_generate_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/minimax/video_generation",
                method=HttpMethod.POST,
                request_model=MinimaxVideoGenerationRequest,
                response_model=MinimaxVideoGenerationResponse,
            ),
            request=MinimaxVideoGenerationRequest(
                model=Model(model),
                prompt=prompt_text,
                callback_url=None,
                first_frame_image=image_url,
                subject_reference=subject_reference,
                prompt_optimizer=None,
            ),
            auth_token=auth_token,
        )
        response = video_generate_operation.execute()

        task_id = response.task_id
        if not task_id:
            raise Exception(f"Minimax generation failed: {response.base_resp}")

        video_generate_operation = PollingOperation(
            poll_endpoint=ApiEndpoint(
                path="/proxy/minimax/query/video_generation",
                method=HttpMethod.GET,
                request_model=EmptyRequest,
                response_model=MinimaxTaskResultResponse,
                query_params={"task_id": task_id},
            ),
            completed_statuses=["Success"],
            failed_statuses=["Fail"],
            status_extractor=lambda x: x.status.value,
            auth_token=auth_token,
        )
        task_result = video_generate_operation.execute()

        file_id = task_result.file_id
        if file_id is None:
            raise Exception("Request was not successful. Missing file ID.")
        file_retrieve_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/minimax/files/retrieve",
                method=HttpMethod.GET,
                request_model=EmptyRequest,
                response_model=MinimaxFileRetrieveResponse,
                query_params={"file_id": int(file_id)},
            ),
            request=EmptyRequest(),
            auth_token=auth_token,
        )
        file_result = file_retrieve_operation.execute()

        file_url = file_result.file.download_url
        if file_url is None:
            raise Exception(
                f"No video was found in the response. Full response: {file_result.model_dump()}"
            )
        logging.info(f"Generated video URL: {file_url}")

        video_io = download_url_to_bytesio(file_url)
        if video_io is None:
            error_msg = f"Failed to download video from {file_url}"
            logging.error(error_msg)
            raise Exception(error_msg)
        return (VideoFromFile(video_io),)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/minimax/minimax-text-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-image-to-video)

[Google Veo2 VideoA node that generates videos from text descriptions using Google's Veo2 technology  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/google/google-veo2-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)