[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
- Video
  
  - MiniMax
  - Google
    
    - [Google Veo2 Video](http://docs.comfy.org/built-in-nodes/api-node/video/google/google-veo2-video)
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

Google Veo2 Video - ComfyUI Native Node Documentation

# Google Veo2 Video - ComfyUI Native Node Documentation

A node that generates videos from text descriptions using Google’s Veo2 technology

The Google Veo2 Video node generates high-quality videos from text descriptions using Google’s Veo2 API technology, converting text prompts into dynamic video content.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptstring""Text description of the video content to generateaspect\_ratioselect”16:9”Output video aspect ratio, “16:9” or “9:16”negative\_promptstring""Text describing what to avoid in the videoduration\_secondsinteger5Video duration, 5-8 secondsenhance\_promptbooleanTrueWhether to use AI to enhance the promptperson\_generationselect”ALLOW”Allow or block person generation, “ALLOW” or “BLOCK”seedinteger0Random seed, 0 means randomly generated

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDefaultDescriptionimageimageNoneOptional reference image to guide video creation

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class VeoVideoGenerationNode(ComfyNodeABC):
    """
    Generates videos from text prompts using Google's Veo API.

    This node can create videos from text descriptions and optional image inputs,
    with control over parameters like aspect ratio, duration, and more.
    """

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Text description of the video",
                    },
                ),
                "aspect_ratio": (
                    IO.COMBO,
                    {
                        "options": ["16:9", "9:16"],
                        "default": "16:9",
                        "tooltip": "Aspect ratio of the output video",
                    },
                ),
            },
            "optional": {
                "negative_prompt": (
                    IO.STRING,
                    {
                        "multiline": True,
                        "default": "",
                        "tooltip": "Negative text prompt to guide what to avoid in the video",
                    },
                ),
                "duration_seconds": (
                    IO.INT,
                    {
                        "default": 5,
                        "min": 5,
                        "max": 8,
                        "step": 1,
                        "display": "number",
                        "tooltip": "Duration of the output video in seconds",
                    },
                ),
                "enhance_prompt": (
                    IO.BOOLEAN,
                    {
                        "default": True,
                        "tooltip": "Whether to enhance the prompt with AI assistance",
                    }
                ),
                "person_generation": (
                    IO.COMBO,
                    {
                        "options": ["ALLOW", "BLOCK"],
                        "default": "ALLOW",
                        "tooltip": "Whether to allow generating people in the video",
                    },
                ),
                "seed": (
                    IO.INT,
                    {
                        "default": 0,
                        "min": 0,
                        "max": 0xFFFFFFFF,
                        "step": 1,
                        "display": "number",
                        "control_after_generate": True,
                        "tooltip": "Seed for video generation (0 for random)",
                    },
                ),
                "image": (IO.IMAGE, {
                    "default": None,
                    "tooltip": "Optional reference image to guide video generation",
                }),
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    RETURN_TYPES = (IO.VIDEO,)
    FUNCTION = "generate_video"
    CATEGORY = "api node/video/Veo"
    DESCRIPTION = "Generates videos from text prompts using Google's Veo API"
    API_NODE = True

    def generate_video(
        self,
        prompt,
        aspect_ratio="16:9",
        negative_prompt="",
        duration_seconds=5,
        enhance_prompt=True,
        person_generation="ALLOW",
        seed=0,
        image=None,
        auth_token=None,
    ):
        # Prepare the instances for the request
        instances = []

        instance = {
            "prompt": prompt
        }

        # Add image if provided
        if image is not None:
            image_base64 = convert_image_to_base64(image)
            if image_base64:
                instance["image"] = {
                    "bytesBase64Encoded": image_base64,
                    "mimeType": "image/png"
                }

        instances.append(instance)

        # Create parameters dictionary
        parameters = {
            "aspectRatio": aspect_ratio,
            "personGeneration": person_generation,
            "durationSeconds": duration_seconds,
            "enhancePrompt": enhance_prompt,
        }

        # Add optional parameters if provided
        if negative_prompt:
            parameters["negativePrompt"] = negative_prompt
        if seed > 0:
            parameters["seed"] = seed

        # Initial request to start video generation
        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path="/proxy/veo/generate",
                method=HttpMethod.POST,
                request_model=Veo2GenVidRequest,
                response_model=Veo2GenVidResponse
            ),
            request=Veo2GenVidRequest(
                instances=instances,
                parameters=parameters
            ),
            auth_token=auth_token
        )

        initial_response = initial_operation.execute()
        operation_name = initial_response.name

        logging.info(f"Veo generation started with operation name: {operation_name}")

        # Define status extractor function
        def status_extractor(response):
            # Only return "completed" if the operation is done, regardless of success or failure
            # We'll check for errors after polling completes
            return "completed" if response.done else "pending"

        # Define progress extractor function
        def progress_extractor(response):
            # Could be enhanced if the API provides progress information
            return None

        # Define the polling operation
        poll_operation = PollingOperation(
            poll_endpoint=ApiEndpoint(
                path="/proxy/veo/poll",
                method=HttpMethod.POST,
                request_model=Veo2GenVidPollRequest,
                response_model=Veo2GenVidPollResponse
            ),
            completed_statuses=["completed"],
            failed_statuses=[],  # No failed statuses, we'll handle errors after polling
            status_extractor=status_extractor,
            progress_extractor=progress_extractor,
            request=Veo2GenVidPollRequest(
                operationName=operation_name
            ),
            auth_token=auth_token,
            poll_interval=5.0
        )

        # Execute the polling operation
        poll_response = poll_operation.execute()

        # Now check for errors in the final response
        # Check for error in poll response
        if hasattr(poll_response, 'error') and poll_response.error:
            error_message = f"Veo API error: {poll_response.error.message} (code: {poll_response.error.code})"
            logging.error(error_message)
            raise Exception(error_message)

        # Check for RAI filtered content
        if (hasattr(poll_response.response, 'raiMediaFilteredCount') and
            poll_response.response.raiMediaFilteredCount > 0):

            # Extract reason message if available
            if (hasattr(poll_response.response, 'raiMediaFilteredReasons') and
                poll_response.response.raiMediaFilteredReasons):
                reason = poll_response.response.raiMediaFilteredReasons[0]
                error_message = f"Content filtered by Google's Responsible AI practices: {reason} ({poll_response.response.raiMediaFilteredCount} videos filtered.)"
            else:
                error_message = f"Content filtered by Google's Responsible AI practices ({poll_response.response.raiMediaFilteredCount} videos filtered.)"

            logging.error(error_message)
            raise Exception(error_message)

        # Extract video data
        video_data = None
        if poll_response.response and hasattr(poll_response.response, 'videos') and poll_response.response.videos and len(poll_response.response.videos) > 0:
            video = poll_response.response.videos[0]

            # Check if video is provided as base64 or URL
            if hasattr(video, 'bytesBase64Encoded') and video.bytesBase64Encoded:
                # Decode base64 string to bytes
                video_data = base64.b64decode(video.bytesBase64Encoded)
            elif hasattr(video, 'gcsUri') and video.gcsUri:
                # Download from URL
                video_url = video.gcsUri
                video_response = requests.get(video_url)
                video_data = video_response.content
            else:
                raise Exception("Video returned but no data or URL was provided")
        else:
            raise Exception("Video generation completed but no video was returned")

        if not video_data:
            raise Exception("No video data was returned")

        logging.info("Video generation completed successfully")

        # Convert video data to BytesIO object
        video_io = io.BytesIO(video_data)

        # Return VideoFromFile object
        return (VideoFromFile(video_io),)

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/google/google-veo2-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/minimax/minimax-text-to-video)

[Kling Camera ControlsA node that provides camera control parameters for Kling video generation  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-controls)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)