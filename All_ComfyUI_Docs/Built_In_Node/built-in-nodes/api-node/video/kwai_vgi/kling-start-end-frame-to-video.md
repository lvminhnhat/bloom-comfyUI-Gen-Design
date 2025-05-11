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

Kling Start-End Frame to Video - ComfyUI Built-in Node

# Kling Start-End Frame to Video - ComfyUI Built-in Node

A node that creates smooth video transitions between start and end frames using Kling’s AI technology

The Kling Start-End Frame to Video node lets you create smooth video transitions between two images. It automatically generates all the intermediate frames to produce a fluid transformation.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterTypeDescriptionstart\_frameImageStarting image for the videoend\_frameImageEnding image for the videopromptStringText describing video content and transitionnegative\_promptStringElements to avoid in the videocfg\_scaleFloatControls how closely to follow the promptaspect\_ratioSelectOutput video aspect ratiomodeSelectVideo generation settings (mode/duration/model)

### [​](http://docs.comfy.org#mode-options) Mode Options

Available mode combinations:

- standard mode / 5s duration / kling-v1
- standard mode / 5s duration / kling-v1-5
- pro mode / 5s duration / kling-v1
- pro mode / 5s duration / kling-v1-5
- pro mode / 5s duration / kling-v1-6
- pro mode / 10s duration / kling-v1-5
- pro mode / 10s duration / kling-v1-6

Default: “pro mode / 5s duration / kling-v1”

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#how-it-works) How It Works

The node analyzes the start and end frames to create a smooth transition sequence between them. It sends the images and parameters to Kling’s API server, which generates all necessary intermediate frames for a fluid transformation.

The transition style and content can be guided using prompts, while negative prompts help avoid unwanted elements.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python


class KlingStartEndFrameNode(KlingImage2VideoNode):
    """
    Kling First Last Frame Node. This node allows creation of a video from a first and last frame. It calls the normal image to video endpoint, but only allows the subset of input options that support the `image_tail` request field.
    """

    @staticmethod
    def get_mode_string_mapping() -> dict[str, tuple[str, str, str]]:
        """
        Returns a mapping of mode strings to their corresponding (mode, duration, model_name) tuples.
        Only includes config combos that support the `image_tail` request field.
        """
        return {
            "standard mode / 5s duration / kling-v1": ("std", "5", "kling-v1"),
            "standard mode / 5s duration / kling-v1-5": ("std", "5", "kling-v1-5"),
            "pro mode / 5s duration / kling-v1": ("pro", "5", "kling-v1"),
            "pro mode / 5s duration / kling-v1-5": ("pro", "5", "kling-v1-5"),
            "pro mode / 5s duration / kling-v1-6": ("pro", "5", "kling-v1-6"),
            "pro mode / 10s duration / kling-v1-5": ("pro", "10", "kling-v1-5"),
            "pro mode / 10s duration / kling-v1-6": ("pro", "10", "kling-v1-6"),
        }

    @classmethod
    def INPUT_TYPES(s):
        modes = list(KlingStartEndFrameNode.get_mode_string_mapping().keys())
        return {
            "required": {
                "start_frame": model_field_to_node_input(
                    IO.IMAGE, KlingImage2VideoRequest, "image"
                ),
                "end_frame": model_field_to_node_input(
                    IO.IMAGE, KlingImage2VideoRequest, "image_tail"
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
                "cfg_scale": model_field_to_node_input(
                    IO.FLOAT, KlingImage2VideoRequest, "cfg_scale"
                ),
                "aspect_ratio": model_field_to_node_input(
                    IO.COMBO,
                    KlingImage2VideoRequest,
                    "aspect_ratio",
                    enum_type=AspectRatio,
                ),
                "mode": (
                    modes,
                    {
                        "default": modes[2],
                        "tooltip": "The configuration to use for the video generation following the format: mode / duration / model_name.",
                    },
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    DESCRIPTION = "Generate a video sequence that transitions between your provided start and end images. The node creates all frames in between, producing a smooth transformation from the first frame to the last."

    def parse_inputs_from_mode(self, mode: str) -> tuple[str, str, str]:
        """Parses the mode input into a tuple of (model_name, duration, mode)."""
        return KlingStartEndFrameNode.get_mode_string_mapping()[mode]

    def api_call(
        self,
        start_frame: torch.Tensor,
        end_frame: torch.Tensor,
        prompt: str,
        negative_prompt: str,
        cfg_scale: float,
        aspect_ratio: str,
        mode: str,
        auth_token: Optional[str] = None,
    ):
        mode, duration, model_name = self.parse_inputs_from_mode(mode)
        return super().api_call(
            prompt=prompt,
            negative_prompt=negative_prompt,
            model_name=model_name,
            start_frame=start_frame,
            cfg_scale=cfg_scale,
            mode=mode,
            aspect_ratio=aspect_ratio,
            duration=duration,
            end_frame=end_frame,
            auth_token=auth_token,
        )


```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/kwai_vgi/kling-start-end-frame-to-video.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-image-to-video)

[Kling Text to Video (Camera Control)A text to video generation node with camera control features  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-t2v)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Mode Options](http://docs.comfy.org#mode-options)
- [Output](http://docs.comfy.org#output)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)