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
    
    - [Luma Text to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-text-to-video)
    - [Luma Image to Video](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video)
    - [Luma Concepts](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-concepts)
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

Luma Concepts - ComfyUI Native Node Documentation

# Luma Concepts - ComfyUI Native Node Documentation

A helper node that provides concept guidance for Luma image generation

The Luma Concepts node allows you to apply predefined camera concepts to the Luma generation process, providing precise control over camera angles and perspectives without complex prompt descriptions.

## [​](http://docs.comfy.org#node-function) Node Function

This node serves as a helper tool for Luma generation nodes, enabling users to select and apply predefined camera concepts. These concepts include different shooting angles (like overhead or low angle), camera distances (like close-up or long shot), and movement styles (like push-in or follow). It simplifies the creative workflow by providing an intuitive way to control camera effects in the generated output.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDescriptionconcept1selectFirst camera concept choice, includes various presets and “none”concept2selectSecond camera concept choice, includes various presets and “none”concept3selectThird camera concept choice, includes various presets and “none”concept4selectFourth camera concept choice, includes various presets and “none”

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterTypeDescriptionluma\_conceptsLUMA\_CONCEPTSOptional Camera Concepts to merge with selected concepts

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionluma\_conceptsLUMA\_CONCEPTCombined object containing all selected concepts

## [​](http://docs.comfy.org#usage-examples) Usage Examples

[**Luma Text to Video Workflow Example**  
\
Luma Text to Video Workflow Example](http://docs.comfy.org/tutorials/api-nodes/luma/luma-text-to-video)

[**Luma Image to Video Workflow Example**  
\
Luma Image to Video Workflow Example](http://docs.comfy.org/tutorials/api-nodes/luma/luma-image-to-video)

## [​](http://docs.comfy.org#how-it-works) How It Works

The Luma Concepts node offers a variety of predefined camera concepts including:

- Camera distances (close-up, medium shot, long shot)
- View angles (eye level, overhead, low angle)
- Movement types (push-in, follow, orbit)
- Special effects (handheld, stabilized, floating)

Users can select up to 4 concepts to use together. The node creates an object containing the selected camera concepts, which is then passed to Luma generation nodes. During generation, Luma AI uses these camera concepts to influence the viewpoint and composition of the output, ensuring the results reflect the chosen photographic effects.

By combining multiple camera concepts, users can create complex camera guidance without writing detailed prompt descriptions. This is particularly useful when specific camera angles or compositions are needed.

## [​](http://docs.comfy.org#source-code) Source Code

\[Node source code (Updated on 2025-05-03)]

```python

class LumaConceptsNode(ComfyNodeABC):
    """
    Holds one or more Camera Concepts for use with Luma Text to Video and Luma Image to Video nodes.
    """

    RETURN_TYPES = (LumaIO.LUMA_CONCEPTS,)
    RETURN_NAMES = ("luma_concepts",)
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "create_concepts"
    CATEGORY = "api node/image/Luma"

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "concept1": (get_luma_concepts(include_none=True),),
                "concept2": (get_luma_concepts(include_none=True),),
                "concept3": (get_luma_concepts(include_none=True),),
                "concept4": (get_luma_concepts(include_none=True),),
            },
            "optional": {
                "luma_concepts": (
                    LumaIO.LUMA_CONCEPTS,
                    {
                        "tooltip": "Optional Camera Concepts to add to the ones chosen here."
                    },
                ),
            },
        }

    def create_concepts(
        self,
        concept1: str,
        concept2: str,
        concept3: str,
        concept4: str,
        luma_concepts: LumaConceptChain = None,
    ):
        chain = LumaConceptChain(str_list=[concept1, concept2, concept3, concept4])
        if luma_concepts is not None:
            chain = luma_concepts.clone_and_merge(chain)
        return (chain,)


```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/video/luma/luma-concepts.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/video/luma/luma-image-to-video)

[Pika 2.2 Text to VideoA node that converts text descriptions into videos using Pika AI  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/video/pika/pika-text-to-video)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Examples](http://docs.comfy.org#usage-examples)
- [How It Works](http://docs.comfy.org#how-it-works)
- [Source Code](http://docs.comfy.org#source-code)