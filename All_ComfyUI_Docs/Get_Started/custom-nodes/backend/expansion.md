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

Node Expansion

# Node Expansion

## [​](http://docs.comfy.org#node-expansion) Node Expansion

Normally, when a node is executed, that execution function immediately returns the output results of that node. “Node Expansion” is a relatively advanced technique that allows nodes to return a new subgraph of nodes that should take its place in the graph. This technique is what allows custom nodes to implement loops.

### [​](http://docs.comfy.org#a-simple-example) A Simple Example

First, here’s a simple example of what node expansion looks like:

We highly recommend using the `GraphBuilder` class when creating subgraphs. It isn’t mandatory, but it prevents you from making many easy mistakes.

```python
def load_and_merge_checkpoints(self, checkpoint_path1, checkpoint_path2, ratio):
    from comfy_execution.graph_utils import GraphBuilder # Usually at the top of the file
    graph = GraphBuilder()
    checkpoint_node1 = graph.node("CheckpointLoaderSimple", checkpoint_path=checkpoint_path1)
    checkpoint_node2 = graph.node("CheckpointLoaderSimple", checkpoint_path=checkpoint_path2)
    merge_model_node = graph.node("ModelMergeSimple", model1=checkpoint_node1.out(0), model2=checkpoint_node2.out(0), ratio=ratio)
    merge_clip_node = graph.node("ClipMergeSimple", clip1=checkpoint_node1.out(1), clip2=checkpoint_node2.out(1), ratio=ratio)
    return {
        # Returning (MODEL, CLIP, VAE) outputs
        "result": (merge_model_node.out(0), merge_clip_node.out(0), checkpoint_node1.out(2)),
        "expand": graph.finalize(),
    }
```

While this same node could previously be implemented by manually calling into ComfyUI internals, using expansion means that each subnode will be cached separately (so if you change `model2`, you don’t have to reload `model1`).

### [​](http://docs.comfy.org#requirements) Requirements

In order to perform node expansion, a node must return a dictionary with the following keys:

1. `result`: A tuple of the outputs of the node. This may be a mix of finalized values (like you would return from a normal node) and node outputs.
2. `expand`: The finalized graph to perform expansion on. See below if you are not using the `GraphBuilder`.

#### [​](http://docs.comfy.org#additional-requirements-if-not-using-graphbuilder) Additional Requirements if not using GraphBuilder

The format expected from the `expand` key is the same as the ComfyUI API format. The following requirements are handled by the `GraphBuilder`, but must be handled manually if you choose to forego it:

1. Node IDs must be unique across the entire graph. (This includes between multiple executions of the same node due to the use of lists.)
2. Node IDs must be deterministic and consistent between multiple executions of the graph (including partial executions due to caching).

Even if you don’t want to use the `GraphBuilder` for actually building the graph (e.g. because you’re loading the raw json of the graph from a file), you can use the `GraphBuilder.alloc_prefix()` function to generate a prefix and `comfy.graph_utils.add_graph_prefix` to fix existing graphs to meet these requirements.

### [​](http://docs.comfy.org#efficient-subgraph-caching) Efficient Subgraph Caching

While you can pass non-literal inputs to nodes within the subgraph (like torch tensors), this can inhibit caching *within* the subgraph. When possible, you should pass links to subgraph objects rather than the node itself. (You can declare an input as a `rawLink` within the input’s [Additional Parameters](http://docs.comfy.org/datatypes#additional-parameters) to do this easily.)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/backend/expansion.mdx)

[Previous](http://docs.comfy.org/custom-nodes/backend/lazy_evaluation)

[Data lists  
\
Next](http://docs.comfy.org/custom-nodes/backend/lists)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Expansion](http://docs.comfy.org#node-expansion)
- [A Simple Example](http://docs.comfy.org#a-simple-example)
- [Requirements](http://docs.comfy.org#requirements)
- [Additional Requirements if not using GraphBuilder](http://docs.comfy.org#additional-requirements-if-not-using-graphbuilder)
- [Efficient Subgraph Caching](http://docs.comfy.org#efficient-subgraph-caching)