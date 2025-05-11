[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Built-in Nodes

- [Overview](http://docs.comfy.org/built-in-nodes/overview)

##### API Node

- Image
  
  - BFL
  - Luma
  - Recraft
    
    - [Save SVG](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/save-svg)
    - [Recraft Style - Realistic Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-realistic-image)
    - [Recraft Text to Vector](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-vector)
    - [Recraft Creative Upscale](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-creative-upscale)
    - [Recraft Image to Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-to-image)
    - [Recraft Crisp Upscale](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-crisp-upscale)
    - [Recraft Color RGB](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-color-rgb)
    - [Recraft Text to Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-text-to-image)
    - [Recraft Image Inpainting](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-inpainting)
    - [Recraft Vectorize Image](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-vectorize-image)
    - [Recraft Style - Digital Illustration](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-digital-illustration)
    - [Recraft Remove Background](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-remove-background)
    - [Recraft Style - Logo Raster](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-logo-raster)
    - [Recraft Controls](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-controls)
    - [Recraft Replace Background](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-replace-background)
  - Ideogram
  - Stability AI
  - OpenAI
- Video

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

Recraft Crisp Upscale - ComfyUI Native Node Documentation

# Recraft Crisp Upscale - ComfyUI Native Node Documentation

A Recraft API node that enhances image clarity and resolution using AI

The Recraft Crisp Upscale node uses Recraft’s API to improve image resolution and clarity.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionimageimage-Input image to be upscaled

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionIMAGEimageUpscaled and enhanced output image

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python
class RecraftCrispUpscaleNode:
    """
    Upscale image synchronously.
    Enhances a given raster image using ‘crisp upscale’ tool, increasing image resolution, making the image sharper and cleaner.
    """

    RETURN_TYPES = (IO.IMAGE,)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "api_call"
    API_NODE = True
    CATEGORY = "api node/image/Recraft"

    RECRAFT_PATH = "/proxy/recraft/images/crispUpscale"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "image": (IO.IMAGE, ),
            },
            "optional": {
            },
            "hidden": {
                "auth_token": "AUTH_TOKEN_COMFY_ORG",
            },
        }

    def api_call(
        self,
        image: torch.Tensor,
        auth_token=None,
        **kwargs,
    ):
        images = []
        total = image.shape[0]
        pbar = ProgressBar(total)
        for i in range(total):
            sub_bytes = handle_recraft_file_request(
                image=image[i],
                path=self.RECRAFT_PATH,
                auth_token=auth_token,
            )
            images.append(torch.cat([bytesio_to_image_tensor(x) for x in sub_bytes], dim=0))
            pbar.update(1)

        images_tensor = torch.cat(images, dim=0)
        return (images_tensor,)
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/recraft-crisp-upscale.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-image-to-image)

[Recraft Color RGBHelper node for defining color controls in Recraft image generation  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-color-rgb)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Source Code](http://docs.comfy.org#source-code)