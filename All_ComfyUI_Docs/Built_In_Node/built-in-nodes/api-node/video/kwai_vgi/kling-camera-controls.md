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

Kling Camera Controls - ComfyUI Built-in Node Documentation

# Kling Camera Controls - ComfyUI Built-in Node Documentation

A node that provides camera control parameters for Kling video generation

The Kling Camera Controls node defines virtual camera behavior parameters to control camera movement and view changes during Kling video generation.

## [​](http://docs.comfy.org#parameters) Parameters

ParameterTypeDefaultDescriptioncamera\_control\_typeSelect”simple”Preset camera motion types. simple: Custom camera movement; down\_back: Camera moves down and back; forward\_up: Camera moves forward and up; right\_turn\_forward: Rotate right and move forward; left\_turn\_forward: Rotate left and move forwardhorizontal\_movementFloat0Controls camera movement on horizontal axis (x-axis). Negative values move left, positive values move rightvertical\_movementFloat0Controls camera movement on vertical axis (y-axis). Negative values move down, positive values move uppanFloat0.5Controls camera rotation in vertical plane (x-axis). Negative values rotate down, positive values rotate uptiltFloat0Controls camera rotation in horizontal plane (y-axis). Negative values rotate left, positive values rotate rightrollFloat0Controls camera roll amount (z-axis). Negative values rotate counterclockwise, positive values rotate clockwisezoomFloat0Controls camera focal length. Negative values narrow field of view, positive values widen it

**Note**: At least one non-zero camera control parameter is required for the effect to work.

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptioncamera\_controlCAMERA\_CONTROLConfiguration object with camera settings

**Note**: Not all model and mode combinations support camera control. Please check the Kling API documentation for details.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python

class KlingCameraControls(KlingNodeBase):
    """Kling Camera Controls Node"""

    @classmethod
    def INPUT_TYPES(cls):
        return {
            "required": {
                "camera_control_type": (
                    IO.COMBO,
                    {
                        "options": [
                            camera_control_type.value
                            for camera_control_type in CameraType
                        ],
                        "default": "simple",
                        "tooltip": "Predefined camera movements type. simple: Customizable camera movement. down_back: Camera descends and moves backward. forward_up: Camera moves forward and tilts up. right_turn_forward: Rotate right and move forward. left_turn_forward: Rotate left and move forward.",
                    },
                ),
                "horizontal_movement": get_camera_control_input_config(
                    "Controls camera's movement along horizontal axis (x-axis). Negative indicates left, positive indicates right"
                ),
                "vertical_movement": get_camera_control_input_config(
                    "Controls camera's movement along vertical axis (y-axis). Negative indicates downward, positive indicates upward."
                ),
                "pan": get_camera_control_input_config(
                    "Controls camera's rotation in vertical plane (x-axis). Negative indicates downward rotation, positive indicates upward rotation.",
                    default=0.5,
                ),
                "tilt": get_camera_control_input_config(
                    "Controls camera's rotation in horizontal plane (y-axis). Negative indicates left rotation, positive indicates right rotation.",
                ),
                "roll": get_camera_control_input_config(
                    "Controls camera's rolling amount (z-axis). Negative indicates counterclockwise, positive indicates clockwise.",
                ),
                "zoom": get_camera_control_input_config(
                    "Controls change in camera's focal length. Negative indicates narrower field of view, positive indicates wider field of view.",
                ),
            }
        }

    DESCRIPTION = "Kling Camera Controls Node. Not all model and mode combinations support camera control. Please refer to the Kling API documentation for more information."
    RETURN_TYPES = ("CAMERA_CONTROL",)
    RETURN_NAMES = ("camera_control",)
    FUNCTION = "main"

    @classmethod
    def VALIDATE_INPUTS(
        cls,
        horizontal_movement: float,
        vertical_movement: float,
        pan: float,
        tilt: float,
        roll: float,
        zoom: float,
    ) -> bool | str:
        if not is_valid_camera_control_configs(
            [
                horizontal_movement,
                vertical_movement,
                pan,
                tilt,
                roll,
                zoom,
            ]
        ):
            return "Invalid camera control configs: at least one of the values must be non-zero"
        return True

    def main(
        self,
        camera_control_type: str,
        horizontal_movement: float,
        vertical_movement: float,
        pan: float,
        tilt: float,
        roll: float,
        zoom: float,
    ) -> tuple[CameraControl]:
        return (
            CameraControl(
                type=CameraType(camera_control_type),
                config=CameraConfig(
                    horizontal=horizontal_movement,
                    vertical=vertical_movement,
                    pan=pan,
                    roll=roll,
                    tilt=tilt,
                    zoom=zoom,
                ),
            ),
        )
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/kwai_vgi/kling-camera-controls.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/google/google-veo2-video)

[Kling Text to VideoA node that converts text descriptions into videos using Kling's AI technology  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/kwai_vgi/kling-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)