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

Kling Text to Video (Camera Control) - ComfyUI Built-in Node

# Kling Text to Video (Camera Control) - ComfyUI Built-in Node

A text to video generation node with camera control features

The Kling Text to Video (Camera Control) node converts text into videos with professional camera movements. It extends the standard Kling Text to Video node by adding camera control capabilities.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionpromptString""Text prompt describing video contentnegative\_promptString""Elements to avoid in the videocfg\_scaleFloat7.0Controls how closely to follow the promptaspect\_ratioSelect”16:9”Output video aspect ratiocamera\_controlCAMERA\_CONTROL-Camera settings from Kling Camera Controls node

### [​](http://docs.comfy.org#fixed-parameters) Fixed Parameters

Note: The following parameters are fixed and cannot be changed:

- Model: kling-v1-5
- Mode: pro
- Duration: 5 seconds

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionVIDEOVideoGenerated video

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class KlingCameraControlT2VNode(KlingTextToVideoNode):
    """
    Kling Text to Video Camera Control Node. This node is a text to video node, but it supports controlling the camera.
    Duration, mode, and model_name request fields are hard-coded because camera control is only supported in pro mode with the kling-v1-5 model at 5s duration as of 2025-05-02.
    """

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "prompt": model_field_to_node_input(
                    IO.STRING, KlingText2VideoRequest, "prompt", multiline=True
                ),
                "negative_prompt": model_field_to_node_input(
                    IO.STRING,
                    KlingText2VideoRequest,
                    "negative_prompt",
                    multiline=True,
                ),
                "cfg_scale": model_field_to_node_input(
                    IO.FLOAT, KlingText2VideoRequest, "cfg_scale"
                ),
                "aspect_ratio": model_field_to_node_input(
                    IO.COMBO,
                    KlingText2VideoRequest,
                    "aspect_ratio",
                    enum_type=AspectRatio,
                ),
                "camera_control": (
                    "CAMERA_CONTROL",
                    {
                        "tooltip": "Can be created using the Kling Camera Controls node. Controls the camera movement and motion during the video generation.",
                    },
                ),
            },
            "hidden": {"auth_token": "AUTH_TOKEN_COMFY_ORG"},
        }

    DESCRIPTION = "Transform text into cinematic videos with professional camera movements that simulate real-world cinematography. Control virtual camera actions including zoom, rotation, pan, tilt, and first-person view, while maintaining focus on your original text."

    def api_call(
        self,
        prompt: str,
        negative_prompt: str,
        cfg_scale: float,
        aspect_ratio: str,
        camera_control: Optional[CameraControl] = None,
        auth_token: Optional[str] = None,
    ):
        return super().api_call(
            model_name="kling-v1-5",
            cfg_scale=cfg_scale,
            mode="pro",
            aspect_ratio=aspect_ratio,
            duration="5",
            prompt=prompt,
            negative_prompt=negative_prompt,
            camera_control=camera_control,
            auth_token=auth_token,
        )



```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/kwai_vgi/kling-camera-control-t2v.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-start-end-frame-to-video)

[Luma Text to VideoA node that converts text descriptions to videos using Luma AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Fixed Parameters](http://docs.comfy.org#fixed-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)