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

Pika 2.2 Scenes - ComfyUI Built-in Node Documentation

# Pika 2.2 Scenes - ComfyUI Built-in Node Documentation

A node that creates coherent scene videos from multiple images using Pika AI

The Pika 2.2 Scenes node allows you to upload multiple images and generate a high-quality video incorporating these elements. It uses Pika’s 2.2 API to create smooth scene transitions between the images.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDefaultDescriptionprompt\_textstring""Text prompt describing video content and scenesnegative\_promptstring""Elements to exclude from the videoseedinteger0Random seed for generationingredients\_modeselect”creative”Image combination moderesolutionselectAPI defaultOutput video resolutiondurationselectAPI defaultOutput video lengthaspect\_ratiofloat1.7777777777777777 (16:9)Video aspect ratio, range 0.4-2.5

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionimage\_ingredient\_1imageFirst scene imageimage\_ingredient\_2imageSecond scene imageimage\_ingredient\_3imageThird scene imageimage\_ingredient\_4imageFourth scene imageimage\_ingredient\_5imageFifth scene image

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOvideoGenerated video

## [​](http://docs.comfy.org#how-it-works) How It Works

The Pika 2.2 Scenes node analyzes all input images and creates a video containing these image elements. The node sends the images and parameters to Pika’s API server, which processes them and returns the generated video.

Users can guide the video style and content through prompts, and exclude unwanted elements using negative prompts. The node supports up to 5 input images as ingredients and generates the final video based on the specified combination mode, resolution, duration, and aspect ratio.

## [​](http://docs.comfy.org#source-code) Source Code

```python

class PikaScenesV2_2(PikaNodeBase):
    """Pika 2.2 Scenes Node."""

    @classmethod
    def INPUT_TYPES(cls):
        image_ingredient_input = (
            IO.IMAGE,
            {"tooltip": "Image that will be used as ingredient to create a video."},
        )
        return {
            "required": {
                **cls.get_base_inputs_types(
                    PikaBodyGenerate22C2vGenerate22PikascenesPost,
                ),
                "ingredients_mode": model_field_to_node_input(
                    IO.COMBO,
                    PikaBodyGenerate22C2vGenerate22PikascenesPost,
                    "ingredientsMode",
                    enum_type=IngredientsMode,
                    default="creative",
                ),
                "aspect_ratio": model_field_to_node_input(
                    IO.FLOAT,
                    PikaBodyGenerate22C2vGenerate22PikascenesPost,
                    "aspectRatio",
                    step=0.001,
                    min=0.4,
                    max=2.5,
                    default=1.7777777777777777,
                ),
            },
            "optional": {
                "image_ingredient_1": image_ingredient_input,
                "image_ingredient_2": image_ingredient_input,
                "image_ingredient_3": image_ingredient_input,
                "image_ingredient_4": image_ingredient_input,
                "image_ingredient_5": image_ingredient_input,
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    DESCRIPTION = "Combine your images to create a video with the objects in them. Upload multiple images as ingredients and generate a high-quality video that incorporates all of them."
    RETURN_TYPES = ("VIDEO",)

    def api_call(
        self,
        prompt_text: str,
        negative_prompt: str,
        seed: int,
        resolution: str,
        duration: int,
        ingredients_mode: str,
        aspect_ratio: float,
        image_ingredient_1: Optional[torch.Tensor] = None,
        image_ingredient_2: Optional[torch.Tensor] = None,
        image_ingredient_3: Optional[torch.Tensor] = None,
        image_ingredient_4: Optional[torch.Tensor] = None,
        image_ingredient_5: Optional[torch.Tensor] = None,
        auth_token: Optional[str] = None,
    ) -> tuple[VideoFromFile]:
        """API call for Pika Scenes 2.2."""
        all_image_bytes_io = []
        for image in [
            image_ingredient_1,
            image_ingredient_2,
            image_ingredient_3,
            image_ingredient_4,
            image_ingredient_5,
        ]:
            if image is not None:
                image_bytes_io = tensor_to_bytesio(image)
                image_bytes_io.seek(0)
                all_image_bytes_io.append(image_bytes_io)

        # Prepare files data for multipart upload
        pika_files = [
            ("images", (f"image_{i}.png", image_bytes_io, "image/png"))
            for i, image_bytes_io in enumerate(all_image_bytes_io)
        ]

        # Prepare non-file data using the Pydantic model
        pika_request_data = PikaBodyGenerate22C2vGenerate22PikascenesPost(
            ingredientsMode=ingredients_mode,
            promptText=prompt_text,
            negativePrompt=negative_prompt,
            seed=seed,
            resolution=resolution,
            duration=duration,
            aspectRatio=aspect_ratio,
        )

        initial_operation = SynchronousOperation(
            endpoint=ApiEndpoint(
                path=PATH_PIKASCENES,
                method=HttpMethod.POST,
                request_model=PikaBodyGenerate22C2vGenerate22PikascenesPost,
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

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/pika/pika-scenes.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-text-to-video)

[Pika 2.2 Image to VideoA node that converts static images to dynamic videos using Pika AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-image-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)