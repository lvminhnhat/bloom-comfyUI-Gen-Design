[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Development

##### ComfyUI Server

- [Server Overview](http://docs.comfy.org/essentials/comfyui-server/comms_overview)
- [Messages](http://docs.comfy.org/essentials/comfyui-server/comms_messages)
- [Execution Model Inversion Guide](http://docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide)

##### CLI

- [Getting Started](http://docs.comfy.org/comfy-cli/getting-started)
- [Reference](http://docs.comfy.org/comfy-cli/reference)

##### Develop Custom Nodes

- [Overview](http://docs.comfy.org/custom-nodes/overview)
- [Getting Started](http://docs.comfy.org/custom-nodes/walkthrough)
- Backend
  
  - [Properties](http://docs.comfy.org/custom-nodes/backend/server_overview)
  - [Lifecycle](http://docs.comfy.org/custom-nodes/backend/lifecycle)
  - [Publishing to the Manager](http://docs.comfy.org/custom-nodes/backend/manager)
  - [Datatypes](http://docs.comfy.org/custom-nodes/backend/datatypes)
  - [Images, Latents, and Masks](http://docs.comfy.org/custom-nodes/backend/images_and_masks)
  - [Hidden and Flexible inputs](http://docs.comfy.org/custom-nodes/backend/more_on_inputs)
  - [Lazy Evaluation](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation)
  - [Node Expansion](http://docs.comfy.org/custom-nodes/backend/expansion)
  - [Data lists](http://docs.comfy.org/custom-nodes/backend/lists)
  - [Annotated Examples](http://docs.comfy.org/custom-nodes/backend/snippets)
  - [Working with torch.Tensor](http://docs.comfy.org/custom-nodes/backend/tensors)
- UI
- [Workflow templates](http://docs.comfy.org/custom-nodes/workflow_templates)
- [Tips](http://docs.comfy.org/custom-nodes/tips)

##### Registry

- [Overview](http://docs.comfy.org/registry/overview)
- [Publishing Nodes](http://docs.comfy.org/registry/publishing)
- [Standards](http://docs.comfy.org/registry/standards)
- [Custom Node CI/CD](http://docs.comfy.org/registry/cicd)
- [pyproject.toml](http://docs.comfy.org/registry/specifications)
- [](http://docs.comfy.org/)

##### Specifications

- Workflow JSON
- Node Definitions

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

Hidden and Flexible inputs

# Hidden and Flexible inputs

## [​](http://docs.comfy.org#hidden-inputs) Hidden inputs

Alongside the `required` and `optional` inputs, which create corresponding inputs or widgets on the client-side, there are three `hidden` input options which allow the custom node to request certain information from the server.

These are accessed by returning a value for `hidden` in the `INPUT_TYPES` `dict`, with the signature `dict[str,str]`, containing one or more of `PROMPT`, `EXTRA_PNGINFO`, or `UNIQUE_ID`

```python
@classmethod
def INPUT_TYPES(s):
    return {
        "required": {...},
        "optional": {...},
        "hidden": {
            "unique_id": "UNIQUE_ID",
            "prompt": "PROMPT", 
            "extra_pnginfo": "EXTRA_PNGINFO",
        }
    }
```

### [​](http://docs.comfy.org#unique-id) UNIQUE\_ID

`UNIQUE_ID` is the unique identifier of the node, and matches the `id` property of the node on the client side. It is commonly used in client-server communications (see [messages](http://docs.comfy.org/essentials/comfyui-server/comms_messages#getting-node-id)).

### [​](http://docs.comfy.org#prompt) PROMPT

`PROMPT` is the complete prompt sent by the client to the server. See [the prompt object](http://docs.comfy.org/custom-nodes/js/javascript_objects_and_hijacking#prompt) for a full description.

### [​](http://docs.comfy.org#extra-pnginfo) EXTRA\_PNGINFO

`EXTRA_PNGINFO` is a dictionary that will be copied into the metadata of any `.png` files saved. Custom nodes can store additional information in this dictionary for saving (or as a way to communicate with a downstream node).

Note that if Comfy is started with the `disable_metadata` option, this data won’t be saved.

### [​](http://docs.comfy.org#dynprompt) DYNPROMPT

`DYNPROMPT` is an instance of `comfy_execution.graph.DynamicPrompt`. It differs from `PROMPT` in that it may mutate during the course of execution in response to [Node Expansion](http://docs.comfy.org/custom-nodes/backend/expansion).

`DYNPROMPT` should only be used for advanced cases (like implementing loops in custom nodes).

## [​](http://docs.comfy.org#flexible-inputs) Flexible inputs

### [​](http://docs.comfy.org#custom-datatypes) Custom datatypes

If you want to pass data between your own custom nodes, you may find it helpful to define a custom datatype. This is (almost) as simple as just choosing a name for the datatype, which should be a unique string in upper case, such as `CHEESE`.

You can then use `CHEESE` in your node `INPUT_TYPES` and `RETURN_TYPES`, and the Comfy client will only allow `CHEESE` outputs to connect to a `CHEESE` input. `CHEESE` can be any python object.

The only point to note is that because the Comfy client doesn’t know about `CHEESE` you need (unless you define a custom widget for `CHEESE`, which is a topic for another day), to force it to be an input rather than a widget. This can be done with the `forceInput` option in the input options dictionary:

```python
@classmethod
def INPUT_TYPES(s):
    return {
        "required": { "my_cheese": ("CHEESE", {"forceInput":True}) }
    }
```

### [​](http://docs.comfy.org#wildcard-inputs) Wildcard inputs

```python
@classmethod
def INPUT_TYPES(s):
    return {
        "required": { "anything": ("*",{})},
    }

@classmethod
def VALIDATE_INPUTS(s, input_types):
    return True
```

The frontend allows `*` to indicate that an input can be connected to any source. Because this is not officially supported by the backend, you can skip the backend validation of types by accepting a parameter named `input_types` in your `VALIDATE_INPUTS` function. (See [VALIDATE\_INPUTS](http://docs.comfy.org/server_overview#validate-inputs) for more information.) It’s up to the node to make sense of the data that is passed.

### [​](http://docs.comfy.org#dynamically-created-inputs) Dynamically created inputs

If inputs are dynamically created on the client side, they can’t be defined in the Python source code. In order to access this data we need an `optional` dictionary that allows Comfy to pass data with arbitrary names. Since the Comfy server

```python
class ContainsAnyDict(dict):
    def __contains__(self, key):
        return True
...

@classmethod
def INPUT_TYPES(s):
    return {
        "required": {},
        "optional": ContainsAnyDict()
    }
...

def main_method(self, **kwargs):
    # the dynamically created input data will be in the dictionary kwargs

```

Hat tip to rgthree for this pythonic trick!

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/more_on_inputs.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/images_and_masks)

[Lazy Evaluation  
\
Next](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Hidden inputs](http://docs.comfy.org#hidden-inputs)
- [UNIQUE\_ID](http://docs.comfy.org#unique-id)
- [PROMPT](http://docs.comfy.org#prompt)
- [EXTRA\_PNGINFO](http://docs.comfy.org#extra-pnginfo)
- [DYNPROMPT](http://docs.comfy.org#dynprompt)
- [Flexible inputs](http://docs.comfy.org#flexible-inputs)
- [Custom datatypes](http://docs.comfy.org#custom-datatypes)
- [Wildcard inputs](http://docs.comfy.org#wildcard-inputs)
- [Dynamically created inputs](http://docs.comfy.org#dynamically-created-inputs)