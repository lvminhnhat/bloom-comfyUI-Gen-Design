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

Execution Model Inversion Guide

# Execution Model Inversion Guide

[PR #2666](https://github.com/comfyanonymous/ComfyUI/pull/2666) inverts the execution model from a back-to-front recursive model to a front-to-back topological sort. While most custom nodes should continue to “just work”, this page is intended to serve as a guide for custom node creators to the things that *could* break.

## [​](http://docs.comfy.org#breaking-changes) Breaking Changes

### [​](http://docs.comfy.org#monkey-patching) Monkey Patching

Any code that monkey patched the execution model is likely to stop working. Note that the performance of execution with this PR exceeds that with the most popular monkey patches, so many of them will be unnecessary.

### [​](http://docs.comfy.org#optional-input-validation) Optional Input Validation

Prior to this PR, only nodes that were connected to outputs exclusively through a string of `"required"` inputs were actually validated. If you had custom nodes that were only ever connected to `"optional"` inputs, you previously wouldn’t have been seeing that they failed validation.

If your nodes’ outputs could already be connected to `"required"` inputs, it is unlikely that anything in this section applies to you. It will primarily apply to custom node authors who use custom types and exclusively use `"optional"` inputs.

Here are some of the things that could cause you to fail validation along with recommended solutions:

- Use of reserved [Additional Parameters](http://docs.comfy.org/custom-nodes/backend/datatypes#additional-parameters) like `min` and `max` on types that aren’t comparable (e.g. dictionaries) in order to configure custom widgets.
  
  - Change the additional parameters used to non-reserved keys like `uiMin` and `uiMax`. *(Recommended Solution)*
    
    ```python
    @classmethod
    def INPUT_TYPES(cls):
        return {
            "required": {
                "my_size": ("VEC2", {"uiMin": 0.0, "uiMax": 1.0}),
            }
        }
    ```
  - Define a custom [VALIDATE\_INPUTS](http://docs.comfy.org/custom-nodes/backend/server_overview#validate-inputs) function with this input so validation of it is skipped. *(Quick Solution)*
    
    ```python
    @classmethod
    def VALIDATE_INPUTS(cls, my_size):
        return True
    ```
- Use of composite types (e.g. `CUSTOM_A,CUSTOM_B`)
  
  - (When used as output) Define and use a wrapper like `MakeSmartType` [seen here in the PR’s unit tests](https://github.com/comfyanonymous/ComfyUI/pull/2666/files#diff-714643f1fdb6f8798c45f77ab10d212ca7f41dd71bbe55069f1f9f146a8f0cb9R2)
    
    ```python
    class MyCustomNode:
    
        @classmethod
        def INPUT_TYPES(cls):
            return {
                "required": {
                    "input": (MakeSmartType("FOO,BAR"), {}),
                }
            }
    
        RETURN_TYPES = (MakeSmartType("FOO,BAR"),)
    
        # ...
    ```
  - (When used as input) Define a custom[VALIDATE\_INPUTS](http://docs.comfy.org/custom-nodes/backend/server_overview#validate-inputs) function that takes a `input_types` argument so type validation is skipped.
    
    ```python
    @classmethod
    def VALIDATE_INPUTS(cls, input_types):
        return True
    ```
  - (Supports both, convenient) Define and use the `@VariantSupport` decorator [seen here in the PR’s unit tests](https://github.com/comfyanonymous/ComfyUI/pull/2666/files#diff-714643f1fdb6f8798c45f77ab10d212ca7f41dd71bbe55069f1f9f146a8f0cb9R15)
    
    ```python
    @VariantSupport
    class MyCustomNode:
    
        @classmethod
        def INPUT_TYPES(cls):
            return {
                "required": {
                    "input": ("FOO,BAR", {}),
                }
            }
        
        RETURN_TYPES = (MakeSmartType("FOO,BAR"),)
    
        # ...
    ```
- The use of lists (e.g. `[1, 2, 3]`) as constants in the graph definition (e.g. to represent a const `VEC3` input). This would have required a front-end extension before. Previously, lists of size exactly `2` would have failed anyway — they would have been treated as broken links.
  
  - Wrap the lists in a dictionary like `{ "value": [1, 2, 3] }`

### [​](http://docs.comfy.org#execution-order) Execution Order

Execution order has always changed depending on which nodes happen to have which IDs, but it may now change depending on which values are cached as well. In general, the execution order should be considered non-deterministic and subject to change (beyond what is enforced by the graph’s structure).

Don’t rely on the execution order.

*HIC SUNT DRACONES*

## [​](http://docs.comfy.org#new-functionality) New Functionality

### [​](http://docs.comfy.org#validation-changes) Validation Changes

A number of features were added to the `VALIDATE_INPUTS` function in order to lessen the impact of the [Optional Input Validation](http://docs.comfy.org/_sites/docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide#optional-input-validation) mentioned above.

- Default validation will now be skipped for inputs which are received by the `VALIDATE_INPUTS` function.
- The `VALIDATE_INPUTS` function can now take `**kwargs` which causes all inputs to be treated as validated by the node creator.
- The `VALIDATE_INPUTS` function can take an input named `input_types`. This input will be a dict mapping each input (connected via a link) to the type of the connected output. When this argument exists, type validation for the node’s inputs is skipped.

You can read more at [VALIDATE\_INPUTS](http://docs.comfy.org/custom-nodes/backend/server_overview#validate-inputs).

### [​](http://docs.comfy.org#lazy-evaluation) Lazy Evaluation

Inputs can be evaluated lazily (i.e. you can wait to see if they are needed before evaluating the attached node and all its ancestors). See [Lazy Evaluation](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation) for more information.

### [​](http://docs.comfy.org#node-expansion) Node Expansion

At runtime, nodes can expand into a subgraph of nodes. This is what allows loops to be implemented (via tail-recursion). See [Node Expansion](http://docs.comfy.org/custom-nodes/backend/expansion) for more information.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/comfyui-server/execution_model_inversion_guide.mdx)

[Previous](http://docs.comfy.org/essentials/comfyui-server/comms_messages)

[Getting Started  
\
Next](http://docs.comfy.org/comfy-cli/getting-started)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Breaking Changes](http://docs.comfy.org#breaking-changes)
- [Monkey Patching](http://docs.comfy.org#monkey-patching)
- [Optional Input Validation](http://docs.comfy.org#optional-input-validation)
- [Execution Order](http://docs.comfy.org#execution-order)
- [New Functionality](http://docs.comfy.org#new-functionality)
- [Validation Changes](http://docs.comfy.org#validation-changes)
- [Lazy Evaluation](http://docs.comfy.org#lazy-evaluation)
- [Node Expansion](http://docs.comfy.org#node-expansion)