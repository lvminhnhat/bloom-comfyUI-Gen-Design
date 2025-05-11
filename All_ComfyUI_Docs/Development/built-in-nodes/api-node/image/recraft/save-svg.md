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

Save SVG - ComfyUI Built-in Node Documentation

# Save SVG - ComfyUI Built-in Node Documentation

A utility node for saving SVG vector graphics to files

The Save SVG node allows you to save SVG data from Recraft vector generation nodes as usable files in the filesystem. This is an essential component for handling and exporting vector graphics.

## [​](http://docs.comfy.org#node-function) Node Function

This node receives SVG vector data and saves it as standard SVG files in the filesystem. It supports automatic file naming and save path specification, allowing vector graphics to be opened and edited in other software.

## [​](http://docs.comfy.org#parameters) Parameters

### [​](http://docs.comfy.org#basic-parameters) Basic Parameters

ParameterTypeDefaultDescriptionsvgSVG-SVG vector data to savefilename\_prefixstring”recraft”Prefix for the filenameoutput\_dirstring-Output directory, defaults to ComfyUI output folder at `ComfyUI/output/svg/`indexinteger-1Save index, -1 means save all generated SVGs

### [​](http://docs.comfy.org#output) Output

OutputTypeDescriptionSVGSVGPasses through the input SVG data

## [​](http://docs.comfy.org#usage-example) Usage Example

[**Recraft Text to Image Workflow Example**  
\
Recraft Text to Image Workflow Example](http://docs.comfy.org/tutorials/api-nodes/recraft/recraft-text-to-image)

## [​](http://docs.comfy.org#source-code) Source Code

\[Node Source Code (Updated 2025-05-03)]

```python
class SaveSVGNode:
    """
    Save SVG files on disk.
    """

    def __init__(self):
        self.output_dir = folder_paths.get_output_directory()
        self.type = "output"
        self.prefix_append = ""

    RETURN_TYPES = ()
    DESCRIPTION = cleandoc(__doc__ or "")  # Handle potential None value
    FUNCTION = "save_svg"
    CATEGORY = "api node/image/Recraft"
    OUTPUT_NODE = True

    @classmethod
    def INPUT_TYPES(s):
        return {
            "required": {
                "svg": (RecraftIO.SVG,),
                "filename_prefix": ("STRING", {"default": "svg/ComfyUI", "tooltip": "The prefix for the file to save. This may include formatting information such as %date:yyyy-MM-dd% or %Empty Latent Image.width% to include values from nodes."})
            },
            "hidden": {
                "prompt": "PROMPT",
                "extra_pnginfo": "EXTRA_PNGINFO"
            }
        }

    def save_svg(self, svg: SVG, filename_prefix="svg/ComfyUI", prompt=None, extra_pnginfo=None):
        filename_prefix += self.prefix_append
        full_output_folder, filename, counter, subfolder, filename_prefix = folder_paths.get_save_image_path(filename_prefix, self.output_dir)
        results = list()

        # Prepare metadata JSON
        metadata_dict = {}
        if prompt is not None:
            metadata_dict["prompt"] = prompt
        if extra_pnginfo is not None:
            metadata_dict.update(extra_pnginfo)

        # Convert metadata to JSON string
        metadata_json = json.dumps(metadata_dict, indent=2) if metadata_dict else None

        for batch_number, svg_bytes in enumerate(svg.data):
            filename_with_batch_num = filename.replace("%batch_num%", str(batch_number))
            file = f"{filename_with_batch_num}_{counter:05}_.svg"

            # Read SVG content
            svg_bytes.seek(0)
            svg_content = svg_bytes.read().decode('utf-8')

            # Inject metadata if available
            if metadata_json:
                # Create metadata element with CDATA section
                metadata_element = f"""  <metadata>
    <![CDATA[
{metadata_json}
    ]]>
  </metadata>
"""
                # Insert metadata after opening svg tag using regex
                import re
                svg_content = re.sub(r'(<svg[^>]*>)', r'\1\n' + metadata_element, svg_content)

            # Write the modified SVG to file
            with open(os.path.join(full_output_folder, file), 'wb') as svg_file:
                svg_file.write(svg_content.encode('utf-8'))

            results.append({
                "filename": file,
                "subfolder": subfolder,
                "type": self.type
            })
            counter += 1
        return { "ui": { "images": results } }

```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/built-in-nodes/api-node/image/recraft/save-svg.mdx)

[Previous](http://docs.comfy.org/built-in-nodes/api-node/image/luma/luma-image-to-image)

[Recraft Style - Realistic ImageA helper node for setting realistic photo style in Recraft image generation  
\
Next](http://docs.comfy.org/built-in-nodes/api-node/image/recraft/recraft-style-realistic-image)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Function](http://docs.comfy.org#node-function)
- [Parameters](http://docs.comfy.org#parameters)
- [Basic Parameters](http://docs.comfy.org#basic-parameters)
- [Output](http://docs.comfy.org#output)
- [Usage Example](http://docs.comfy.org#usage-example)
- [Source Code](http://docs.comfy.org#source-code)